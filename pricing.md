```
 ____       _      _
|  _ \ _ __(_) ___(_)_ __   __ _
| |_) | '__| |/ __| | '_ \ / _` |
|  __/| |  | | (__| | | | | (_| |
|_|   |_|  |_|\___|_|_| |_|\__, |
                           |___/
```
[**<- home**](./README.md)

# Honesty time

Look, I ain't usually the one paying the bills so I don't pay too much attention to this stuff. The only thing I do when it's my own project and I am paying the bills, is make sure it's free.

# Some tips

You get charged:
- **double rate** for transactional reading or writing
- **regular rate** for consistent reads
- **half rate** for eventually consistent reads
- per Gb if point in time recovery is enabled
- for reads on a Stream after the first 2.5 million read request units (a DynamoDB stream is a data stream that details all changes in your table)


# Be afraid (of on demand)... be very afraid


### on demand mode

In on demand mode, you are charged for each individual RCU or WCU. In `eu-west-2`, you are charged $0.7423 per million write request units and $0.1487 per million read request units. So if you read 100Gb of data in a month that should come out at:

```
100Gb of data is 12,500,000Kb
1 RCU is 4Kb per second
** Assuming our 100Gb is fully utilising each RCU
100Gb of data is 3,125,000 RCUs
3,125,000 @ $0.1487 per million RCUs = $0.4646875
```
**$0.4646875**
| Note |
|------|
| The first 1Gb is actually free in on demand mode |


### provisioned mode

In provisioned mode, you are charged for the RCUs and WCUs you provision regardless of whether or not you use them. In `eu-west-2` you are charged $0.000772 per WCU and $0.0001544 per RCU. So let's say you want to allow 100Gb of data to be read in a month, but only allow an even amount of reading between 9am and 5pm (so 8 hours of reading data every day for a month with totally even distribution, no spikes or anything like that). That should come out at:

```
8 hours is 28,800 seconds
365 days in a typical year divided by 12 months in a year gives an average of 30 (0dp) days a month.
With an 8 hour window per day, the average month yields 864,000 seconds per month.
100Gb of data is 12,500,000Kb
12,500,000Kb distributed evenly across 864,000 seconds gives 14.5 (1dp) Kbs per second.
1 RCU is 4Kb per second
Since AWS rounds up 14.5kb/s is 4 RCUs
** 4 RCUs is well within the free tier but we'll pretend there isn't a free tier.
4 RCUs of provisioned throughput @ $0.0001544 per RCU = $0.0006176
```
**$0.0006176**


### a comparison

In our 100Gb monthly read in on demand mode, we came up with a monthly cost of $0.4646875. So, let's just dump that money into provisioned mode and see what it can buy for us. Spending $0.4646875 on provisioned reading should get us:
```
$0.4646875 spent @ $0.0001544 per RCU = 3,009 RCUs (rounded down to the nearest whole RCU)
1 RCU is 4Kb per second
3,009 RCUs is 12,036Kb/s
If we impose the same 8 hours a day restriction we have 864,000 seconds in an average month
12,036Kb/s multiplied by 864,000 seconds gives 10,399,104,000Kb per month
10,399,104,000Kb is 83,193Gb
```
**83,193Gb**


### So what the hell should you use?

If you're not expecting gargantuan spikes of activity at completely unpredictable times, then just go for provisioned throughput and over estimate that by a good wide margin and it'll still be cheaper.

| Note |
|------|
| You can absolutely switch between provisioned and on demand as much as you like, so bear that approach in mind too. If you know you have unpredictable reads and or writes say at the beginning of the month, you can just switch to on demand for a day or two then switch it back. |
