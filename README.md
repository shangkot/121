# Operationalizing Machine Learning

## Overview
This project is part of the Udacity Nanodegree Program, Machine Learning Engineering with Microsoft Azure.  
The objective of this project is to show how to operationalize Machine Learning.  

The project is divided in two steps:  
* The manual deployment of a Machine Learning model
* The automated deployment through a pipeline for a part of the process




## Business Case
The dataset provided for the project is the UCI [Bank Marketing Data Set](https://archive.ics.uci.edu/ml/datasets/Bank+Marketing).  
The data is related with direct marketing campaigns of a Portuguese banking institution.  
The classification goal is to predict if the client will subscribe a term deposit, based in the features provided such as age, job, marital status, education.  





## Architectural Diagram

![Architecture Diagram](images/Architecture_Diagram.png)


### Manual Deployment
The steps for the manual deployment were:  
* Get the dataset: it was provided as a URL link to a csv file.  
* Register the dataset: the dataset was registered as a tabular dataset in Azure ML Studio.  
* Generate an AutoML experiment: an AutoML experiment was created, configured, and executed, to generate several classification models.  
* Select the best model: the best model was selected, based on the accuracy obtained by each model.  
* Deploy the best model: the model was deployed manually.  
* Enable Application Insights: after the deployment, Application Insights was enabled through code, to monitor the model.  
* Consume endpoints: the deployed model was tested by interacting with the endpoints through code.  


### Pipeline Deployment
A pipeline was created through code in a Jupyter notebook provided for the project.  
This pipeline was focused on the execution of an AutoML experiment.  





## Key Steps

### Step 1. Authentication
To ensure a continuous flow of the operations, Authentication was enabled through a Service Principal.  

The steps followed to create the Service Principal were:  
* Login to the Azure cloud platform.  
* Add the Azure Machine Learning Extension.  
* Create the Service Principal.  
* Assign access to the workspace and resource group.  

![Authentication Step 1](images/1.%20Authentication/1_Create_Service_Principal.png)
![Authentication Step 2](images/1.%20Authentication/2_Get_objectid.png)
![Authentication Step 3](images/1.%20Authentication/3_Assign_sp.png)


### Step 2. Automated ML Experiment

#### Dataset Registration
The dataset provided as an [URL link](https://automlsamplenotebookdata.blob.core.windows.net/automl-sample-notebook-data/bankmarketing_train.csv) was registered in the Dataset section as a tabular dataset.  

![Dataset registration](images/2.%20AutoML%20Experiment/1_BankMarketing_Dataset.png)


#### AutoML Experiment Execution
An AutoML experiment was configured as a Classification task and executed.  

![AutoML Experiment 1](images/2.%20AutoML%20Experiment/2_Completed_Experiment_1.png)
![AutoML Experiment 1](images/2.%20AutoML%20Experiment/2_Completed_Experiment_2.png)


The best model was a Voting Ensemble.  

![Best Model 1](images/2.%20AutoML%20Experiment/3_Best_Model_1.png)
![Best Model 2](images/2.%20AutoML%20Experiment/3_Best_Model_2.png)
![Best Model 3](images/2.%20AutoML%20Experiment/3_Best_Model_3.png)
![Best Model 4](images/2.%20AutoML%20Experiment/3_Best_Model_4.png)


### Step 3. Deploy the Best Model
The best model was deployed manually, with an Azure Container Instance. Authentication was enabled, so the Service Principal created previously could be used.  

![Model Deployment 1](images/3.%20Deploy%20Model/1_Deploy_Model.png)
![Model Deployment 2](images/3.%20Deploy%20Model/2_Deploy_Model.png)


### Step 4. Enable Logging
Although Application Insights can be enabled manually when the model is deployed, the project requested to enable it through code, once the model was deployed.  

This is the deployed model with Application Insights disabled.  
![Application Insights 1](images/4.%20Enable%20Login/1_AppInsights_Disabled.png)

This is the execution of the script to enable Application Insights.  
![Application Insights 2](images/4.%20Enable%20Login/2_Run_enable_script.png)

This is the deployed model with Application Insights enabled.  
![Application Insights 3](images/4.%20Enable%20Login/3_AppInsights_Enabled.png)

This is the execution of the script to produce the logging output.  
![Application Insights 4](images/4.%20Enable%20Login/4_Logs_1.png)
![Application Insights 5](images/4.%20Enable%20Login/5_Logs_2.png)

This is the Application Insights Dashboard.  
![Application Insights 6](images/4.%20Enable%20Login/6_Application_Insights.png)


### Step 5. Swagger Documentation
Endpoints allow other services to interact with deployed models. A deployed service can be consumed via HTTP APIs using various methods like:  
* Swagger
* JSON workloads


##### Swagger
Swagger is a tool that helps build, document, and consume RESTful web services.  
Azure provides a swagger.json file that is used to create a web site that documents the HTTP endpoint for a deployed model.  

This is the web site created for the model.
![Swagger 1](images/5.%20Swagger/1_model.png)

It has the GET and POST HTTP requests supported for the model.

This is an example of an interaction with the POST request.  
The model receives a data set with values for the features.  
![Swagger 2](images/5.%20Swagger/2_model_response_1.png)

And produces a predictions as a response. In this case, the prediction was that the client will not subscribe.  
![Swagger 3](images/5.%20Swagger/2_model_response_2.png)


### Step 6. Consume Model Endpoints
Other way to interact with the endpoint is through a python script. This was provided as part of the project and contains:  
* The URL to the endpoint.  
* The key to authenticate.  
* A JSON data set to score.  
* A POST request.  

This is the output of the provided script:  
![Endpoint 1](images/6.%20Consume%20Endpoints/1_Results.png)

An additional script was tested, containing data from the validation dataset:  
![Endpoint 2](images/6.%20Consume%20Endpoints/2_Results_val.png)


### Step 7. Create, Publish, and Consume a Pipeline
A Jupyter notebook provided for the project was used to create a pipeline that automates the execution of an AutoML Experiment.  

This is the pipeline that was created.  
![Pipeline 1](images/7.%20Pipeline/1_Pipeline_creation.png)

This is the pipeline endpoint.  
![Pipeline 2](images/7.%20Pipeline/2_Pipeline_endpoint.png)

This is the Bankmarketing dataset, the AutoML module, and the Published Pipeline Overview.  
![Pipeline 3](images/7.%20Pipeline/3_Dataset_and_AutoML_model.png)

This is the Jupyter notebook showing the Use RunDetails widget.  
![Pipeline 4](images/7.%20Pipeline/4_Pipeline_run.png)

This is the scheduled run in Azure ML Studio.  
![Pipeline 5](images/7.%20Pipeline/5_Pipeline_completion.png)
![Pipeline 6](images/7.%20Pipeline/6_Pipeline_completion.png)





## Future Improvements
Some suggestions to improve the project are:  
* Include more pipeline steps to create a fully automated process.  
* Test datasets for different business cases.  



## Screen Recording
This is the link to the screen recording of the project.  
https://www.youtube.com/watch?v=Wp1VvHod4EE&feature=youtu.be

