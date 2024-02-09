
# Homework Week 3

## -- Creating external table referring to gcs path

CREATE OR REPLACE EXTERNAL TABLE `mystic-cable-406415.ny_taxi.external_green_tripdata`
OPTIONS (
  format = 'parquet',
  uris = ['gs://mage-zoomcamp-acalcines/green_taxi_2022.parquet']
);

## -- Create unpartion table

CREATE OR REPLACE TABLE `mystic-cable-406415.ny_taxi.green_tripdata`
AS SELECT * FROM `mystic-cable-406415.ny_taxi.external_green_tripdata`;

## -- Question 1

SELECT count(*) FROM `mystic-cable-406415.ny_taxi.green_tripdata`

## -- Question 2 

SELECT COUNT(DISTINCT(VendorID)) FROM `mystic-cable-406415.ny_taxi.external_green_tripdata`
SELECT COUNT(DISTINCT(VendorID)) FROM `mystic-cable-406415.ny_taxi.green_tripdata`

## -- Question 3

SELECT count(*) 

FROM `mystic-cable-406415.ny_taxi.green_tripdata`

WHERE fare_amount = 0 

## -- Question 4 Creating a partition and cluster table
CREATE OR REPLACE TABLE `mystic-cable-406415.ny_taxi.green_tripdata_partitoned_clustered`

PARTITION BY lpep_pickup_date

CLUSTER BY PUlocationID AS


SELECT * FROM `mystic-cable-406415.ny_taxi.green_tripdata`;

## --Question 5

SELECT DISTINCT PUlocationID

FROM `mystic-cable-406415.ny_taxi.green_tripdata`

WHERE lpep_pickup_date BETWEEN '2022-06-01' AND '2022-06-30'
  
SELECT DISTINCT PUlocationID

FROM `mystic-cable-406415.ny_taxi.green_tripdata_partitoned_clustered`

WHERE lpep_pickup_date BETWEEN '2022-06-01' AND '2022-06-30'
