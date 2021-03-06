# File Return Folder
## Submission Instructions
Please fill out the files in this folder for final submission.
Submissions must be returned in a .zip folder titled \<principal contact last name\>_srpam_challenge.zip".
This should be sent to nycza@ornl.gov with the subject line "SRP AM Challenge."
Any questions or concerns for challenge submission can be raised in the [discussions](https://github.com/SRP-AM/SRP_AM_Prediction_Challenge/discussions) tab, or emailed to nycza@ornl.gov.

## Challenge Return Files
The following challenge return files are *required* for final evaluation.
Files must be returned in the following format for evaluation and inclusion in the final challenge results.

#### Participant Questionaire
Please provide your answers to the questions about basic methodology. The Participant Questionaire has been included in both Word and LaTeX file formats for ease of completion.
Either format may be filled and submitted.

#### CHAL-4_TempRemoved_nodate_nospikeTemperature&SysData.xlsx
This file contains the timestamp, ambient temperature (at Thermocouple 12), weld voltage, weld current, on/off state, and XYZ position of the print head.
The predicted temperature histories for each of the 11 thermocouple locations should be filled out in columns 2-12 and returned.

#### DeformationMapsChallDataRemoved.xlsx
Column 1, titled X (distance from left end) gives the locations along the x axis at which the deformation should be reported.
Predicted values for the challenge deformation should be reported in Column 2, "Deformation".

#### Residual Stress _challenge sample_template.xlsx
The Residual Stress challenge file return format varies from the residual stress calibration data file.
There are two tabs for the residual stress challenge data:
1. **Mid Plane (Y=0)**
2. **Side Plane (Y=125)**

For each of these Y planes, residual stress values should reported along seven lines:
  1. **Col 1-4:** $X = 0, Z \in [-12.7, 10]$
  2. **Col 5-9:** $X = 10, Z \in [-12.7, 10]$
  3. **Col 10-14:** $X = 20, Z \in [-12.7, 10]$
  4. **Col 15-19:** $Z = 7, X \in [-24, 24]$
  5. **Col 20-24:** $Z = 1, X \in [-24, 24]$
  6. **Col 25-29:** $Z = -2, X \in [-24, 24]$
  7. **Col 30-34:** $Z = -12, X \in [-24, 24]$

These locations are visualized in Figure 3.4 of the [Challenge Information Packet](https://github.com/SRP-AM/SRP_AM_Prediction_Challenge/blob/main/challenge_info_packet.pdf).
Note that the resolution for the residual stress predictions is left to the participant, and should be reported as locations in the first column of each reporting segment.

#### Temperature_Challenge_Sample_Model_Locations.xlsx
Section 3.2.1  of the [Challenge Information Packet](https://github.com/SRP-AM/SRP_AM_Prediction_Challenge/blob/main/challenge_info_packet.pdf) describes the optional temperature history reporting for the challenge problem.
Additional location points through the center of the weld pass are provided in rows 4-6, and temperature predictions should be reported for these additional 27 points in one second intervals.
This problem is optional, since the true temperature results were recorded only at the thermocouples.
However, center of the pass predictive behavior is important for cross model comparison, so this exercise is *highly encouraged.*

## Optional Calibration Return Files
The following calibration return files are *optional but encouraged* for final evaluation.

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
