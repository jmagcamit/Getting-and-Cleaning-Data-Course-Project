# CODEBOOK

Describes the variables, the data, and any transformations or work performed to clean up the data.

## Loading data set from .txt files to different data frames.   
  
* **activity** = activity_labels.txt: *Links the class labels with* their activity name.  
* **features** = features.txt: *List of all features*  
* **subj_train** = /train/subject_train.txt: *Subject who performed the activity for each window sample. Range is from 1 to 30.*  
* **x_train** = /train/X_train.txt: *Training set*  
* **y_train** = /train/y_train.txt: *Training labels*  
* **subj_test** = /test/subject_test.txt: *Subject who performed the activity for testing. Range is from 2 to 24* 
* **x_test** = /test/X_test.txt: *Test set*  
* **y_test** = /test/y_test.txt: *Test labels*  

## Set column names of data frames
**The features data frame contains the name of variables measured. The features data frame has 561 rows which is equal to number of columns of x test/train data frame.**  
column names of x_test and x_train were set to features[,2]  

**Both y_train and y_test are training and testing labels. It ranges from 1-6, which corresponds to the activity performed in activity data frame.**  
column names for y_train and y_test were set to "activity id". Each activityID(1-6) corresponds to an activity in the activity data frame.  
  
  
## Combining data frames
**The training data are merged into a new data frame (train_data), testing data are merged into a new data frame(test_data), both are combined to form a single data frame (new_data).**  
  
* train_data contains the training data frames (subj_train, x_train, y_train)  
* test_data contains the testing data frames (subj_test, x_test, y_test)  
* new_data is training and testing data frames merged  

**The new dataset is further reduced to mean and std measurements only**  
  
*mean_std* returns logical values (0 or 1) if a column name of new_data frame(cNames) contains "mean", or "std", using regex metacharacters. It also returns the columns with activityID, and subj_id. It is then used to index *new_data* where *mean_std == TRUE*. The resulting data frame is stored in reduced_data, merged by its "activityID".  

## Use descriptive names in the reduced data set

**The activityID in reduced_data is replaced by activityName. The column names of reduced data were modified for better readability, the following changes were made:**  
  
* "**^t**" to "time"  
* "**^f**" to "frequency"  
* "**Acc**" to "Accelerometer"  
* "**Gyro**" to "Gyroscope"  
* "**Mag**" to "Magnitude"  

## Create an independent tidy set with average of each variable for each activity and subject  

reduced_data is grouped by activityID then subj_id. It was then arranged according to subj_id and the mean of each variable for every group was computed and stored in a new data frame called tidyData. The tidyData is exported to a text file called **tidyData.txt** with 180 observations of 82 variables, creating an independent tidy set.  
