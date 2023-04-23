# 01_ingest

In this lab, we will ingest data from an S3 Bucket into Hive Tables using Hue. In an upcoming pattern, we will use Cloudera Data Flow (CDF) to ingest data from numerous other sources. 

The primary goal of this is to build an ingestion data pipeline.

- Source data is pre-loaded in an S3 Bucket in CSV format. There are 5 datasets that we need to ingest into Hive.
    - Flights data
    - Airports data
    - Planes data
    - Airlines data
    - Passenger data
- We connect to the source bucket and pull all 5 datasets and ingest into the CDP Data warehouse (Hive in this case) for further analysis in ![02_analyze](02_analyze.md)
