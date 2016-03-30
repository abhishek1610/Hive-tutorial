# Hive-tutorial - WIP

Hive is a datawarehousing layer above Hadoop. It gives SQl like semantics over Hadoop data(HDFS). Although now many SQl engine over hadoop like Impala,Drill,Presto has come but Hive was the original SQL engine on top of Hadoop.

Sample create table in Hive -
CREATE TABLE IF NOT EXISTS employee ( empid int, name String, salary String, destination String) COMMENT ‘Employee details’ ROW FORMAT DELIMITED FIELDS TERMINATED BY ‘\t’ LINES TERMINATED BY ‘\n’ STORED AS TEXTFILE;

Exp - the row format delimited mentions how the data in HDFS will be. In this case it will be tab delimited. Each row will be delimited by new line(\n). Currently, this delimiter can not be set to anything else but newline.

TextFile is basic format of Hive/HDFS.Later we will look into Avro and Parquet format which is gaining lot of popularity.

Inserting data into table
LOAD DATA INPATH 'usr\emp' INTO employee

Exp- It will load the data present in HDFS path usr\emp into the table that was created.

External table - CREATE EXTERNAL TABLE employee ( empid int, name String, salary String, destination String ) ROW FORMAT DELIMITED FIELDS TERMINATED BY '\t' LOCATION '/usr/emp';
This will create an exernal table in Hive. It similar to internal table just that location needs to be specified. A differnce between internal and external table is that when a internal table is dropped the full table along with data is deleted.

Storage formats - Hive supports various tsorage formats other than textfile mentioned above - a. Sequence file - CREATE TABLE IF NOT EXISTS employee ( empid int, name String, salary String, destination String) COMMENT ‘Employee details’ ROW FORMAT DELIMITED FIELDS TERMINATED BY ‘\t’ LINES TERMINATED BY ‘\n’ STORED AS SEQUENCEFILE;
Stores data as sequence file in hadoop which is kind of binary form.

b. RC- Row cloumnar

CREATE TABLE sample ( column1 STRING, column2 STRING, column3 INT, column4 INT ) STORED AS RCFILE;

It offers below advantage --

(1) Fast data storing, (2) Improved query processing, (3) Optimized storage space utilization

c. ORC - Optimized Row columnar

CREATE TABLE sample ( column1 STRING, column2 STRING, column3 INT, column4 INT ) STORED AS ORCFILE;

The ORC File (Optimized Row Columnar) format provides a more efficient way to store relational data than the RC File, reducing the data storage format of the original. The ORC file format performs better than other Hive files formats when Hive is reading, writing, and processing data
