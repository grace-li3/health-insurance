# Predicting Health Insurance Costs Through Demographic Factors

## Overview and Motivation

Health insurance is a critical component in managing both personal health and financial stability. In the United States, the cost of health insurance and the decision to obtain coverage are influenced by various factors, some of which are deeply embedded within the demographic characteristics of the individual. Despite significant strides in healthcare accessibility, approximately 8% of Americans remain uninsured, highlighting a persistent gap in coverage. This project aims to explore the relationship between demographic factors—specifically age, BMI, and smoking status—and the likelihood of an individual’s health insurance premiums exceeding national average thresholds.

The motivation for this study stems from the need to understand and potentially recalibrate the way health insurance premiums are determined and how these determinations align with fairness and equity. Inspired by research that investigates the impact of demographic and perceptual variables on young adults’ decisions to be covered by private health insurance, this project seeks to delve deeper into the correlation between demographic characteristics and insurance costs. Questions such as "Is there a way to more accurately predict a person’s level of coverage based on their demographic characteristics?", "How do insurance rates change based on one’s observable characteristics?", and "Is there a reason why some pay more than others for health insurance coverage?" are fundamental to understanding disparities in insurance coverage and ensuring that rates are equitable. By identifying the key factors that influence premium costs, this research could provide insights that help insurers design fairer pricing models and possibly extend coverage to larger segments of the population.

## Data Background

The dataset, sourced from Kaggle’s US Health Insurance Costs Dataset, comprises 1,338 entries of insured data, providing a rich foundation for exploring the nuances of health insurance underwriting in the United States. Each entry in this dataset encapsulates various demographic attributes of the insured individuals, including age, sex, BMI, number of children, smoker status, and region, paired with the corresponding insurance charges. This comprehensive data enables a detailed analysis of how these factors influence insurance premiums.

*Demographic and Health Variables*

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

<img width="284" alt="Screenshot 2025-02-25 at 12 47 31 PM" src="https://github.com/user-attachments/assets/73e1a1cb-c3d3-421d-8271-b7def8a07292" />

*Figure 1: Correlation Coefficient Heatmap*

A histogram displaying the age distributions was also used in the explanatory analysis. The data revealed an over-representation of younger in- dividuals in their twenties, while the other age groups appeared to be more evenly distributed.

<img width="276" alt="Screenshot 2025-02-25 at 12 48 18 PM" src="https://github.com/user-attachments/assets/69069e78-b1c1-445c-b8ab-7cb16e59f687" />

*Figure 2: Age Distribution*


##### Logistic Regression

A logistic regression model was used on our dataset to predict the binary outcome of being charged below or above the national average. In order to create a binary classification of our target variable, charges, we calculated the national average of the charges in our dataset. After calculating the mean charges, we created a function that assigned an individual to class 0 if their charges were below the national average or class 1 if their charges were above the national average. Based on the results of our exploratory analysis, we also converted our categorical predictors—smoking status and sex—into dummy variables. We then used a test-train split (80% training data, 20% testing data) to train our data on a logistic regression model.

<img width="282" alt="Screenshot 2025-02-25 at 12 48 52 PM" src="https://github.com/user-attachments/assets/80c97fba-1365-49cb-8d35-34ec382cfbbc" />

*Figure 3: ROC Curve*

The Receiver Operating Characteristic (ROC) curve presented in the graph evaluates a logis- tic regression model, displaying an impressive Area Under the Curve (AUC) of 0.92. This high AUC indicates that the model excels at distin- guishing between individuals whose health in- surance premiums are likely to exceed the na- tional average and those whose premiums do not, based on demographic factors such as age, BMI, and smoking status. The curve, which re- mains significantly above the diagonal line of randomness—especially in the lower left cor- ner—highlights the model’s high sensitivity and low false positive rate. This performance sug- gests not only the accuracy of the model but also its reliability in minimizing incorrect identifications of high-premium cases. Such a model is extremely beneficial in the health insurance sector, aiding insurers and policymakers by enhancing risk assessment capabilities and enabling the formulation of more customized and equitable inurance policies based on individual risk profiles.

<img width="263" alt="Screenshot 2025-02-25 at 12 49 39 PM" src="https://github.com/user-attachments/assets/517a5504-0bd6-4aba-94b7-ee3cb15bd2f5" />

*Figure 4: Predicted Probability Distribution*

The graph effectively illustrates the calibration of the prediction model. For individuals not above the average insurance cost, the predicted probabilities are largely clustered towards the lower end of the probability scale, indicating ac- curate model predictions for this group. Con- versely, for those whose costs are above average, a significant concentration of predictions accu- rately gathers at the higher end, particularly at a probability of 1.0, showcasing strong model con- fidence in these predictions. However, there are overlaps in the middle probabilities (around 0.4 to 0.6), suggesting some instances of uncertainty or mis-classification by the model. This overlap could be an area of focus for improving model precision, potentially by incorporating more fea- tures or fine-tuning model parameters to better distinguish between the two classes. Overall, the distribution indicates a generally effective model for predicting whether individual insurance pre- miums exceed average thresholds, which is vital for targeted interventions and tailored insurance policy development.


##### Multi-Linear Regression

To predict the exact insurance charge, we developed a multi-linear regression model that uses age, smoking status, and BMI as predictors. The three predictors were chosen because they had the highest correlation coefficients (0.3, 0.79, and 0.2, respectively) with charge. The variables had very low correlations with one another, so there is no collinearity in this model.

The features were engineered in four different ways: original predictors, square root transformed predictors, log transformed predictors, and a fifth-degree polynomial fit on age. Since smoking status was one-hot encoded, integer 1 was added to the smoking status column ("smoker yes") to prevent errors due to log(0).

To choose the best model, we used a train-test split of ratio 8:2 and ran a 10-fold cross-validation on the four models. k-Fold cross-validation was used since it is less computationally expensive than Leave-One-Out Cross-Validation (LOO CV), and our dataset is relatively large (1,338 observations). We then collected the R2 score and the Mean Squared Error values of each model.

<img width="198" alt="Screenshot 2025-02-25 at 12 50 32 PM" src="https://github.com/user-attachments/assets/fb56702f-723d-470d-8ffe-c78af61bceed" />

*Figure 5: MSE and R2 Values of Feature Combinations*

We observed that while the square root transfor- mation model (combination 2) had the highest R2 score of 0.7499, the log transformation mode (combination 3) had the lowest MSE value of 0.2232.

To make sure that our model is not overfitting and for higher accuracy, we implemented the Lasso regularization. We chose the Lasso regres- sion as it performs better for models like ours where only one predictor (smoking status) has a significant correlation coefficient while the oth- ers’ coefficients are substantially smaller. Using the built-in Lasso and LassoCV modules, we ran a 10-fold CV with max iter = 100000, which gave us the best Lasso regression model. The line plot on figure 6 below shows the trend of the MSE of the model according to various lasso alphas.

<img width="265" alt="Screenshot 2025-02-25 at 12 51 47 PM" src="https://github.com/user-attachments/assets/9fc0dc8b-a0a6-4f7a-aed5-a53170348171" />

*Figure 6: Lasso Alphas vs MSE*

This indicates that a higher alpha leads to worse prediction accuracy for this model; opti- mal performance, in terms of minimizing MSE, is achieved at lower alpha values.

The best lasso alpha, although not visible from the graph, is 0.000745 and the lasso model coefficients of age, bmi, and smoker yes are [0.41691321 0.12753788 0.74629121], respectively. Compared to the not-regularized square root model, the Lasso regularized square root model has a higher R2 score but a slightly higher MSE. The Lasso regularized square root model, despite having a higher R2 score of 0.8188 compared to the square root transformation fit at 0.7219, indicating better explanatory power and model fit, paradoxically exhibits a higher Mean Squared Error (MSE) of 1.7346 compared to 0.2370 in the non-regularized model, suggesting less accuracy in prediction. This contrast sug- gests that while the Lasso model may better cap- ture the variance within the dataset, it does so at the expense of larger errors on specific predictions, likely due to the regularization imposing a trade-off between complexity and prediction error.

<img width="243" alt="Screenshot 2025-02-25 at 12 53 04 PM" src="https://github.com/user-attachments/assets/83fb3844-ac09-48e0-a361-9eddf7181a58" />

*Figure 7: MSE and R2 Values of Lasso Model*

Finally, we must evaluate if the data at hand is suitable for multi-linear regression. The scatter plot to the right demonstrates the distribution of residuals.

<img width="253" alt="Screenshot 2025-02-25 at 12 53 33 PM" src="https://github.com/user-attachments/assets/5d17a5f6-1072-42d9-bf31-b68e526b8e9f" />

*Figure 8: Residuals vs Fitted Values*

It shows that the variability of the residuals around the 0 line is not completely uniform (i.e., not homoskedastic), as the variability of the residuals on the left seems to be greater than that on the right. Then again, the histogram of residuals in the square root model shows that most residuals are concentrated in the -0.5 to 0.5 range, but it also points to the existence of some outliers (i.e., some residuals belong in the bins above 0.5). However, the three scatter plots be- low that plot data points according to each pre- dictor (age, BMI, smoking status) against charge show that they are roughly linear.

<img width="260" alt="Screenshot 2025-02-25 at 12 54 14 PM" src="https://github.com/user-attachments/assets/41bd7d60-65b6-422d-9ff7-119299b4dbdd" />

*Figure 9: Distribution of Residuals*

The scatter plots below illustrate the relation- ships between square root transformed age, BMI, and smoking status against health in- surance charges. A linear increase occurs in charges as age progresses. Smokers incur signif- icantly higher charges than non-smokers, under- lining the profound impact of smoking on insur- ance costs. The relationship between BMI and charges is less definitive, with a moderate up- ward trend indicating that while BMI influences charges, its effect is overshadowed by other fac- tors like age and smoking status. These visu- alizations clearly underscore the varying degrees of influence that different demographic factors have on health insurance premiums, with smok- ing status being the most decisive predictor.

<img width="929" alt="Screenshot 2025-02-25 at 1 07 53 PM" src="https://github.com/user-attachments/assets/bc151e04-a4fb-4a73-bb27-0cdfab99747f" />


## Conclusion

This project has comprehensively explored the relationship between key demographic factors—age, BMI, and smoking status—and health insurance premiums. Through a detailed exploratory analysis, including the use of logistic and multiple linear regression models, the study has confirmed that these factors significantly influence insurance costs. The models developed have shown high accuracy, as indicated by R2 scores and MSE values, with the best model utilizing a square root transformation to minimize error. Additionally, Lasso regularization helped refine the model further by addressing overfitting and enhancing predictive accuracy, particularly for smoking status, which demonstrated the most significant impact on premiums. Overall, we were able to effectively use a logistic model to predict whether or not an individual’s health insurance charges were above the national average. The results of our model indicate that smoking increases the likelihood of being charged above the national average by e5.83. Furthermore, if age and BMI increase by one unit, the likelihood of being charged above the national average is e0.060 and e0.016. As a result, smoking seems to be the biggest factor in being charged above the national average based on the predictors used.

The coefficients of the lasso-regularized multiple linear regression model that we developed were: 0.417 (age), 0.128 (BMI), and 0.74629121 (smoker); note that the values here are standardized. These predictors were also transformed using square roots as doing so increased the R2 score. However, the residuals plotted against values fitted with our model indicate that the data is not homoskedastic, which indicates that the model is not well-defined and that the target variable (charge) is inadequately defined by the predictor variables, which may cause biased, inaccurate, or inconsistent estimates. On the other hand, using the Lasso regularization, we were able to achieve an R2 score of 0.819, which indicates that our model fits the data well despite the low level of homoskedasticity. After comparing the predicted charges based on our model to the actual charges, we saw that our model underestimated the charges by around 4.2%. The underestimation could have been attributed to the over-representation of young adults in our dataset.

Based on the findings of this project, which analyzed the relationship between demographic factors and health insurance premiums, we can suggest policies regarding risk-adjusted premium structures, where we implement policies that allow for premiums to be adjusted based on quantifiable risk factors such as age, BMI, and smoking status. This would ensure that individuals are charged premiums that accurately reflect their health risk rather than flat rates that might penalize healthier individuals or undercharge higher-risk individuals. Given the significant impact of smoking status on insurance costs, policies should support the introduction of subsidized or free smoking cessation programs. This not only helps in reducing the public health burden but can also decrease individual insurance costs, making health coverage more affordable.

Additional avenues for future investigation on health insurance could be investigating regional impact, analyzing trends in charges over time, or analyzing the effects of pre-existing conditions and its impact on being charged above the national average.

## Bibliography
Cantiello, J., Fottler, M.D., Oetjen, D. et al. The impact of demographic and perceptual variables on a young adult’s decision to be covered by private health insurance. BMC Health Serv Res 15, 195 (2015). https://doi.org/10.1186/s12913-015-0848-6
US health insurance dataset. (2020, February 16). Kaggle. https://www.kaggle.com/datasets/teertha/ushealthinsurancedataset
