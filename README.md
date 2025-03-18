```
 ____                                    ____  ____
|  _ \ _   _ _ __   __ _ _ __ ___   ___ |  _ \| __ )
| | | | | | | '_ \ / _` | '_ ` _ \ / _ \| | | |  _ \
| |_| | |_| | | | | (_| | | | | | | (_) | |_| | |_) |
|____/ \__, |_| |_|\__,_|_| |_| |_|\___/|____/|____/
       |___/
```

# What?

DynamoDB is a noSQL database provided by AWS. It is the **_only_** forever free database solution provided by AWS (at time of writing 2025-03-17), everything else has a free trial just long enough that it's too difficult to migrate off of right before you're hit with massive costs. Anecdotally, I had a friend doing some AWS learning and she switched on RDS (the main AWS SQL solution) for a little bit, no real data, no real queries, and it cost her £30 that month.

DynamoDB is free as long as you:
- store less than 20Gb of data (more complex to count than first thought)
- provision for 25 or less Read Capacity Units (RCUs) and Write Capacity Units (WCUs)

| Note |
|------|
| This is not _per table_ this is for **_all tables in your account_** |


# Terms

A source of data is called a **table** much as it is in other database services, a table contains many **items** (not records), and an item consists of one of more **attributes** (not fields). The initial table you create is known as the "base table".

# Contents
- [Keys](./keys.md)
- [Indexes](./indexes.md)
- [Throughput](./throughput.md)
- [Search Methods](./search_methods.md)
- [Pricing](./pricing.md)
- [Further Reading](./refs.md)