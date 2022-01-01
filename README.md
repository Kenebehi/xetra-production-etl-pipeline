# xetra-production-etl-pipeline
A simple production ready pipline that takes in a time series dataset from one S3 bucket run transformations on the data and places it intarget bucket.

## Requirements
- Target format of the transformed data should br parquet
- The first date of the report should be given as an input (The first time the job runs all dates from the input date until todays date should be extracted and report built)
- There should be autodetection for all files that are already processed.


## View Source Data
```
aws s3 ls deutsche-boerse-xetra-pds/2017-08-01/ --no-sign-request
```

## Production Environment
Code is pushed to the github repository with configuration files as well as a docker file. The Dockerfile is used to create a Docker image. The Docker image will be pushed to an image repository (Dockerhub), from the image repository the image can be pulled by orchestration tool such as airflow. The orchestration tool would create a docker container on an execution platform such as Kubernetes. The Docker container will have the execution code and when this is mounted the configuration files and secrets should also be loaded. Finally the orchestration tool would trigger the application according to the required schedule, so the data would be Extracted from S3 bucket, Transformed and Loaded to the Target S3 bucket.

## Steps to Run
### Set up vitual environment
<pre><font color="#8AE234"><b>❯</b></font> pipenv shell --python /home/ubuntu/anaconda3/bin/python
</pre>


## AWS Setup
<pre><font color="#8AE234"><b>❯</b></font> IAM ❯ USER ❯ ADD_USER ❯ ACCESS_TYPE (PROGRAMMATIC ACCESS) ❯ PERMISSIONS (ATTACH EXISTING POLICY) ❯ AMAZONS3FULLACCESS
</pre>