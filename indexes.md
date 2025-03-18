```
 ___           _
|_ _|_ __   __| | _____  _____  ___
 | || '_ \ / _` |/ _ \ \/ / _ \/ __|
 | || | | | (_| |  __/>  <  __/\__ \
|___|_| |_|\__,_|\___/_/\_\___||___/
```
[**<- home**](./README.md)

# What?

Indexes are a way of changing how you query your data. Rather than using the defined partition key and/or sort key of your base table, you may define a new partition key and/or sort key within an index. When defining an index you also define the projection, the projection defines which attributes are present in the index.

# Local Secondary Index

A Local Secondary Index (LSI) is where you define a new sort key, the partition key however remains the same as your base table. Obviously, if you only have a simple key defined you may not create an LSI as there is no sort key defined in the base table.  
LSIs support consistent reads, when consistent reads are used the data is always up-to-date with the base table.

# Global Secondary Index

A Global Secondary Index (GSI) is where you define a new partition key, and optionally a new sort key. GSIs are essentially a new table, so if you project every attribute from your base table into your GSI and your base table contains 10Gb of data, you are now storing 20Gbs of data in total. For this reason if you are trying to keep DynamoDB free, you need to keep an eye on your GSIs.  
Since GSIs are separate tables, they have their own provisioned throughput
