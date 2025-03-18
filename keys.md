```
 _  __
| |/ /___ _   _ ___
| ' // _ \ | | / __|
| . \  __/ |_| \__ \
|_|\_\___|\__, |___/
          |___/
```
[**<- home**](./README.md)

# The two types of key setup

You have two options for keys, you can have a **_simple key_** or a **_complex key_**.


## Simple Key

With a simple key configuration, you only define your **partition key**. The partition key is an attribute for which the value much be unique amongst all items within your table.  
When you fetch an item in DynamoDB, the partition key is hashed and that gives direct access to the item you are trying to find, giving super quick linear time lookups. Obviously this means you cannot do comparative operations against the partition key.


## Complex key

With a complex key configuration, you not only define your **partition key** you also define a **sort key**. Both the partition and sort keys - when put together - must yield a value that is unique amongst all items within your table. So you can have items with identical partition keys, as long as they all have different sort keys, and you can have items that all have the same sort key, as long as their partition keys are different.  
All items that share a partition key are stored within the same partition and they are sorted by their sort key, this is important to remember when designing your DynamoDB table.  
When you fetch an item in DynamoDB, the partition key is hashed in the same way as it is for a simple key and this gives linear time look up to that partition, then a binary search tree is employed to find the correct sort key value. Due to the way items are stored in a partition, you can do comparative searches for the sort key (i.e. "this exact partition key and a sort key value greater than this").

| Note |
|------|
| The partition key and sort key you define in the base table are the only required attributes on an item. |