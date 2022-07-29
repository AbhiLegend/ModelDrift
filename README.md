# ModelDrift
## Evidently and monitoring production models
We have created our ml models but to get them to production is always tough <br />
As with time the model degrades.For analysing the model drift we need realtime monitoring. <br />
Evidently is such a tool/library that helps us analyse and track data and ml models for the lifecycle. <br />
More details on evidently library [a link] (https://github.com/evidentlyai/evidently) <br />
## Model Scoring and model drift
For showing model scoring and model drift we need evidently library.We will work on a regression process ml model to be deployed in hroku. <br />
We will be using the UCI Bike sharing dataset <br />
## More on Model drift with respect to evidently library
Partculary we will focus on datadrift which is a type of model drift .The description is mentioned in the previous section <br />
If we elaborate evidently it works on the mentioned ways. <br />
![alt text](https://github.com/AbhiLegend/ModelDrift/blob/main/model%20drift_images/ed.PNG) <br />
## Model Quality <br />
We have a model running.Using Evidently library we are able to evaluate the model quality and get all the performance so track where the model fails <br />
## Data Drift 
As the ml model runs,we are bound to get get model drift specifically we are focussing on a type of model drift named as data drift. <br />
Using evidently library we are able to run the statistical tests through which we can compare the input feature distributions and visually explore the drift. <br />
## Target Drift
Over the time applying evidently library we can do a good examination,we can see how model predictions and target behaviour change over the time. <br />
## Data Quality 
As the model runs,we can apply evidently library to get a complete snapshot of of data health and get inside deeper to explore feature behaviour and statistical properties.<br />


## How to check for a drift within a production model
We will be using fastapi and the production model needs to be deployed in heroku.For proper and ease of deployment we will use github <br />
Make sure we have a github account,heroku account ready. <br />
We need to fork the starter code.Accordingly we will also work on the exercise too <br />
The repo contains the following <br />
1)Static folder("Within that all the HTML reports will be generated in Heroku"). <br />
2)A Procfile to get all necessary commands working in Heroku. <br />
3)main.py python file that contains all the programming logic and code for training the data as well as checking the drift <br />
4)requirements.txt file that contains all the libraries to be installed in heroku <br />
5)runtime.txt file that contains which python runtime that needs to be installed in heroku <br />
Exercise <br />
Q1) What are the necessary import files for FASTAPI to be included in main.py file <br />
1> from fastapi import FastAPI and from fastapi.staticfiles import StaticFiles <br />
2> from fastapi import FastAPIs <br />
3>No need to import FASTAPI <br />
4)from fastapi import APIRouter <br />
Answer:1> <br />
Q2)To get going with evidently which library needs to be added to requirements.txt file <br />
1> evidently==0.1.53.dev0 <br />
2> evidently==1 <br />
3> None of these <br />
Answer 1>  <br />
Q3>To get going with evidently dashboard which import is necessary in main.py file <br />
1>import requests <br />
2>import io <br />
3>from evidently.dashboard import Dashboard <br />
Answer 3> <br />
Q4>What is the command that should go inside the Procfile so that the entire code works properly in heroku. <br />
Answer web: uvicorn main:app --host=0.0.0.0 --port=${PORT} <br />
Solution is provided completely in fast7 repo <br />
## Model training and implementing evidently for performance 
For the Dataset we will be using Bike sharing data from UCI <br />
We are not getting in deep into the model creation code as it has been covered.The main.py file works on monitoring bicycle demand data.We unzip the file start <br />
reading it pandas dataframe.After that we start building the regression model with training . <br />
Model performance part is the most important phase where we implement evidently.
First we do column mapping in main.py file <br />
More on column mapping [a link] (https://github.com/evidentlyai/evidently/blob/main/docs/book/dashboards/column_mapping.md) <br />

```
column_mapping = ColumnMapping()

column_mapping.target = target
column_mapping.prediction = prediction
column_mapping.numerical_features = numerical_features
column_mapping.categorical_features = categorical_features
```

To get the performance and see the dashboard the following code is needed <br />
```
regression_perfomance_dashboard = Dashboard(tabs=[RegressionPerformanceTab()])
regression_perfomance_dashboard.calculate(reference, None, column_mapping=column_mapping)
regression_perfomance_dashboard.save('reports/regression_performance_at_training.html')
```
 ### Exercise
As we have already given the code for week1 results of regression performance similarly write the code for week 2 and week 3 so that the html reports are generated <br />
The codes needed to be inserted in main.py file.There is a portion where we have ""week 2 mentioned" and also "week 3".We need to add the codes there. <br />
Solution <br />
The updated main.py is in the fast7 repo <br />
## Data Drift
Full illustration of Data drift [a link] (https://github.com/evidentlyai/evidently/blob/main/docs/book/dashboards/generate_dashboards.md) <br />
Calculating Datadrift within our main.py file <br />
```
column_mapping = ColumnMapping()

column_mapping.numerical_features = numerical_features

data_drift_dashboard = Dashboard(tabs=[DataDriftTab()])
data_drift_dashboard.calculate(reference, current.loc['2011-01-29 00:00:00':'2011-02-07 23:00:00'], 
                                   column_mapping=column_mapping)
                                   
data_drift_dashboard.save("./static/data_drift_dashboard_after_week1.html")
```

### Exercise  <br />
Calculate Data drift for week 2 <br />
Solution <br />
The complete solution is provided at manin.py in the fast7 repo <br />
Save the file in github ,deploy it in heroku.We have implemented a complete ml model deployment checking all the parameters for model drifting and modifying code as <br />
we have already made the automatic code deployment for CD we are able to change the code directly in github and oberve the changes in the model deployed in heroku. <br />









# Understanding the Evidently Data Drift Dashboard
## Data Drift Table
![alt text](https://github.com/AbhiLegend/ModelDrift/blob/main/model%20drift_images/df.PNG) <br />
The table generated by the html shows the drifting features <br />
Evidently is very useful for early monitoring of model quality <br />
In production to check for model decay <br />
## Deploying the model to heroku and observe Model drift(data drift)(How to deploy the final github repo to heroku steps)
Make sure you have a github account.First fork the repo {fast7} <br />
We will also need a free heroku account for deploying the model <br />
When we get inside heroku we will click on new app <br />
![alt text](https://github.com/AbhiLegend/ModelDrift/blob/main/model%20drift_images/1.PNG) <br />
We will give a new app name leave other details unchanged and click on create app <br />
![alt text](https://github.com/AbhiLegend/ModelDrift/blob/main/model%20drift_images/2.PNG) <br />
It will next take you to the deploy tab make sure that github account is linked.On the deployment method click on github tab <br />
![alt text](https://github.com/AbhiLegend/ModelDrift/blob/main/model%20drift_images/3.PNG) <br />
Search for the forked repo and click on search <br />
![alt text](https://github.com/AbhiLegend/ModelDrift/blob/main/model%20drift_images/4.PNG) <br />
When the repo is found we need to click on connect <br />
![alt text](https://github.com/AbhiLegend/ModelDrift/blob/main/model%20drift_images/5.PNG) <br />
In the Automatic Deployment section make sure we enable automatic deploy <br />
![alt text](https://github.com/AbhiLegend/ModelDrift/blob/main/model%20drift_images/6.PNG) <br />
On the named tab option click on deploy branch <br />
![alt text](https://github.com/AbhiLegend/ModelDrift/blob/main/model%20drift_images/7.PNG) <br />
After all steps you will see the app is deployed.Click on view. <br />
The final site is hosted here [a link] (https://fast7.herokuapp.com/)
The repo which contains the final code [a link] (https://github.com/AbhiLegend/fast7) Fork the repo to follow the complete deployment to heroku <br />
