# 01_ingest

In this lab, we will ingest data from an S3 Bucket into Hive Tables using Hue. 

In a pattern that we will release shortly, we will use Cloudera Data Flow (CDF) to ingest data from numerous other sources. 

The primary goal of this is to build an ingestion data pipeline.
- Source data is pre-loaded in an S3 Bucket in CSV format. There are 5 datasets that we need to ingest into Hive.
    - Flights data
    - Airports data
    - Planes data
    - Airlines data
    - Passenger data
- We connect to the source bucket and pull all 5 datasets and ingest into the CDP Data warehouse (Hive in this case) for further analysis in [Analyze](02_analyze.md) phase.

## Lab 1: Ingest Flights data needed for Prediction

- In this lab, we will ingest **Flights data** from a source S3 Bucket into Hive Data warehouse. 
- Note that this is a large dataset and it will take a few minutes to ingest this data. 
- With just Flights data, we can continue to Prediction (As part of Lab 2, we will ingest the remaining tables that is needed for Analyze and Visualize).

1. In your CDP Home Page, click on **Data Hub Clusters**. (For more information about Data Hub, here is a [product tour](https://www.cloudera.com/products/data-hub/cdp-tour-data-hub.html))

![Screen_Shot_2023_04_23_at_2_27_29_PM.png](images/Screen_Shot_2023_04_23_at_2_27_29_PM.png)

2. In the Data Hub Clusters landing page, click on the Data Hub called **dataengg**. 

![Screen_Shot_2023_04_23_at_2_28_05_PM.png](images/Screen_Shot_2023_04_23_at_2_28_05_PM.png)

3. In the list of Services in the Data Hub, click on **Hue** to access Hive.

![Screen_Shot_2023_04_23_at_2_28_36_PM.png](images/Screen_Shot_2023_04_23_at_2_28_36_PM.png)

4. You will be taken to Hive Editor. Create a database called **airlines** using the below query - 

```
create database airlines;
```


