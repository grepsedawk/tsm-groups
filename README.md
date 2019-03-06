# Grepsedawk's TSM Groups (Beta)

These are my TSM groups. They are split so you can pick and choose which groups you want and so the import goes smoothly.

## Installation/Import

1. Create a new profile (Optional)
1. (If you are using the attached operation) Add `normalmarket` Custom Source via `/tsm` -> Settings -> Custom Sources:

    ```tsm
    max(min(dbmarket, 125%dbregionmarketavg), 85%dbregionmarketavg)
    ```

1. Copy the entire contents of any .tsm file and paste into "Import/Export" -> Import

## Contributing

Due to the single-line nature of TSM strings, it is very hard to see the difference between 2 TSM strings. For this reason I will not be accepting any PRs to any .tsm files.

If I missing an item, you have an issue, I leave my mailing operation on the group, etc [make an issue here](https://github.com/grepsedawk/tsm-groups/issues/new).

## How My Transmog Operation Works

### normalmarket Custom Source

```tsm
max(min(dbmarket, 125%dbregionmarketavg), 85%dbregionmarketavg)
```

`normalmarket` is a custom source in which normalizes your realm's `dbmarket` against `regionmarketavg`. It allows some flexibility under and over the region average, but the "base" price will never be <85% region avg and they will never fluctuate >125%. Keeping the value above 85% region keeps you from undervaluing items based on your realm's dbmarket prices, which can be very volitile. The high cap prevents prices from "running" too high, since our normal price is higher than dbmarket.

On the graph, the red line shows the region value while the blue lines show the low and high thresholds for `dbmarket`.

<img alt="Normalmarket Range based on Region Market Value" src=images/normalmarket_graph.png width=50%/>

### Shopping (Experimental)

The shopping is a very simple operation in which looks for any transmog that you do not yet have listed, banked, or on alts that is 10% the "normalmarket" price in which has a "normalmarket" of 5k or higher.

```tsm
iflt(normalmarket, 5000g, 0c,  10% normalmarket)
```

### Transmog Operation Explained

The auctioning operation is smart and tries to get the best value. The minimum price is aggressive but is smart to back off at lower values. The normal price and maximum price keep a reasonable hold on runaway prices whilst allowing your realm to slide above region avg.

#### Minimum Price

```tsm
max(110% AvgBuy / 0.95, iflt(normalmarket, 1000g, 50% normalmarket, normalmarket * min(max((normalmarket - 5000g)*(85 - 50)/(50000g - 5000g) + 50, 50), 85) / 100))
```

The minimum price is based off of [Sheyrah's Operations](https://www.reddit.com/r/woweconomy/comments/93hcpw/sheyrahs_transmog_operation_explained/) with the modification of using `normalmarket` as the price source.

It won't allow you to sell below 110% avgbuy to prevent you from losing money on a sale.
If an item's normalmarket is 5k then it will allow the minimum price to fall no lower than 50% the normalmarket price.
If an item's normalmarket is 50k then it will allow the minimum price to fall no lower than 85% the normalmarket price.
The pricing is a linear equation, draw a line from (5k,50%) and (50k,85%). It gets increasingly more aggressive as the item is more valuable.

If there's an auction below minimum then we post at max price.


#### Normal Price

```tsm
185% normalmarket
```



#### Max Price

```tsm
300% normalmarket
```

We post at max price if auctions are below minimum to force a soft reset. With time it balances the avg to creep upward. If your competitors lapse on posting and undercutting each other, they will sometimes undercut this agressive price, allowing you to undercut and make a sale at a larger profit resulting in a massive reset without paying more than a few extra deposits and patience.

I set a max price of 300% normalmarket because anything higher than this will probably not sell until the price is lowered. If somebody else is posting above max and that is the lowest auction, I simply post at my max price.
