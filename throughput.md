```
 _____ _                           _                 _
|_   _| |__  _ __ ___  _   _  __ _| |__  _ __  _   _| |_
  | | | '_ \| '__/ _ \| | | |/ _` | '_ \| '_ \| | | | __|
  | | | | | | | | (_) | |_| | (_| | | | | |_) | |_| | |_
  |_| |_| |_|_|  \___/ \__,_|\__, |_| |_| .__/ \__,_|\__|
                             |___/      |_|
```
[**<- home**](./README.md)

# Throughput modes

In DynamoDB you have two operating modes **on demand** and **provisioned**.


## Provisioned throughput

Provisioned throughput means that you are defining the rate at which reading and writing can take place, you define this in terms of read capacity units (RCUs) and write capacity units (WCUs). This is very handy when you are trying to keep DynamoDB free as you can ensure you do not exceed the 25 RCUs and WCUs allowed for free.


## On demand throughput

On demand throughput means that you are not posing any of your own restrictions on the ability to read or write to DynamoDB. This can get _very_ expensive.


# Capacity Units

- 1 RCU is defined as 4Kb of data read in one second.
- 1 WCU is defined as 1Kb of data written in one second.

Capacity units are always rounded up. If you read only 0.5 Kb of data in a second, that is still 1 RCU. If you write only 1 byte of data in a second, that is still 1 WCU.
