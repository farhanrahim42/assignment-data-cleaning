# assignment-data-cleaning
## Review criterialess 
The submitted data set is tidy.
The Github repo contains the required scripts.
GitHub contains a code book that modifies and updates the available codebooks with the data to indicate all the variables and summaries calculated, along with units, and any other relevant information.
The README that explains the analysis files is clear and understandable.
## Instructions
One of the most exciting areas in all of data science right now is wearable computing - see for example this article . Companies like Fitbit, Nike, and Jawbone Up are racing to develop the most advanced algorithms to attract new users. The data linked to from the course website represent data collected from the accelerometers from the Samsung Galaxy S smartphone. A full description is available at the site where the data was obtained:

http://archive.ics.uci.edu/ml/datasets/Human+Activity+Recognition+Using+Smartphones

Here are the data for the project:

https://d396qusza40orc.cloudfront.net/getdata%2Fprojectfiles%2FUCI%20HAR%20Dataset.zip

## Explanation
1. Merges the training and the test sets to create one data set.
   ### trainData <- cbind(train.subject, train.y, train.x)
   ### testData <- cbind(test.subject, test.y, test.x)
   ### fullData <- rbind(trainData, testData)

2. Extracts only the measurements on the mean and standard deviation for each measurement.
   ### featureIndex <- grep(("mean\\(\\)|std\\(\\)"), featureName)
   ### finalData <- fullData[, c(1, 2, featureIndex+2)]
   ### colnames(finalData) <- c("subject", "activity", featureName[featureIndex])

3. Uses descriptive activity names to name the activities in the data set
   ### activityName <- read.table("./data/UCI HAR Dataset/activity_labels.txt")
   ### finalData$activity <- factor(finalData$activity, levels = activityName[,1], labels = activityName[,2]) 

4. Appropriately labels the data set with descriptive variable names.
   ### names(finalData) <- gsub("\\()", "", names(finalData))
   ### names(finalData) <- gsub("^t", "time", names(finalData))
   ### names(finalData) <- gsub("^f", "frequence", names(finalData))
   ### names(finalData) <- gsub("-mean", "Mean", names(finalData))
   ### names(finalData) <- gsub("-std", "Std", names(finalData))

5. From the data set in step 4, creates a second, independent tidy data set with the average of each variable for each activity and  each subject.

  ### library(dplyr)
  ### groupData <- finalData %>%
   ### group_by(subject, activity) %>%
   ### summarise_each(funs(mean))

  ### write.table(groupData, "./data/MeanData.txt", row.names = FALSE)


