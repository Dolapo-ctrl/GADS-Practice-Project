#LAB
Google Cloud Fundamentals: Getting Started with BigQuery
#OBJECTIVES
In this lab, you learn how to perform the following tasks:



- Load data from Cloud Storage into BigQuery.



- Perform a query on the data in BigQuery.

##STEPS
1 . **Load data from Cloud Storage into BigQuery**




- Using the console,Create a new dataset within your project by selecting your project in the Resources section, then clicking on CREATE DATASET on the right.



- In the Create Dataset dialog, for Dataset ID, type logdata.



- For Data location, select the continent closest to the region your project was created in. Run the code below to create dataset.


		bq --location "US" mk --dataset "logdata" 

- Create a new table in the logdata to store the data from the CSV file.

		bq mk --external_table_definition "gs://cloud-training/gcpfci/access_log.csv" logdata.accesslog

- (Optional) To track job progress, click Job History.

		bq show -j qwiklabs-gcp-04-f6138d93aa92

- View logdata > accesslog

		bq show logdata.accesslog	



**2 .  **Perform a query on the data using the BigQuery web UI****

In this section of the lab, you use the BigQuery web UI to query the accesslog table you created previously.

- Because you told BigQuery to automatically discover the schema when you load the data, the hour of the day during which each web hit arrived is in a field called int_field_6. Run the following code:

		bq query "select int64_field_6 as hour, count(*) as hitcount from logdata.accesslog group by hour order by hour"

	Notice that the Query Validator tells you that the query syntax is valid (indicated by the green check mark) and indicates how much data the query will process. The amount of data processed allows you to determine the price of the query using the


**3 . Perform a query on the data using the bq command**


In this section of the lab, you use the bq command in Cloud Shell to query the accesslog table you created previously.

- At the Cloud Shell prompt, enter this command:

		bq query "select string_field_10 as request, count(*) as requestcount from logdata.accesslog group by request order by requestcount desc"

	The first time you use the bq command, it caches your Google Cloud Platform credentials, and then asks you to choose your default project. Choose the project that Qwiklabs assigned you to. Its name will look like qwiklabs-gcp- followed by a hexadecimal number.

	The bq command then performs the action requested on its command line. 


**Congratulations!**

In this lab, you loaded data stored in Cloud Storage into a table hosted by Google BigQuery. You then queried the data to discover patterns.

**End your lab**









