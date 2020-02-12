# Boost Customer Satisfaction with Machine Learning (LSTM recurrent neural network)

The goal of this project is to use AWS infrastructure to make sentiment analysis
at scale. The data was provided by Stanford University. The trained model
can be used to make real-time and batch predictions. The repository contains 
infrastructure as code that can be deployed for real-time predictions.

Figure 1.0 shows the architecture of the project

![architecture](https://www.tarasowski.de/img/satisfaction/figure-10-architecture.png)
**Figure 1.0: Sentiment Analysis Architecture**

## Pre-requisites
* Python v3.8
* PyTorch v0.4.0
* Sagemaker v1.40.9
* Joblib v0.14.1
* Numpy v1.18.0
* Pandas v1.0.1
* Nltk v3.4.5
* Beautifulsoup v4.8.2

## Getting Started
The machine learning pipeline can run locally as well as in the cloud. There is
one limitation of AWS Sagemaker, there is no way to manage the training process
through CloudFormation. Due to the described limitation, the training process needs to be
started first before deploying the model and the endpoint. 

Following steps should be executed to setup the sentiment analysis end-to-end machine learning pipeline:

1) Download the data from the Stanford server. Data will be downloaded into the input folder.
* Basic usage: `make download`

2) Preprocess the downloaded data and save the train.csv into the input folder.
* Basic usage: `make preprocess`

3) Train the model on AWS Sagemaker. GPU-enabled instances are available on request.
* Basic usage: `make train-cloud` 
* Options:
  * Train on the local machine: `make train-local`

4) Wait until the training job finishes and get the job name. It can be
found in the AWS Console or AWS CLI. Run the command to deploy Sagemaker
endpoint, API Gateway endpoint, and AWS Lambda. 
* Basic usage: `make deploy job_name=XX stack_name=XX` 

5) Test the newly created endpoint. Send a test review to receive 1 for positive
and 0 for negative.
* Basic usage: `curl -d "It was an awesome movie. I really like it" -X POST https://xxxxxxx.execute-api.aws-region.amazonaws.com/predict`

**Important**: The AWS Sagemaker endpoints are billed per seconds. The endpoints
are not serverless. Therefore the endpoint should be deleted if not in use. The deletion of the CloudFormation
stack also deletes the AWS Sagemaker endpoint. 

## Support
Patches are encouraged and may be submitted by forking this project and
submitting a pull request through GitHub.

## Credits
The project was developed during the ML program of
[Udacity.com](https://www.udacity.com/)

## Licence
Released under the [MIT License](./License.md)

