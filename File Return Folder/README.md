## Challenge Return Files
The following challenge return files are required for final evaluation.
Please return in the given format.  

#### CHAL-4_TempRemoved_nodate_nospikeTemperature&SysData.xlsx
This file contains the timestamp, ambient temperature (at Thermocouple 12), weld coltage, weld current, on/off state, and XYZ position of the print head.
The predicted temperatures over time for each of the 11 thermocouple locations should be filled out in columns 2-12 and returned.

#### DeformationMapsChallDataRemoved.xlsx

#### Residual Stress _challenge sample_template.xlsx

#### Temperature_Challenge_Sample_Model_Locations.xlsx


## Optional Calibration Return Files
The following calibration return files are optionally included to demonstrate model performance on the calibration data.

#### DeformationMapsCal.xlsx
Calibration deformation predictions should be appended to the original calibration deformation file, as the third column (called "Predictions" here).

#### Residual Stress _calibration sample_empty.xlsx
This file is identical to the [original residual stress calibration file](https://github.com/SRP-AM/SRP_AM_Prediction_Challenge/blob/main/ResidualStress/CalTask/Residual%20Stress%20_calibration%20sample.xlsx), with all residual stress measurements removed.
Predicted stresses for the calibration problem should be returned in the appropriate columns.

#### SRP-4_nospike_Temperature&SysData_empty.xlsx
This file is identical to the [original temperature calibration file](https://github.com/SRP-AM/SRP_AM_Prediction_Challenge/blob/main/Temperature/CalTask/SRP-4_nospike_Temperature%26SysData.xlsx), with data for thermocouples 1-11 removed.
Columns 2-12 should be filled out with the calibration predictions.

#### Temperature_Calibration_Sample_Model_Locations.xlsx
As explained in section 2.3.1 of the [challenge information packet](https://github.com/SRP-AM/SRP_AM_Prediction_Challenge/blob/main/challenge_info_packet.pdf), challenge participants can also return predicted temperature history corresponding to the center of the weld passes.
These 27 reporting locations are specified in rows 4-6 of [the file](https://github.com/SRP-AM/SRP_AM_Prediction_Challenge/blob/main/File%20Return%20Folder/Optional%20Calibration%20Return%20Files/Temperature_Calibration_Sample_Model_Locations.xlsx).
Although the actual temperatures at these points are unknown for the challenge problem, cross prediction comparison at the center locations is important for cross model comparison.
