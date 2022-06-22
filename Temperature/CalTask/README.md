# Calibration Temperature data
## List of Files
|File Name| Description|
|:---|:---|
|[SRP-4_nospike_Temperature&SysData.xlsx](https://github.com/SRP-AM/SRP_AM_Prediction_Challenge/blob/main/Temperature/CalTask/SRP-4_nospike_Temperature%26SysData.xlsx)|Calibration task temperature and location, current voltage, and time data
[Temperature_Calibration_Sample_Model_Locations.xlsx](https://github.com/SRP-AM/SRP_AM_Prediction_Challenge/blob/main/Temperature/CalTask/Temperature_Calibration_Sample_Model_Locations.xlsx)|Template to input optional additional temperature simulated results–calibration.|

### SRP-4_nospike_Temperature&SysData.xlsx
The calibration temperature data is provided in SRP-4_nospike_Temperature&SysData.xlsx.
The first 5 rows provide background statistics for the experiment data (operator, wire, gas, etc.)
Columns are then delineated as follows:

- ***Column 1, Timestamp:*** Timestamp data formatted as \<hour\>:\<minute\>:\<second\>.
- ***Columns 2-13, Thermocouple \<number\>:***. Continuous data, temperature measurements in celsius for each thermocouple (total of 12).
- ***Column 14, Weld Voltage:*** Continuous data, measured in V (volts)
- ***Column 15, Weld Current:*** Continuous data, Measured in A (amperes)
- ***Column 16, Weld on:*** Binary data, indicates whether the power is on or off, 1 for on and 0 for off.
- ***Column 17-19, \<axis\> Position:*** Continuous data, print head locations (X, Y, Z) in mm. The origin is located in the center of the part.





```python
import pandas as pd
import dateutil
import numpy as np
from matplotlib import pyplot as plt
import matplotlib.dates as mdates


Tmp_npspike = pd.read_excel('SRP-4_nospike_Temperature&SysData.xlsx', skiprows=5)

times = np.array(Tmp_npspike)[:,0].astype(str)
Thermocouples = np.array(Tmp_npspike)[:,1:13].astype(float)
```

## Thermocouple Data

Here we provide a simple visualization of the thermocouple temperature data collected over time (Columns 2-13 of SRP-4_nospike_Temperature&SysData.xlsx). Note that the ambient and table temperatures are lower throughout the experiment, as we would expect.


```python

t = [dateutil.parser.parse(s) for s in times]

for i in [1, 2, 3, 4, 6, 7, 8, 9]:
    plt.plot(t, Thermocouples[:,i], color='tab:purple', linewidth=.5)
plt.plot([], [], color='tab:purple', label='Interior (2-5, 7-10)')

plt.plot(t, Thermocouples[:,0], label='Right end (1)')
plt.plot(t, Thermocouples[:,5], label='Left end (6)')
plt.plot(t, Thermocouples[:,-2], label='Table (11)', linestyle = '--')
plt.plot(t, Thermocouples[:,-1], label='Ambient (12)', linestyle = '--')


plt.legend(loc='center left', bbox_to_anchor=(1, 0.5), title='Thermocouple #')
plt.ylabel('Temperature (C)')
plt.xlabel('Time')
ax=plt.gca()
xfmt = mdates.DateFormatter('%H:%M:%S')
ax.xaxis.set_major_formatter(xfmt)
plt.title('Calibration Temperature Evolution')
plt.show()
```



![png](README/output_4_0.png)



## Weld on, weld off behavior

Here we provide a simple visualization for the weld on, weld off behavior (provided in column 16 of SRP-4_nospike_Temperature&SysData.xlsx).
Again, as we would expect, the temperature measured on the base plate thermocouples (1-10) decreases when the weld is off.


```python
weld_off = [t[i] for i in np.where(Tmp_npspike['Weld On'] == 0)[0]]

plt.vlines(weld_off, 0, 175, alpha=.01, color='tab:purple')
plt.plot([], [], color='tab:purple', linewidth='7', alpha=.25, label='Weld off')
plt.plot(t, Thermocouples[:,:10].mean(axis=1), label='Thermocouple Average (1-10)')

plt.legend(loc='center left', bbox_to_anchor=(1, 0.5))
plt.ylabel('Temperature (C)')
plt.xlabel('Time')
ax=plt.gca()
xfmt = mdates.DateFormatter('%H:%M:%S')
ax.xaxis.set_major_formatter(xfmt)
plt.title('Average Calibration Temperature vs Weld Power State')
plt.show()
```



![png](README/output_6_0.png)



## Power behavior

Here we visualize the power data, which was logged indirectly via the voltage and current (columns 14 and 15, respectively, of SRP-4_nospike_Temperature&SysData.xlsx).
The setup problem assumes constant power when the weld is on: we can calculate the average power in the on state to be approximately 2599.01452 Watts.


```python
Power = np.array(Tmp_npspike['Weld Voltage'] * Tmp_npspike['Weld Current'])

#plt.plot(t, Power)
plt.scatter(t, Power, s=.4)
plt.plot(t, np.ones_like(t)*Power[Power > 500].mean(), 'k--')
xfmt = mdates.DateFormatter('%H:%M:%S')
ax=plt.gca()
ax.xaxis.set_major_formatter(xfmt)
plt.title("Calibration power over time")
plt.xlabel('Time')
plt.ylabel('Power (watts)')
plt.show()
```



![png](README/output_8_0.png)



## Print Head Position

Here we demonstrate how to animate the behavior of the print head position over time, noting the weld on/weld off state.
This data is provided in columns 17-19 of SRP-4_nospike_Temperature&SysData.xlsx.
The print head movement in the weld-off state follows th

https://user-images.githubusercontent.com/7451908/175178817-33b4422d-758e-428a-b405-0e48b78f7136.mp4

e infill pattern as discussed in section 2.6 of the challenge_info_packet.


```python
import matplotlib.ticker as ticker
import mpl_toolkits.mplot3d.axes3d as p3
import matplotlib.animation as animation
from IPython.display import HTML

XYZ = np.array(Tmp_npspike[['X Position', 'Y Position', 'Z Position']])

fig = plt.figure(figsize=(10,10))
ax = plt.axes(projection='3d')
xlim = (np.min(XYZ[:,0])-10, np.max(XYZ[:,0])+10)
ylim = (np.min(XYZ[:,1])-10, np.max(XYZ[:,1])+10)
zlim = (np.min(XYZ[:,2])-10, np.max(XYZ[:,2])+10)
ax.set_xlim(xlim)
ax.set_ylim(ylim)
ax.set_zlim(zlim)
ax.grid(False)

timestamp_str = np.array(Tmp_npspike['Timestamp'], dtype=str)
scatter_frame = ax.scatter3D([],[],[], c='k')
weldstat = 'Weld off'
title = ax.set_title('Print Head Position: '+ weldstat)

ax.w_xaxis.set_pane_color((0.5,.5,.5,1))
ax.w_yaxis.set_pane_color((0.5,.5,.5,.9))
ax.w_zaxis.set_pane_color((0.5,.5,.5,.8))

ax.xaxis.set_major_locator(ticker.MaxNLocator(4))
ax.yaxis.set_major_locator(ticker.MaxNLocator(4))
ax.zaxis.set_major_locator(ticker.MaxNLocator(4))

def drawframe(i):
    scatter_frame._offsets3d = (XYZ[i,0:1], XYZ[i,1:2], XYZ[i,2:])
    title.set_text('Print Head Position\n' + str(timestamp_str[i]))
    if Tmp_npspike['Weld On'][i] == 0:
        weldstat = 'Weld off'
    else:
        weldstat = 'Weld on'
    if i > 1:
        if (Tmp_npspike['Weld On'][i] == 0) and (Tmp_npspike['Weld On'][i-1] == 1):
            ax.w_xaxis.set_pane_color((0.5,.5,.5,1))
            ax.w_yaxis.set_pane_color((0.5,.5,.5,.9))
            ax.w_zaxis.set_pane_color((0.5,.5,.5,.8))

        if (Tmp_npspike['Weld On'][i] == 1) and (Tmp_npspike['Weld On'][i-1] == 0):
            ax.w_xaxis.set_pane_color((.8,.8,.8,1))
            ax.w_yaxis.set_pane_color((.8,.8,.8,.9))
            ax.w_zaxis.set_pane_color((.8,.8,.8,.8))

    title.set_text('Print Head Position: ' + weldstat + '\n' + str(timestamp_str[i]))

    return(scatter_frame, title)

anim = animation.FuncAnimation(fig, drawframe, XYZ.shape[0], repeat=False, interval=100)#XYZ.shape[0])
HTML(anim.to_html5_video())


```
![](README/Print_Head_Pos.mp4)
