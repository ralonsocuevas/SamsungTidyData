#Getting and Cleaning Data Course Project

##Description of the work

run_analysis.R: The script that does the transformation
COdeBook.md: Contains the variables names and experiment explanation
Readme.md: Description of the work

###Explanation of the R code:

#1. First of all we merge the datasets and put the features names in the columns
testpath<-file.path(getwd(),"test")
trainpath<-file.path(getwd(),"train")


subject_test<- read.table(file.path(testpath,"subject_test.txt"))
x_test<- read.table(file.path(testpath,"X_test.txt"))
y_test<- read.table(file.path(testpath,"y_test.txt"))

subject_train<- read.table(file.path(trainpath,"subject_train.txt"))
x_train<- read.table(file.path(trainpath,"X_train.txt"))
y_train<- read.table(file.path(trainpath,"y_train.txt"))

x<-rbind(x_test,x_train)
y<-rbind(y_test,y_train)
subject<-rbind(subject_test,subject_train)

data<-cbind(subject,y,x)

features <- read.csv(file.path(getwd(),'features.txt'), header = FALSE, sep = ' ')
features2 <- as.character(features[,2])
names(data)<-c(c('Subject','Activity'),features2)

#2. Extract only the columns that contains mean or std in the header, also
# the subject and the activity id
mean_std <- data[,grepl("mean\\(\\)|std\\(\\)|Subject|Activity", names(data))]

#3. Change the activities id's by the names
activities <- read.csv(file.path(getwd(),'activity_labels.txt'), header = FALSE, sep = ' ')
names(activities)<-c('Activity','Activity_Name')
data_act_names<-merge(data,activities,by.x = 'Activity',by.y='Activity',all=TRUE)
data_act_names<-data_act_names[,c('Subject','Activity_Name',features2)]

#4. Change the name of the variables with the information of the features_info file
features_fix<-features2
features_fix<-gsub("[(][)]","",features_fix)
features_fix<-gsub("^t","Time_",features_fix)
features_fix<-gsub("^f","Frequency_",features_fix)
features_fix<-gsub("Acc","Accelerometer",features_fix)
features_fix<-gsub("Gyro","Gyroscope",features_fix)
features_fix<-gsub("Mag","Magnitude",features_fix)
features_fix<-gsub("-mean-","_Mean_",features_fix)
features_fix<-gsub("-std-","_StandardDeviation_",features_fix)
features_fix<-gsub("-","_",features_fix)

names(data_act_names)<-c('Subject','Activity_Name',features_fix)

#5. Create an independent dataset with the average of each variable for each activity and subject
dataMeansGroupedBy <- aggregate(data_act_names[,3:563], by= list(Activity_Name= data_act_names$Activity_Name, Subject = data_act_names$Subject),FUN = mean)
write.table(dataMeansGroupedBy,"tidy_dataset.txt",row.names = FALSE)

