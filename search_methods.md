```
 ____                      _       __  __      _   _               _
/ ___|  ___  __ _ _ __ ___| |__   |  \/  | ___| |_| |__   ___   __| |___
\___ \ / _ \/ _` | '__/ __| '_ \  | |\/| |/ _ \ __| '_ \ / _ \ / _` / __|
 ___) |  __/ (_| | | | (__| | | | | |  | |  __/ |_| | | | (_) | (_| \__ \
|____/ \___|\__,_|_|  \___|_| |_| |_|  |_|\___|\__|_| |_|\___/ \__,_|___/
```
[**<- home**](./README.md)


# A simple choice
In DynamoDB you have three methods to fetch data:
- get item
- query
- scan


### Get Item

This method yields exactly one item (or none if there isn't a match). In order to perform this method, you must know the whole key whether it is a simple key or complex key. You then get the only item this applies to.


### Query

This method is only supported if a complex key is defined. You have to state the partition key you want, and then optionally define a comparison for the sort key such as less than, greater than or equal to, between, etc.


### Scan

This method just gets all the data out of your table, it is not elegant nor is it efficient (unless you do genuinely need _all_ the data).


# More choice!

You may also define a filter for the data, a filter can apply to any attribute not just the partition key and/or sort key. Something to be aware of is that your RCUs are calculated according to the volume of data returned by your search method, the filter is then applied after your search method meaning you are still charged for the data filtered out. The only benefit being that you do not have to filter the data yourself.


# Be careful!
Whenever you read a lot of data you need to be aware that DynamoDB will only give you the first 1Mb worth of data. In this event, it will also give you an `ExclusiveStartKey` which can can be fed back into the exact same query in order to return you the next 1Mb of data.
