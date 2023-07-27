# Iceberg Capabilites 

In this lab, we will test some cool features of Iceberg in Impala including In-place Table Evolution features, Time Travel, ACID etc.

## Lab 1: Ingest data 

1. In your CDP Home Page, click on **Data Hub Clusters**. (For more information about Data Hub, here is a [product tour](https://www.cloudera.com/products/data-hub/cdp-tour-data-hub.html))

![Screen_Shot_2023_04_23_at_2_27_29_PM.png](images/Screen_Shot_2023_04_23_at_2_27_29_PM.png)

2. In the Data Hub Clusters landing page - 

   a. **Note the Environment Name** as it will be used as one of the inputs while we create tables
   
   b. Click on the Data Hub called **dwarehouse**. 

![Screenshot_2023_05_31_at_5_13_05_PM.png](images/Screenshot_2023_05_31_at_5_13_05_PM.png)

3. In the list of Services in the Data Hub, click on **Hue** to access Impala.

![Screenshot_2023_05_31_at_5_13_36_PM.png](images/Screenshot_2023_05_31_at_5_13_36_PM.png)

4. You will be taken to Impala Editor. Create a database called **airlines** and **airlines_csv** using the below query - 

```
CREATE DATABASE airlines;
CREATE DATABASE airlines_csv;
```

5. Create **flights** table

```

drop table if exists airlines_csv.flights_csv;

CREATE EXTERNAL TABLE airlines_csv.flights_csv (month int, dayofmonth int, dayofweek int, deptime int, crsdeptime int, arrtime int, crsarrtime int, uniquecarrier string, flightnum int, tailnum string, actualelapsedtime int, crselapsedtime int, airtime int, arrdelay int, depdelay int, origin string, dest string, distance int, taxiin int, taxiout int, cancelled int, cancellationcode string, diverted string, carrierdelay int, weatherdelay int, nasdelay int, securitydelay int, lateaircraftdelay int, year int)
ROW FORMAT DELIMITED FIELDS TERMINATED BY ',' LINES TERMINATED BY '\n'
STORED AS TEXTFILE LOCATION 's3a://${cdp_environment_name}/trial-odlh-data/airline-demo-data/flights' tblproperties("skip.header.line.count"="1");

```

* In **cdp_environment_name** field, enter the environment name you captured earlier
