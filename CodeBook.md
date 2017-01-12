# Code Book
This file contains the summary of the data worked with and the transformations performed and how they interact

##Tranformations

In this project we perform the following five tranformations to the data: 
1. Merge the datasets and put the features names in the columns 
2. Extract only the columns that contains mean or std in the header, also the subject and the activity id 
3. Change the activities id's by the names 
4. Change the name of the variables with the information of the features_info file 
5. Create an independent dataset with the average of each variable for each activity and subject

To run this transformations you need to execute the run_analysis.R script.

##Variables
data: the raw data combined
features2: Names of the variables of the raw data
data_act_names: The merged data with the names of the activities
x: The x data merged
y: The y data merged
subject: The subject data merged


##Raw data
The experiments have been carried out with a group of 30 volunteers within an age bracket of 19-48 years. 
Each person performed six activities (WALKING, WALKING_UPSTAIRS, WALKING_DOWNSTAIRS, SITTING, STANDING, LAYING) wearing a smartphone 
(Samsung Galaxy S II) on the waist. Using its embedded accelerometer and gyroscope, we captured 3-axial linear acceleration and 3-axial 
angular velocity at a constant rate of 50Hz. The experiments have been video-recorded to label the data manually.
The obtained dataset has been randomly partitioned into two sets, where 70% of the volunteers was selected for generating the 
training data and 30% the test data. 

The sensor signals (accelerometer and gyroscope) were pre-processed by applying noise filters and then sampled in fixed-width sliding 
windows of 2.56 sec and 50% overlap (128 readings/window). The sensor acceleration signal, which has gravitational and body motion 
components, was separated using a Butterworth low-pass filter into body acceleration and gravity. The gravitational force is assumed 
to have only low frequency components, therefore a filter with 0.3 Hz cutoff frequency was used. From each window, a vector of features 
was obtained by calculating variables from the time and frequency domain.

####For each record it is provided:
======================================

- Triaxial acceleration from the accelerometer (total acceleration) and the estimated body acceleration.
- Triaxial Angular velocity from the gyroscope. 
- A 561-feature vector with time and frequency domain variables. 
- Its activity label. 
- An identifier of the subject who carried out the experiment.

