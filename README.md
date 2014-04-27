
Description for run_analysis.R
============================

This script is developed for the peer assignment for the Coursera class : *Getting and Cleaning Data Project*
The data for this script was obtained from *https://d396qusza40orc.cloudfront.net/getdata%2Fprojectfiles%2FUCI%20HAR%20Dataset.zip*

This R script does the following:
    1. Merges the training and the test sets to create one data set.
    2. Extracts only the measurements on the mean and standard deviation for each measurement. 
    3. Uses descriptive activity names to name the activities in the data set
    4. Appropriately labels the data set with descriptive activity names. 
    5. Creates a second, independent tidy data set with the average of each variable for each activity and each subject.  


The reshape2 package is required for melt and dcast functions, which are used later in the script, the package is loaded.
Note that to reproduce this process the reshape2 package must be installed.

Download zip file from url: https://d396qusza40orc.cloudfront.net/getdata%2Fprojectfiles%2FUCI%20HAR%20Dataset.zip
Unzip getdata_projectfiles_UCI HAR Dataset.zip file in R working directory


1. Reading data from files
```
# Reading subjects
subject_test <- read.table("test/subject_test.txt", header=FALSE, col.names=c("SubjectID"))
subject_train <- read.table("train/subject_train.txt", header=FALSE, col.names=c("SubjectID"))

# Reading labels
y_test <- read.table("test/y_test.txt", header=FALSE, col.names=c("Activity"))
y_train <- read.table("train/y_train.txt", header=FALSE, col.names=c("Activity"))

# Reading features
features <- read.table("features.txt", header=FALSE, as.is=TRUE, col.names=c("FeatireID", "FeatireName"))

# Reading data set
X_test <- read.table("test/X_test.txt", header=FALSE, sep="", col.names=features$FeatireName)
X_train <- read.table("train/X_train.txt", header=FALSE, sep="", col.names=features$FeatireName)
```

2. Extracts only the measurements on the mean and standard deviation for each measurement. Merge
```
# Getting indexes of measurement names with std() and mean()
mean_std_index <- grep(".*mean\\(\\)|.*std\\(\\)", features$FeatireName)
# Getting data by indexes
X_test <- X_test[, mean_std_index]
X_train <- X_train[, mean_std_index]


# Setting subjects  and labels to data set
X_test$SubjectID <- subject_test$SubjectID
X_train$SubjectID <- subject_train$SubjectID

X_test$Activity <- y_test$Activity
X_train$Activity <- y_train$Activity

# Merging data
X_data <- rbind(X_test, X_train)
column_names <- colnames(X_data)
column_names <- gsub("\\.+mean\\.+", column_names, replacement="Mean")
column_names <- gsub("\\.+std\\.+", column_names, replacement="Std")
colnames(X_data) <- column_names
```

3. Uses descriptive activity names to name the activities in the data set
```
activity_labels <- read.table("activity_labels.txt", header=F, col.names=c("Activity", "ActivityName"))
activity_labels$ActivityName <- as.factor(activity_labels$ActivityName)
```

4. Appropriately labels the data set with descriptive activity names
```
X_data$Activity <- factor(X_data$Activity, levels = 1:6, labels = activity_labels$ActivityName)
```

5. Creates a second, independent tidy data set with the average of each variable for each activity and each subject
```
melt_data <- melt(X_data, id.vars = c("Activity", "SubjectID"))
tidy_data <- dcast(melt_data, Activity + SubjectID ~ variable, mean)
    
# Save tidy data set
write.table(tidy_data, "tidy_data.txt", row.names = FALSE)
```
