    pregnant         glucose         pressure         triceps         insulin           mass          pedigree           age        diabetes 
 Min.   : 0.000   Min.   :  0.0   Min.   :  0.00   Min.   : 0.00   Min.   :  0.0   Min.   : 0.00   Min.   :0.0780   Min.   :21.00   neg:500  
 1st Qu.: 1.000   1st Qu.: 99.0   1st Qu.: 62.00   1st Qu.: 0.00   1st Qu.:  0.0   1st Qu.:27.30   1st Qu.:0.2437   1st Qu.:24.00   pos:268  
 Median : 3.000   Median :117.0   Median : 72.00   Median :23.00   Median : 30.5   Median :32.00   Median :0.3725   Median :29.00            
 Mean   : 3.845   Mean   :120.9   Mean   : 69.11   Mean   :20.54   Mean   : 79.8   Mean   :31.99   Mean   :0.4719   Mean   :33.24            
 3rd Qu.: 6.000   3rd Qu.:140.2   3rd Qu.: 80.00   3rd Qu.:32.00   3rd Qu.:127.2   3rd Qu.:36.60   3rd Qu.:0.6262   3rd Qu.:41.00            
 Max.   :17.000   Max.   :199.0   Max.   :122.00   Max.   :99.00   Max.   :846.0   Max.   :67.10   Max.   :2.4200   Max.   :81.00            



p1 <- ggplot(diabetes, aes(x=pregnant)) + ggtitle("Number of times pregnant") +
  geom_histogram(aes(y = 100*(..count..)/sum(..count..)), binwidth = 1, colour="black", fill="white") + ylab("Percentage")
p2 <- ggplot(diabetes, aes(x=glucose)) + ggtitle("Glucose") +
  geom_histogram(aes(y = 100*(..count..)/sum(..count..)), binwidth = 5, colour="black", fill="white") + ylab("Percentage")
p3 <- ggplot(diabetes, aes(x=pressure)) + ggtitle("Blood Pressure") +
  geom_histogram(aes(y = 100*(..count..)/sum(..count..)), binwidth = 2, colour="black", fill="white") + ylab("Percentage")
p4 <- ggplot(diabetes, aes(x=triceps)) + ggtitle("Triceps") +
  geom_histogram(aes(y = 100*(..count..)/sum(..count..)), binwidth = 2, colour="black", fill="white") + ylab("Percentage")
p5 <- ggplot(diabetes, aes(x=insulin)) + ggtitle("Insulin") +
  geom_histogram(aes(y = 100*(..count..)/sum(..count..)), binwidth = 20, colour="black", fill="white") + ylab("Percentage")
p6 <- ggplot(diabetes, aes(x=mass)) + ggtitle("Body Mass Index") +
  geom_histogram(aes(y = 100*(..count..)/sum(..count..)), binwidth = 1, colour="black", fill="white") + ylab("Percentage")
p7 <- ggplot(diabetes, aes(x=pedigree)) + ggtitle("Diabetes Pedigree Function") +
  geom_histogram(aes(y = 100*(..count..)/sum(..count..)), colour="black", fill="white") + ylab("Percentage")
p8 <- ggplot(diabetes, aes(x=age)) + ggtitle("Age") +
  geom_histogram(aes(y = 100*(..count..)/sum(..count..)), binwidth=1, colour="black", fill="white") + ylab("Percentage")
grid.arrange(p1, p2, p3, p4, p5, p6, p7, p8, ncol=2)


attach(diabetes)
par(mfrow=c(2,4))
boxplot(pregnant~diabetes, main="No. of Pregnancies vs. Diabetes", 
        xlab="diabetes", ylab="Pregnancies")
boxplot(glucose~diabetes, main="Glucose vs. Diabetes", 
        xlab="diabetes", ylab="Glucose")
boxplot(pressure~diabetes, main="Blood Pressure vs. Diabetes", 
        xlab="diabetes", ylab="Blood Pressure")
boxplot(triceps~diabetes, main="Skin Thickness vs. Diabetes", 
        xlab="diabetes", ylab="Skin Thickness")
boxplot(insulin~diabetes, main="Insulin vs. Diabetes", 
        xlab="diabetes", ylab="Insulin")
boxplot(mass~diabetes, main="BMI vs. Diabetes", 
        xlab="diabetes", ylab="BMI")
boxplot(pedigree~diabetes, main="Diabetes Pedigree Function vs. Diabetes", xlab="diabetes", ylab="DiabetesPedigreeFunction")
boxplot(age~diabetes, main="Age vs. Diabetes", 
        xlab="diabetes", ylab="Age")



for salary one. 
What is logistic regression and how to use it 
use of anova
meaning of test = CHisq in anova

