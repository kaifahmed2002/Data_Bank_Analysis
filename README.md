# Medical Data Analysis

## About the Project

In this case study, I will perform data analysis for a Fictional healthcare organization Medicare, As a Junior Data Analyst in the Medicare Solutions project, my role is crucial in supporting the analysis of the personal medical data of 1,338 patients.The primary objective of the analysis is to gain insights into the factors influencing the cost of medical care. By analyzing variables such as age, gender, region, and other relevant factors, Medicare Solutions aims to identify patterns and understand the effects of these variables on the cost of medical services.  I  


## ERD 

![Medical Data ERD](https://user-images.githubusercontent.com/112409778/228036499-add02f0a-54b8-4a90-90f9-47e71c843ef0.png)

## Variables

There are a variety of variables that will impact the outcome of this analysis:

- Age: age of primary beneficiary
  
- Sex: insurance contractor gender,
  - Male 
  - Female
- Body Mass Index (BMI): Weight to height body mass ratio
  - Underweight: Below 18.5
  - Normal: 18.5 - 24.9
  - Overweight: 25.0 – 29.9
  - Obese: Greater Than or equal to 30.0 
- Children: Number of dependents
- Smoker: Smoking
- Region: Region of domicile of the patient in the United States.
  - Northeast 
  - Southeast 
  - Northwest
- Charges: Individual medical costs billed by health insurance for services provided


## Objective

The objective of the analysis is to analyze the effects of variables on the cost of medical care. The analysis seeks to answer the following questions:

1. Which region has the lowest cost of medical care?
2. Which gender has the highest typical medical charges?
3. Is there correlation between the number of dependents a patient has and medical charges?
4. Is there correlation between age and medical charges?
5. Do individuals with higher BMI have higher medical charges?
6. What is the relationship between smoking and medical charges?


## Analysis

1. What region has the lowest cost of medical care?

![Q1 P1](https://github.com/kaifahmed2002/Medical_Data_Analysis/assets/92524691/31d4fab9-4080-461c-94fa-f4fea0c27c62)

The overall average of charges in the dataset is $13,463.17. However, there is an uneven distribution of charges in the dataset. As indicated in the histogram above there is a right skew that is affecting the average. The median charge, $9,421.96, is a better indication of the amount of a typical medical charge. 


![Q1 P2](https://github.com/kaifahmed2002/Medical_Data_Analysis/assets/92524691/5c02d5f0-0497-4a09-862c-afe1fae5b94d)

Northeast have the Highest median medical charges of $10,058 and on the other hand, Southeast have the Lowest median medical charges of $8,871.


2. Which  gender has the highest highest typical charges?

The distribution of the charges of both male and females have a right skew in which outliers are impacting the calculation of the average charges.

![Q2P1 (1)](https://github.com/kaifahmed2002/Medical_Data_Analysis/assets/92524691/78519fb6-30fb-4567-aef8-b27445d79d76)

Average medical charges of Male's is Greater then Female's.

Female - $12,945, 

Male - $13,969.


![Q2 P2 (1)](https://github.com/kaifahmed2002/Medical_Data_Analysis/assets/92524691/bde6db10-5278-431e-afbe-d63e5e24fca8)

On the other hand, Median medical charges of Female's is Greater then Male's

Female - $9,575, 

Male - $9,289.


3. Is there correlation between the number of dependents a patient has and medical charges?

![Q3](https://github.com/kaifahmed2002/Medical_Data_Analysis/assets/92524691/2e9974ae-a33b-477a-83ca-129b65fb94ca)

The Correlation between Number of Children and Medical Charges is 0.085, that means their is no correlation between the number of dependents a patient has and medical charges.


4. Is there correlation between age and medical charges?
   
![Q4](https://github.com/kaifahmed2002/Medical_Data_Analysis/assets/92524691/a204a3d6-3481-473f-a06e-c9809a2c7dfe)

The Correlation between Patients Age and Medical Charges is 0.30, That means their is low positive correlation between patients age and medical charges, This suggests that medical charges tend to increase as the age of the patient increases


5. Do individuals with higher BMI have higher medical costs?

![Q5](https://github.com/kaifahmed2002/Medical_Data_Analysis/assets/92524691/a6cd1aff-b681-431b-9fab-30a84a8e398a)

Each BMI (weight) category has the following average charges: Underweight(below 18.5) - $9,042, Normal(18.5 - 24.9) - $10,650, Overweight(25.5 - 29.9) - $11,164, Obese(30+) - $15,497, The Obese weight category exhibits the highest average charges, while the Underweight category has the lowest. This suggests that medical charges tend to increase with weight gain. 


6. What is the relationship between smoking and medical charges?
   
![Q6 P1 (1)](https://github.com/kaifahmed2002/Medical_Data_Analysis/assets/92524691/91bfe98f-5b17-45f6-a60e-a3fd7ace8de6)

The average medical charges of smokers and non-smokers are as follows: Smoker - $31,886, Non-smoker - $8,507. Patients who smoke have significantly higher average medical charges, with smokers having an average of $31,886 compared to $8,507 for non-smokers. 


![Q6 P2](https://github.com/kaifahmed2002/Medical_Data_Analysis/assets/92524691/1be35244-94fb-454f-8797-69334b19e911)

As seen in the histogram, the distribution of charges of smokers is bimodal. The two modes are indicative of the subgroups related to BMI. 
