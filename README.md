This file contains a detailed description of the R-script 'run_analysis.R' used in the project.
The script 'run_analysis.R' can be run as long as the Samsung data are in the working directory.
'run_analysis.R' calls another R-script 'create_data_set.R' which creates the table on which the analysis will be performed.


==============================================================================
Description of 'run_analysis.R':
==============================================================================


The script calls another script, 'create_data_set.R', which builds the data set which will be used for the analysis. 

The package 'dplyr' is loaded in order to use the functions 'group_by' and 'summarize_each'.

Using the pipe operator %<% which chains a series of operations, we first group the values by activity and subject and then we apply the mean to each column (i.e. to each variable).

The resulting data set is written in a .txt file formatted as table which can be easily read with read.table.
The option row.names = FALSE is used to prevent that the row names are to be written along with the table.


==============================================================================
Description of 'create_data_set.R':
==============================================================================
This script is run in 'run_analysis.R' to generate the data set.

All the files which will be merged together are loaded with 'read.table'.
The option stringsAsFactors = FALSE is very important. This prevent that strings are treated as factors. Strings interpreted as factors can create several problems.
(This will be crucial later when reading 'features.txt' which contains the activity names as strings).

(We add to the traning and test set a column containg the activity labels (with value ranging from 1 to 6) and the subject label (with value raning from 1 to 30). 
The function 'cbind' combine the three tables by columns.

The two tables obtained at previous step are combined together by rows using 'rbind'.

We build a vector containing the indexes of the features that we want to extract.
A vector of features labels is build starting from the list of features in 'features.txt' loaded.
Features containing the word mean() and std() are selected with the function 'grep' which returns an array with the indexes of the vector whose element contains the specific pattern (first argument in 'grep').  
All the indexes are put together and sorted with increasing index (just to keep the original order). 
The index of the activity and subject columns are added.

Using the index vector the measurements on the mean and standard deviation can be extracted.

Here the activity label expressed as a number are replaced with the name of the activities.
The for loop iterates over all the observations of activity and performs the replacement.

Finally a header with the correct feature labels is build taking care of adding also labels to column with the activity labels and the subjects. 

