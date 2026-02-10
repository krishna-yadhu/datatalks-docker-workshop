--BigQuery Queries--

CREATE OR REPLACE EXTERNAL TABLE `zoom-camp-test.zoomcamp.yellow_trip_2024_ext`
OPTIONS(
  FORMAT= 'PARQUET',
  uris = ['gs://krishna-zoomcamp-kestra/yellow_tripdata_2024-*.parquet']
);


CREATE OR REPLACE TABLE zoom-camp-test.zoomcamp.yellow_trip_2024_int AS
SELECT * FROM zoom-camp-test.zoomcamp.yellow_trip_2024_ext;


SELECT count(*)
FROM `zoomcamp.yellow_trip_2024_ext`;

SELECT count(passenger_count) 
FROM zoomcamp.yellow_trip_2024_ext;

SELECT count(passenger_count) 
FROM zoomcamp.yellow_trip_2024_int;

SELECT PULocationID
FROM zoomcamp.yellow_trip_2024_int;

SELECT PULocationID,DOLocationID
FROM zoomcamp.yellow_trip_2024_int;

SELECT count(fare_amount)
FROM `zoomcamp.yellow_trip_2024_int`
WHERE fare_amount = 0;

CREATE OR REPLACE TABLE zoom-camp-test.zoomcamp.yellow_trip_2024_int_partitioned_clustered
PARTITION BY
  DATE(tpep_dropoff_datetime) 
CLUSTER BY VendorID  AS
SELECT * FROM zoom-camp-test.zoomcamp.yellow_trip_2024_int;

SELECT DISTINCT(VendorID) 
FROM zoom-camp-test.zoomcamp.yellow_trip_2024_int_partitioned_clustered
WHERE tpep_dropoff_datetime BETWEEN '2024-03-01' and '2024-03-15';

SELECT DISTINCT(VendorID) 
FROM zoom-camp-test.zoomcamp.yellow_trip_2024_int
WHERE tpep_dropoff_datetime BETWEEN '2024-03-01' and '2024-03-15';


SELECT *
FROM zoom-camp-test.zoomcamp.yellow_trip_2024_int;
