# Predicting Health Insurance Costs Through Demographic Factors

## Overview and Motivation

Health insurance is a critical component in managing both personal health and financial stability. In the United States, the cost of health insurance and the decision to obtain coverage are influenced by various factors, some of which are deeply embedded within the demographic characteristics of the individual. Despite significant strides in healthcare accessibility, approximately 8% of Americans remain uninsured, highlighting a persistent gap in coverage. This project aims to explore the relationship between demographic factors—specifically age, BMI, and smoking status—and the likelihood of an individual’s health insurance premiums exceeding national average thresholds.

The motivation for this study stems from the need to understand and potentially recalibrate the way health insurance premiums are determined and how these determinations align with fairness and equity. Inspired by research that investigates the impact of demographic and perceptual variables on young adults’ decisions to be covered by private health insurance, this project seeks to delve deeper into the correlation between demographic characteristics and insurance costs. Questions such as "Is there a way to more accurately predict a person’s level of coverage based on their demographic characteristics?", "How do insurance rates change based on one’s observable characteristics?", and "Is there a reason why some pay more than others for health insurance coverage?" are fundamental to understanding disparities in insurance coverage and ensuring that rates are equitable. By identifying the key factors that influence premium costs, this research could provide insights that help insurers design fairer pricing models and possibly extend coverage to larger segments of the population.

## Data Background

The dataset, sourced from Kaggle’s US Health Insurance Costs Dataset, comprises 1,338 entries of insured data, providing a rich foundation for exploring the nuances of health insurance underwriting in the United States. Each entry in this dataset encapsulates various demographic attributes of the insured individuals, including age, sex, BMI, number of children, smoker status, and region, paired with the corresponding insurance charges. This comprehensive data enables a detailed analysis of how these factors influence insurance premiums.

## Demographic and Health Variables

Age: The individuals range from young adults (as young as 18) to older adults (up to 60 years old).

Sex: Both males and females are represented in the dataset.

BMI (Body Mass Index): The BMI values vary widely, indicating a diverse set of body weights relative to height, which is an important health risk factor.

Children: The number of children covered by the insurance ranges from 0 to 3, reflecting different family sizes.

Smoker: Smoking status is a crucial health risk factor and is indicated as either "yes" or "no".

Region: The geographic distribution includes regions like the Southeast, Northwest, and Northeast, which could correlate with regional health trends and insurance pricing models.

Insurance Charges

Charges vary significantly, from as low as $1,725 to as high as $29,023. This wide range suggests that factors like age, BMI, smoking status, and perhaps even the region significantly influence insurance costs.

*Notable Observations*

Impact of Smoking: The dataset highlights the impact of smoking on insurance costs. For instance, a 19-year-old female smoker has insurance charges of approximately $16,884, which is high relative to her age group.

Age and Cost Correlation: Older adults tend to have higher insurance charges, as seen with the 60-year-old female, with charges nearing $29,023.

Region and Insurance Cost: Different regions might have different average healthcare costs, potentially influencing the insurance charges.

## Exploratory Analysis

An exploratory analysis was conducted to determine the most influential predictors for health insurance charges. A correlational heat map revealed that age, BMI, and smoking status demonstrated the strongest associations with charges. Age and smoking status show strong associations with charges, with smoking likely having the most significant impact. Interestingly, the number of children an individual has showed a slightly higher correlational value than sex; however, its impact on charges was notably lower than BMI, smoking status, and age.

##### Logistic Regression

A logistic regression model was used on our dataset to predict the binary outcome of being charged below or above the national average. In order to create a binary classification of our target variable, charges, we calculated the national average of the charges in our dataset. After calculating the mean charges, we created a function that assigned an individual to class 0 if their charges were below the national average or class 1 if their charges were above the national average. Based on the results of our exploratory analysis, we also converted our categorical predictors—smoking status and sex—into dummy variables. We then used a test-train split (80% training data, 20% testing data) to train our data on a logistic regression model.

##### Multi-Linear Regression

To predict the exact insurance charge, we developed a multi-linear regression model that uses age, smoking status, and BMI as predictors. The three predictors were chosen because they had the highest correlation coefficients (0.3, 0.79, and 0.2, respectively) with charge. The variables had very low correlations with one another, so there is no collinearity in this model.

The features were engineered in four different ways: original predictors, square root transformed predictors, log transformed predictors, and a fifth-degree polynomial fit on age. Since smoking status was one-hot encoded, integer 1 was added to the smoking status column ("smoker yes") to prevent errors due to log(0).

To choose the best model, we used a train-test split of ratio 8:2 and ran a 10-fold cross-validation on the four models. k-Fold cross-validation was used since it is less computationally expensive than Leave-One-Out Cross-Validation (LOO CV), and our dataset is relatively large (1,338 observations). We then collected the R2 score and the Mean Squared Error values of each model.

## Conclusion

This project has comprehensively explored the relationship between key demographic factors—age, BMI, and smoking status—and health insurance premiums. Through a detailed exploratory analysis, including the use of logistic and multiple linear regression models, the study has confirmed that these factors significantly influence insurance costs.

The models developed have shown high accuracy, as indicated by R2 scores and MSE values, with the best model utilizing a square root transformation to minimize error. Additionally, Lasso regularization helped refine the model further by addressing overfitting and enhancing predictive accuracy, particularly for smoking status, which demonstrated the most significant impact on premiums.

Based on the findings of this project, we suggest policies regarding risk-adjusted premium structures that allow for premiums to be adjusted based on quantifiable risk factors such as age, BMI, and smoking status. This would ensure that individuals are charged premiums that accurately reflect their health risk rather than flat rates that might penalize healthier individuals or undercharge higher-risk individuals. Given the significant impact of smoking status on insurance costs, policies should support the introduction of subsidized or free smoking cessation programs to reduce the public health burden and decrease individual insurance costs, making health coverage more affordable.

Future research could investigate regional impact, analyze trends in charges over time, or assess the effects of pre-existing conditions on insurance premiums.

## Bibliography
Cantiello, J., Fottler, M.D., Oetjen, D. et al. The impact of demographic and perceptual variables on a young adult’s decision to be covered by private health insurance. BMC Health Serv Res 15, 195 (2015). https://doi.org/10.1186/s12913-015-0848-6
US health insurance dataset. (2020, February 16). Kaggle. https://www.kaggle.com/datasets/teertha/ushealthinsurancedataset
