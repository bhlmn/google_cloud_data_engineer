# Inbox

Here is where I capture notes as I'm learning and then I figure out a spot for them later.

Recommendation Systems:
* Cloud SQL
* Cloud Dataproc

? What recommendation systems can we implement at work?
* Which providers to visit
* Which preventative services to get (gaps in care)
* Which searches to do (enhancements to shortcuts)
* Which services to explore costs
* What to do when you land on the no results screen

Study questions:

How do recommendation systems generally work?

The model is attacking two problems at the same time. First, it is trying to understand which items users rate highly. Second, it is trying to figure out which users are most like you. That way it can estimate things that you haven't tried, but might like, based on what users similar to you like, calibrated agains the quality of those items.

What is a good infrastructure framework for calculating recommendations?

We don't want to calculate recommendations at runtime ... that would be costly and take a long time. Instead, this is a good use case for a batch process. We can stream the data into a data warehouse, the have a weekly batch process that munges all of these data, puts them into a model, and then outputs the recommendations from that model into a relational database, such as Cloud SQL. Then, at run time, all the application has to do is pull a value from the database, which it can do very quickly.

When should you use the following Cloud storage solutions?
* Cloud Storage - unstructured data
* Cloud SQL - good for data that is transactional, is on the gigabyte scale, and can be managed in one database.
* Datastore
* Bigtable - real-time high throughput applications
* BigQuery - petabyte scall analytics with seconds latency

## Zero to Apache Spark job in 10 minutes

* Cloud Dataproc!!
* Create a cluster (pretty simple GUI)
* Creat and submit a job (Hadoop/Spark)

Questions ... how can you spin up a Hadoop cluster and run hadoop jobs in Google Cloud?
* Cloud Dataproc! Go to Dataproc in Google cloud and spin up a Hadoop cluster in minutes. Then submit a job, wait for that job to complete, and then shut the cluster down. Clusters are ephemeral (designed to last for a short time), and shouldn't be used for storing data (use Cloud Storage for that).

What is Cloud Dataproc?
* It is GCP's managed Hadoop resources.

How and why is Cloud Dataproc ephemeral? What are the advantages of that?
* They are designed to be spun up when needed and shut down when not.
* This reduces cost as clusters are only used when needed so you only pay for what you need.
* This also prevents resource starvation, since you can easily spin up as many clusters as you need. If you are running 5 jobs one day, or 15 the next, there will be plenty of power for either.
* Clusters can auto-scale in size as long as data aren't stored on the HDFS (which it isn't designed to do).

Why do we want to store data off-cluster, instead of on a Dataproc Hadoop cluster?
* The future is separation of storage and compute!
* This increases the efficiency of your application/workflow. Because GCP's network is _so_ fast. We don't need to copy data from one location to another. Instead, it can live in one spot, and whatever compute resources (Dataproc, Compute Engine) can access it directly from its storage home.
* It allows us to shut down the cluster when we are done with our jobs.
* This allows for the cluster to autoscale to its compute needs.
* This allows for preemptive VMs (still don't understand these).

What type of off-cluster storage options are available?
* Cloud Storage
* Cloud Bigtable
* Cloud BigQuery

To dos (to cover in blogs):
- [ ] Create a cloud SQL instance
- [ ] Explain why we might want to use Cloud SQL instead of BigQuery
- [ ] Create cloud SQL tables
- [ ] Load data from cloud storage into Cloud SQL and BigQuery
- [ ] Run a PySpark jobs in Dataproc (spinning up and shutting down clusters when done)
- [ ] Put the PySpark output back into Cloud SQL or BigQuery.

## Lab -- recommendations using PySpark
1. Create a Cloud SQL instance
2. Connect using cloud shell and create tables
``` bash
# in cloud shell
gcloud sql connect rentals --user=root --quiet
```
``` sql
-- once the editor loads
CREATE DATABASE IF NOT EXISTS recommendation_spark;

USE recommendation_spark;

DROP TABLE IF EXISTS Recommendation;
DROP TABLE IF EXISTS Rating;
DROP TABLE IF EXISTS Accommodation;

CREATE TABLE IF NOT EXISTS Accommodation
(
  id varchar(255),
  title varchar(255),
  location varchar(255),
  price int,
  rooms int,
  rating float,
  type varchar(255),
  PRIMARY KEY (ID)
);

CREATE TABLE  IF NOT EXISTS Rating
(
  userId varchar(255),
  accoId varchar(255),
  rating int,
  PRIMARY KEY(accoId, userId),
  FOREIGN KEY (accoId)
    REFERENCES Accommodation(id)
);

CREATE TABLE  IF NOT EXISTS Recommendation
(
  userId varchar(255),
  accoId varchar(255),
  prediction float,
  PRIMARY KEY(userId, accoId),
  FOREIGN KEY (accoId)
    REFERENCES Accommodation(id)
);

SHOW DATABASES;
```
3. Create a CLoud Storage bucket and copy data
``` bash
echo "Creating bucket: gs://$DEVSHELL_PROJECT_ID"
gsutil mb gs://$DEVSHELL_PROJECT_ID

echo "Copying data to our storage from public dataset"
gsutil cp gs://cloud-training/bdml/v2.0/data/accommodation.csv gs://$DEVSHELL_PROJECT_ID
gsutil cp gs://cloud-training/bdml/v2.0/data/rating.csv gs://$DEVSHELL_PROJECT_ID

echo "Show the files in our bucket"
gsutil ls gs://$DEVSHELL_PROJECT_ID

echo "View some sample data"
gsutil cat gs://$DEVSHELL_PROJECT_ID/accommodation.csv
```
4. Load data from Cloud Storage into the Cloud SQL tables
* They use the GUI (using Import at the top), but I need to figure out how to do this with command line.
5. Explore the data using the Cloud SQL command prompt (in the cloud shell).
6. Launch Dataproc
- [ ] Create and spin down a cluster using the SDK.
* Find the IP addresses of the Dataproc cluster machines and give them access to the Cloud SQL instance.

7. Copy the ML model and set the CloudSQL IP address and password (in the python file)

8. Run the ML job on DataProc
* In the Dataproc menu click create job. Specify that it is a SparkML job, give it the Cloud Storage location (gs://{BUCKET}/train_and_apply.py), and submit the job!

9. Explore the recommendations!

Lab summary
In this lab, you:

Created a fully-managed Cloud SQL instance for rentals
Created tables and explored the schema with SQL
Ingested data from CSVs
Edited and ran a Spark ML job on Dataproc
Viewed prediction results

## 20210302

* BigQuery is two services in one, a data storage/warehouse solotion, and a fast SQL engine!
* Designed for geospatial analysis
* In the BigQuery web UI you can control click on the table in a query to take you to that table in the table/dataset explorer.
* In the web UI you can also select fields in the table preview and it will add them to that query.
* Cloud Dataprep for some basic statistics for your BigQuery data
* BigQuery has a scheduler!!
* Use BigQuery Query Engine on csv files in drive or somewhere else on the web.
* BigQuery arrays!!
* STRUCT data types
* GIS functions ... https://cloud.google.com/bigquery/docs/reference/standard-sql/geography_functions
* GLobal surface summary of the day (NOAA) and GFS model and HRR model. NOAA lightning strikes!
* BigQuery Geo Viz
* BigQuery ML! https://cloud.google.com/bigquery-ml/docs:
    * ETL
    * Preprocess
    * `create model`
    * `ml.evaluate`
    * `ml.weights` -- inspect what the model learned.
    * `ml.predict`

BQ ML cheatsheet:
* label - alias a column as `label` or specify columns in OPTIONS using `input_label_cols`
* feature - passed through to the model as part of the select statement
``` sql
select * from ml.feature_info(model {dataset}.{model_name})
```
* model - an object created inside the BQ dataset
* model types - e.g., linear or logistic regression
``` sql
create or replace model {dataset}.{model_name}
options(model_type='{type}') as 
<training_dataset>
```
* training progress - `select * from ml.training_info(model {dataset}.{model_name})`
* inspect weights - `select * from ml.weights(model {dataset}.{model_name}, (<query>))`
* evaluate
* predict