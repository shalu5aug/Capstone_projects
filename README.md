# Capstone_projects

Predicting Heart disease from a set of attributes of patient’s health 

This data set dates from 1988 and consists of four databases: Cleveland, Hungary, Switzerland, and Long Beach V. It contains 76 attributes, including the predicted attribute, but all published experiments refer to using a subset of 14 of them. The "target" field refers to the presence of heart disease in the patient. It is integer valued 0 = no disease and 1 = disease. Link for the dataset: https://www.kaggle.com/datasets/johnsmith88/heart-disease-dataset

1.	Data:
 Column Descriptions:
 id (Unique id for each patient)
 age (Age of the patient in years)
 origin (place of study)
 sex (Male/Female)
 cp chest pain type ([typical angina, atypical angina, non-anginal, asymptomatic])
 trestbps resting blood pressure (resting blood pressure (in mm Hg on admission to the hospital))
 chol (serum cholesterol in mg/dl)
 fbs (if fasting blood sugar > 120 mg/dl)
 restecg (resting electrocardiographic results)
 -- Values: [normal, stt abnormality, lv hypertrophy]
 thalach: maximum heart rate achieved
 exang: exercise-induced angina (True/ False)
 oldpeak: ST depression induced by exercise relative to rest
 slope: the slope of the peak exercise ST segment
 ca: number of major vessels (0-3) colored by fluoroscopy
 thal: [normal; fixed defect; reversible defect]
num: the predicted attribute

This problem is a classification problem i.e to predict the presence of heart disease or not using some other attributes about patient’s health.

2.	Models used for prediction are:
1.	DecisionTreeClassifier, 
2.	RandomForest 
3.	GradientBoostingClassifier
4.	Logistic Regression 
5.	and SVM 
3.	Data Cleaning:
1.	columns which are not relevant for prediction are removed like ‘id’ 
2.	column ‘hd’ represent different level of heart disease , here we are only predicting the heart disease and not the level so all the values >=1 are replaced as 1 else 0.

4.	EDA
<img width="361" alt="image" src="https://user-images.githubusercontent.com/83147951/194668593-fbb4239a-68bf-4a74-9ef2-2abcc1a295a8.png"> 
Heart disease age group wise, according to the graph heart disease is present in age group mostly between 55-70
 
<img width="411" alt="image" src="https://user-images.githubusercontent.com/83147951/194668643-5a0c5361-36fa-445c-bb25-faece8a68a08.png">
 Correlation between chest pain and heart disease:
It shows heart disease in mostly those patients who have asymptomatic chest pain 

<img width="250" alt="image" src="https://user-images.githubusercontent.com/83147951/194668663-7ca1261f-0aaa-4c26-9bee-5e250c6df38b.png">
Looks like ‘flat’ slope is highly correlated to heart disease.
 
<img width="346" alt="image" src="https://user-images.githubusercontent.com/83147951/194668687-78dc89af-d375-4866-9782-c5f35cff1b38.png">
The ‘reversable defect’ has high correlation with hd.

<img width="288" alt="image" src="https://user-images.githubusercontent.com/83147951/194668711-9c17b3a7-0b51-4035-8338-2eee3ccab1ee.png">
All the type of restecg are equally correlated with hd

5.	Feature Engineering:
Here the categorical columns like 'sex','chest_pain','fbs','restecg','exang','slope','thal' are converted into numerical columns using get_dummies method 
6.	After feature engineering data is divided into train and test set so that models can be trained on train set and tested on test set
7.	Hyperparameter tuning for models:	
Choosing alpha parameter for decision tree
 
<img width="292" alt="image" src="https://user-images.githubusercontent.com/83147951/194668735-7b83555c-0599-45ea-aee2-0003a611819c.png">
Here base decision tree model is trained on training and prediction is made on both training and test set with different alpha values and accuracy is plotted for both the set of data for each alpha value

<img width="285" alt="image" src="https://user-images.githubusercontent.com/83147951/194668757-48a7a3b9-7084-4d31-abc6-516f97b9a68f.png">
Here again base DT model is trained on training data and then cross validation score is computed with cv score = 5 on set of different alpha values. Here the standard deviation is shown as error for each value and corresponding cross validation score 

From both the above graph alpha value of 0.02 is a good value as it is showing accuracy of around 80% on both training and test set

8.	After Decision tree hyperparameter tunning is done for all the models like Random Forest, Gradient boosting, Logistic Regression and SVM using Grid Search CV method.


9.	Feature importance 
<img width="468" alt="image" src="https://user-images.githubusercontent.com/83147951/194668781-d45f8962-5640-4a01-83cb-cf654b7c7617.png">
According to gradient boosting model feature importance of each feature in dataset is shown as above.
It shows that ‘exang_true’ and ‘chol’ are the top two highly correlated features	

10.	Comparison of models:
hyperparameter tunning is done to choose parameters of all the models like alpha , criterion: (gini, entropy), depth of the tree, max features and max leaf nodes, penalty, kernel using grid search CV

accuracy and comparison of all the models using accuracy_score
<img width="273" alt="image" src="https://user-images.githubusercontent.com/83147951/194668835-65b55864-18a0-478d-9693-419776a1f0c0.png">
<img width="287" alt="image" src="https://user-images.githubusercontent.com/83147951/194668869-a250bbdd-b7c7-4961-90a4-7642bdb956e3.png">
Comparison of all the models on NMSE on train and test score using cross validation 
11.	For predicting heart disease, we want a model with high recall value i.e. which makes less type 2 errors:
 
<img width="376" alt="image" src="https://user-images.githubusercontent.com/83147951/194668892-6244d128-9d69-47a9-bd00-e153fa91deca.png">
Here In this graph true positive rate i.e TPR is shown corresponding to different threshold values which helps in deciding the true or false value of the target column.
For ex : if we want all the predicted values above and equal to 0.8 are to be considered as true otherwise false . in the below picture threshold value is shown as 0.5, so if target value is above 0.5 , it is considered to be true(1) otherwise false(0)
<img width="129" alt="image" src="https://user-images.githubusercontent.com/83147951/194668918-076d85aa-381f-4e34-82d5-15b2331f7782.png">

12.	ROC Curve
<img width="382" alt="image" src="https://user-images.githubusercontent.com/83147951/194668935-16ce58cd-059b-4045-985d-e9bdedb351b9.png">

13.	Conclusion :
After comparing accuracy of all the models it turns out that Gradient Boosting and SVC models are performing better than others with almost 83% accuracy.

14.		Future Improvements:
1.	We can use more complicated model like XGboost for more accurate results.
2.	it might possible that different values of categorical columns like ‘trestbps,’cp’,’restecg’, ‘slope’ and ‘thal’  have different impact on possibility of heart disease, so to get better and accurate results
	      these columns can be explored further to check if ordinal encoding can 	  	      be applied on them.


![image](https://user-images.githubusercontent.com/83147951/194668556-9ae78dc9-54c4-4f6a-a7be-1b360356054c.png)
