setwd("F:/data science/Hackathon2")

#reading the files

train=read.csv("train.csv")
test=read.csv("test.csv")

str(train)
str(test)

test$shares=0

#dropping the categorial variables
drops <- c("Day_of_publishing","Category_article")
train=train[,!(names(train) %in% drops)]
test=test[,!(names(test) %in% drops)]

#fitting a linear regression model
fit<-lm(shares~.,data=train)

#predicting for the test dataset
pred= predict(fit,test)
test$shares=pred

#creating a submission file
submit<-data.frame(id=test$id,predictions=test$shares)
write.csv(submit,file="submit1.csv",row.names=FALSE)



