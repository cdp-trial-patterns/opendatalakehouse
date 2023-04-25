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
5. Go inside the airlines database and click **+** to create a table by importing from a CSV file

![Screen_Shot_2023_04_23_at_2_35_16_PM.png](images/Screen_Shot_2023_04_23_at_2_35_16_PM.png)

6. You will be taken to **Import to table** screen. Keeping _Remote File_ as Type, click **..** in the Path. 
7. Select S3 and you will see file path as s3a://<environment_name>/user/<user_name>. **Change path to s3a://<environment_name>/data**.

Source files have been pre-loaded to the S3 folder, _data_

![Screen_Shot_2023_04_23_at_2_36_50_PM.png](images/Screen_Shot_2023_04_23_at_2_36_50_PM.png)

8. Select **flights.csv**. The file will be parsed and the appropriate columns will be identified. 
9. Ensure that "Field Separator" is Comma(,) and "Has Header" is selected.

![Screen_Shot_2023_04_23_at_2_52_46_PM.png](images/Screen_Shot_2023_04_23_at_2_52_46_PM.png)


