===========================
BRIEF PROJECT DESCRIPTION
===========================
For this project data collected from the accelerometers from the Samsung Galaxy S smartphone by 30 different partecipants were used as described in features_info.txt. 

Data were dowloaded from https://d396qusza40orc.cloudfront.net/getdata%2Fprojectfiles%2FUCI%20HAR%20Dataset.zip 

The goal of the project is to prepare tidy data that can be used for later analysis.
For the purpose a R script called 'run_analysis.R' has been created that does the following:
 
(1) Merges the training and the test sets to create one data set.

(2) Extracts only the measurements on the mean and standard deviation for each measurement. 

(3) Uses descriptive activity names to name the activities in the data set.

(4) Appropriately labels the data set with descriptive variable names.
 
(5) From the data set in step 4, creates a second, independent tidy data set with the average of each variable for each activity and each subject.


============================
CREATING THE TIDY DATA FILE
============================
The data used to create the tidy data file are contained in the files:

- 'X_train.txt': Training set (7352 observations for 561 features). 

- 'y_train.txt': Training (activity) labels (with 7352 observations).

- 'X_test.txt': Test set (2947 observations for 561 features).

- 'y_test.txt': Test (activity) labels (with 2947 observations).

plus the following files which contains information about the features, the activities and the subjects:

- 'features.txt': List of all the 561 features.

- 'activity_labels.txt': Links the 6 class labels with their activity name.

- 'subject_train.txt' and 'subject_test': Each row identifies the subject who performed the activity for each window sample. Its range is from 1 to 30.
					  There are 7352 observations in 'subject_train.txt' and 2947 observations in 'subject_test'
					  



The files 'X_train.txt','y_train.txt','X_test.txt','y_test.txt','subject_train.txt' and 'subject_test.txt' are initially loaded into R using read.table and assigned respectively to the following variables (dim indicates the dimension of the table):

X_train 	--> dim: 7352	561 
y_train 	--> dim: 7352	  1
X_test  	--> dim: 2947	561
y_test		--> dim: 2947	  1
subject_train 	--> dim: 7352 	  1
subject_test	--> dim: 2947 	  1

'X_train','y_train' and 'subject_train' where merged into one 7352 * 563 table named X_train_all.
'X_test','y_test' and 'subject_test' where merged into one 2947 * 563 named X_train_all.
These last one was appended to the previous one in order to obtain one table with 10299 observations of 563 variables and it was named X_all.
(completed step (1))

Afterwards we selected only the set of variables that were estimated by performing mean and standard deviation from the signals taken from the accelerometers (i.e. the features containing mean() and std() in the label). These selected variables are 66. The list of the selected variables is contained in 'ftrs_slct.txt'.

From now on we worked on such a table obtained by subsetting 'X_all'.
This new table was named 'X_slct' and it shows 10299 observations of 68 variables (having included also columns for activity and subject).
(completed step (2))

At this point we replaced the activity label expressed as a number (ranging from 1 to 6) with the name of the activities (WALKING, WALKING_UPSTAIRS, WALKING_DOWNSTAIRS, SITTING, STANDING, LAYING).
(completed step(3))

A header was created for table 'X_slct' extracting the selected feature labels from the initial feature list and adding the labels for the activity and the subject. (completed step (4))
 
Finally, a data set containing the average value of each variable for each activity and each subject was created based on the data set at step 4. 
This data set called 'grpd_avrg is represented as 180 * 68 table. (completed step (5))


=============================
CONTENT OF THE FOLDER
=============================
The current folder contains the following files:

'run_analysis.R.txt' containing the R-code performing the analysis
'create_data_set_R.txt' containing the R-code which create the data set on which the analysis is performed

'README.md' describing how the R-scripts work together
'CodeBood.md' containing a brief description of the project and of the data used in the analysis. 

'averages_data.txt' containing the data set obtained at step (5)
'ftrs_slct.txt' containing the list of selected features

Additional files provided together with the raw data giving more information on the variables and the raw data.
'README_orig.txt'
'features_info.txt'
'features.txt'
'activity_labels.txt'

=============================
ADDITIONAL INFORMATION
=============================
Additional information on the raw data can be found in README_orig.txt and features_info.txt or on the website:
http://archive.ics.uci.edu/ml/datasets/Human+Activity+Recognition+Using+Smartphones.

Additional information on the script 'run_analysis.R', performing the data manipulation, can be found in 'README.md'.  

