# assignment17.1
Steps taken to solve the problem:
-	Read the background information about the data and detailed description of the featureset
-	Data Cleansing:
o	Dropped Duplicates
o	Plotted data in bar charts
o	Dropped “unknown” data points which reduced the data set by 10K data points of 25%
o	Converted Object Data types into “new columns” using “GetDummies” function and Numerical Data data types into Scaler quantity
-	Expected correlation target is >0.80
-	Modelling
o	Created a “Logistics Regression Model” with score of 0.90 and stored Train Time, Training Score and Test Score in Score dataframe
o	Created KNN Model and stored Time and scores in Score data frame
o	Created Decision Tree Model and stored Time and scores in Score data frame
o	Created SVC Model and stored Time and scores in Score data frame
o	Score table as below
 
o	Overall High Scores for Training and Test datasets shows that model are good at default settings 
	SVC takes lot of time to run compare to other methods 
-	Improving the models
o	Correlation between factors showed some opportunity for reducing number of feature used in the model. For example:  factors like 'euribor3m' and 'emp.var.rate' or 'euribor3m' and 'nr.employed' have high correlation with each other thus, dimensionality of the dataset can be reduced.
o	Performed “feature selection” steps on the data set
o	Rewrote all the steps into “pipe” Pipeline with following steps 
	“prep” : another pipeline (using column_transformer function) for preparing the Data and comprise of two steps
•	StandardScaler for Numerical Data 
•	OneHotEncoder for Object Data
	“column_selector”: step for feature selection to top 7 features
•	Ran multiple combinations and it seems model will be good even with less number of features but kept 7 as few comments in the questionnaire stated to use “top 7” features
	Ran all models one at a time and stored parameters like, run time, Train accuracy and Test accuracy data in a grid_score dataframe
•	“pipe” function is essentially repeating the previous work but now this pipeline can be used for “Grid Search CV” to optimize the hyperparameters
o	Optimizing hyperparameters
	Drafted a dictionary of parameters to optimize for each “Model” Type as belo
	# optimizing logistic regression parameters
•	# optimizing logistic regression parameters 
•	# knn parameters for model tuning
o	#k_range = [30,32,34,36,38,40] 'knn params used'
o	#params = {'m__n_neighbors' :k_range}  'knn params used'
•	#decision tree parameters for model tuning
o	k_range = list(range(1,10))
o	params = {'m__max_depth' : k_range, 'm__criterion':["gini", "entropy", "log_loss"]}
•	  # SVC parameters for model tuning
o	#params = {'m__C': [0.1, 1, 10, 100],
o	#          'm__gamma': [1, 0.1, 0.01],
o	#          'm__kernel': ['rbf']}
	Ran GridSearchCV function for each of the model types and stored the data to compare with original models
	Most models showed marginal improvement with 7 features 
 
	Also checked “Precision” and “recall” and while precision is high, recall is low 
Results
-	Decision Tree seem to be best model with high Train and Test Accuracy
-	Best parameters for various algorithms are as follows
-	 
-	More work needs to be done to understand why Recall score is low.
