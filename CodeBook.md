
CodeBook
==============

Data can be downloaded by url *https://d396qusza40orc.cloudfront.net/getdata%2Fprojectfiles%2FUCI%20HAR%20Dataset.zip*. 

1. Merges the training and the test sets to create one data set.
2. Extracts only the measurements on the mean and standard deviation for each measurement.
3. Uses descriptive activity names to name the activities in the data set.
4. Appropriately labels the data set with descriptive activity names. 
5. Creates a second, independent tidy data set with the average of each variable for each activity and each subject.

To create complete train and test data, several files were merged together. These data files included:

	Training data set - 'train/X_train.txt'
	Test data set - 'test/X_test.txt'
	Training labels - 'train/y_train.txt'
	Test labels - 'test/y_test.txt'
 
	Two files with row identifies the subject who performed the activity for each window sample in range from 1 to 30. 
	- 'train/subject_train.txt'
	- 'test/subject_test.txt'

1. Activity: factor with 6 levels, in order: WALKING, WALKING_UPSTAIRS, WALKING_DOWNSTAIRS, SITTING, STANDING, LAYING,
             indicated the activity being performed at the moment of data gathering,

2. SubjectID: numeric value from 1 to 30 indicating the subject Id.

* For variables 3 to 68 the variable is numeric and the name indicates:

    * Acc and Gyro: data origin, accelerometer and gyroscope, respectively.
    * -XYZ: the three dimensional axis, X,Y, or Z, respectively (3-axial)
    * Body and Gravity: Acceleration signal source, Body or Gravity,
                        determined using low pass Butter worth filter with a corner frequency of 0.3 Hz. 
    * Mean and Std: Mean value or Standard deviation, respectively.
    * t of f: t denotes time domain signals, these were captured at a constant rate of 50 Hz.
                Then they were filtered using a median filter and a 3rd order low pass Butter worth filter
                with a corner frequency of 20 Hz to remove noise. On the other hand, f denotes the use of a
                Fast Fourier Transform (FFT) was applied.

out of command "names(tidy_data)"
 [1] "Activity"                 "SubjectID"                "tBodyAccMeanX"            "tBodyAccMeanY"            "tBodyAccMeanZ"            "tBodyAccStdX"            
 [7] "tBodyAccStdY"             "tBodyAccStdZ"             "tGravityAccMeanX"         "tGravityAccMeanY"         "tGravityAccMeanZ"         "tGravityAccStdX"         
[13] "tGravityAccStdY"          "tGravityAccStdZ"          "tBodyAccJerkMeanX"        "tBodyAccJerkMeanY"        "tBodyAccJerkMeanZ"        "tBodyAccJerkStdX"        
[19] "tBodyAccJerkStdY"         "tBodyAccJerkStdZ"         "tBodyGyroMeanX"           "tBodyGyroMeanY"           "tBodyGyroMeanZ"           "tBodyGyroStdX"           
[25] "tBodyGyroStdY"            "tBodyGyroStdZ"            "tBodyGyroJerkMeanX"       "tBodyGyroJerkMeanY"       "tBodyGyroJerkMeanZ"       "tBodyGyroJerkStdX"       
[31] "tBodyGyroJerkStdY"        "tBodyGyroJerkStdZ"        "tBodyAccMagMean"          "tBodyAccMagStd"           "tGravityAccMagMean"       "tGravityAccMagStd"       
[37] "tBodyAccJerkMagMean"      "tBodyAccJerkMagStd"       "tBodyGyroMagMean"         "tBodyGyroMagStd"          "tBodyGyroJerkMagMean"     "tBodyGyroJerkMagStd"     
[43] "fBodyAccMeanX"            "fBodyAccMeanY"            "fBodyAccMeanZ"            "fBodyAccStdX"             "fBodyAccStdY"             "fBodyAccStdZ"            
[49] "fBodyAccJerkMeanX"        "fBodyAccJerkMeanY"        "fBodyAccJerkMeanZ"        "fBodyAccJerkStdX"         "fBodyAccJerkStdY"         "fBodyAccJerkStdZ"        
[55] "fBodyGyroMeanX"           "fBodyGyroMeanY"           "fBodyGyroMeanZ"           "fBodyGyroStdX"            "fBodyGyroStdY"            "fBodyGyroStdZ"           
[61] "fBodyAccMagMean"          "fBodyAccMagStd"           "fBodyBodyAccJerkMagMean"  "fBodyBodyAccJerkMagStd"   "fBodyBodyGyroMagMean"     "fBodyBodyGyroMagStd"     
[67] "fBodyBodyGyroJerkMagMean" "fBodyBodyGyroJerkMagStd" 