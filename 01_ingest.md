# 01_ingest

In this lab, we will ingest data from an S3 Bucket into Impala Tables using Hue. 

In a pattern that we will release shortly, we will use Cloudera Data Flow (CDF) to ingest data from numerous other sources. 

The primary goal of this is to build an ingestion data pipeline.
- Source data is pre-loaded in an S3 Bucket in CSV format. There are 5 datasets that we need to ingest into Impala.
    - Flights data
    - Airports data
    - Planes data
    - Airlines data
    - Passenger data
- We connect to the source bucket and pull all 5 datasets and ingest into the CDP Data warehouse (Impala in this case) for further analysis in [Analyze](02_analyze.md) phase.

## Lab 1: Ingest Flights data needed for Prediction

- In this lab, we will ingest **Flights data** from a source S3 Bucket into Impala Data warehouse. 
- Note that this is a large dataset and it will take a few minutes to ingest this data. 
- With just Flights data, we can continue to Prediction (As part of Lab 2, we will ingest the remaining tables that is needed for Analyze and Visualize).

1. In your CDP Home Page, click on **Data Hub Clusters**. (For more information about Data Hub, here is a [product tour](https://www.cloudera.com/products/data-hub/cdp-tour-data-hub.html))

![Screen_Shot_2023_04_23_at_2_27_29_PM.png](images/Screen_Shot_2023_04_23_at_2_27_29_PM.png)

2. In the Data Hub Clusters landing page - 

   a. **Note the Environment Name** as it will be used as one of the inputs while we create tables
   
   b. Click on the Data Hub called **dwarehouse**. 

![Screenshot_2023_05_31_at_5_13_05_PM.png](images/Screenshot_2023_05_31_at_5_13_05_PM.png)

3. In the list of Services in the Data Hub, click on **Hue** to access Impala.

![Screenshot_2023_05_31_at_5_13_36_PM.png](images/Screenshot_2023_05_31_at_5_13_36_PM.png)

4. You will be taken to Impala Editor. Create a database called **airlines** using the below query - 

```
create database airlines;
```

5. Create tables needed for further analysis, visualization and prediction

   a. We start with **flights** table

```
drop table if exists airlines.flights;

CREATE EXTERNAL TABLE airlines.flights (month int, dayofmonth int, dayofweek int, deptime int, crsdeptime int, arrtime int, crsarrtime int, uniquecarrier string, flightnum int, tailnum string, actualelapsedtime int, crselapsedtime int, airtime int, arrdelay int, depdelay int, origin string, dest string, distance int, taxiin int, taxiout int, cancelled int, cancellationcode string, diverted string, carrierdelay int, weatherdelay int, nasdelay int, securitydelay int, lateaircraftdelay int, year int)
ROW FORMAT DELIMITED FIELDS TERMINATED BY ',' LINES TERMINATED BY '\n'
STORED AS TEXTFILE LOCATION 's3a://${cdp_environment_name}/trial-odlh-data/airline-demo-data/flights' tblproperties("skip.header.line.count"="1");

```

* In **cdp_environment_name** field, enter the environment name you captured earlier

6. Query the newly created table, execute the below query - 

```
select count(*) from airlines.flights;
```

![Screenshot20230531at52523PM.png](images/Screenshot20230531at52523PM.png)

13. From here, you can go to Lab 2 to ingest the remaining files or you can head to [lab around Predict](04_predict.md) to build an end-to-end machine learning project using Cloudera Machine Learning

## Lab 2: Create other Tables needed for Analysis and Visualization

1. Similar to how airlines.flights was created, we will create other tables with data pre-loaded in S3.
2. 
3. In airlines database, click + to go to "Import to table" screen.

![Screenshot20230601at65527AM.png](images/Screenshot20230601at65527AM.png)

3. Keeping _Remote File_ as Type, click **..** in the Path. 
4. Select S3 and if you are not in the same folder as before(airline-demo-data), **Change path to s3a://<environment_name>/trial-odlh-data/airline-demo-data/**.

5. Select **airlines.csv**. The file will be parsed and the appropriate columns will be identified. 
6. Ensure that "Field Separator" is Comma(,) and "Has Header" is selected. Click Next.

![Screenshot20230601at70407AM.png](images/Screenshot20230601at70407AM.png)

7. In the Next Screen, verify that the Destination Name is **airlines.airlines**. 
8. Click Submit. 
9. Query the newly loaded table, execute the below query - 

```
select count(*) from airlines.airlines;
```

10. Similar to how airlines.csv was uploaded, we will upload other csv files present in **s3a://<environment_name>/trial-odlh-data/airline-demo-data/**.
11. Select each of the below files to create appropriate tables
    - airports.csv
    - planes.csv
    - unique_tickets.csv
12. Ensure that "Field Separator" is Comma(,) and "Has Header" is selected.
13. In the Next Screen, verify that the Destination Name is **airlines.<table_name>**.
14. Each of these files have a few 1000 records and import will happen in minutes.

We are now ready to [Analyze](02_analyze.md), [Visualize](03_visualize.md) and [Predict](04_predict.md) Data!
