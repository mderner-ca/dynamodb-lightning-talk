```
 _____                      
|_   _|   _ _ __   ___  ___ 
  | || | | | '_ \ / _ \/ __|
  | || |_| | |_) |  __/\__ \
  |_| \__, | .__/ \___||___/
      |___/|_|  
```
[**<- home**](./README.md)




## Basic types

You've got some basic fundamental types in DynamoDB.

| Type | Description |
|------|-------------|
| String | |
| Number | Number is always represented by some Decimal type like `Decimal` in Python or `BigDecimal` in Ruby or Java |
| Boolean | |
| Null | Represented by things like `None` in Python or `nil` in Ruby |

## Composite types 

You can build upon your basic types with these composite types. A lot of composite types support storing other composite types up to a max depth of 32.

| Type | Description |
|------|-------------|
| List | A list can be a mix of any types, no homogeny required |
| Map | This is your basic hashmap or in Python it'd be a `dict` in Ruby it'd be a `Hash`. Maps have string keys and whatever you're feeling values. |
| Set | A set is just a list where all the data types are the same, you're allowed number sets, string sets, and binary sets (a binary set can store booleans and nulls) |
