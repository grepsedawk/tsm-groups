# Grepsedawk's Sniper String (Beta)

This sniper string is based off of BilisOnyxia's very popular sniper string, but rather than having hard
price brackets, it applies a smooth curve to the values.

<img alt="Graph of Grepsedawk's Price String vs BilisOnyxia's Sniper String" src=/images/sniper-graph.png width=50%/>

## Custom Sources (Required!)

It requires the same `minprice` custom source as BilisOnyxia's string which is as follows: 

```tsm
max(min(dbhistorical, dbregionmarketavg, dbregionhistorical), vendorsell)
```

## Sniper String

```tsm
ifgte(itemquality, 1, ifgte(minprice, 1000g, minprice * min(5 * (minprice / 10000) ^ (0.22), 80) / 100, 0c), 0c)
```

It takes all non-grey items that have a `minprice` > 1000g and applies the curve as pictured in the graph with a ceiling of 80% minprice
