# normalmarket Custom Source

```tsm
max(min(dbmarket, 125%dbregionmarketavg), 85%dbregionmarketavg)
```

`normalmarket` is a custom source in which normalizes your realm's `dbmarket` against `regionmarketavg`.
It allows some flexibility under and over the region average, but the "base" price will never be
<85% region avg and they will never fluctuate >125%. Keeping the value above 85% region keeps you
from undervaluing items based on your realm's dbmarket prices, which can be very volitile. The high
cap prevents prices from "running" too high, since our normal price is higher than dbmarket.

On the graph, the red line shows the region value while the blue lines show the low and high thresholds for `dbmarket`.

<img alt="Normalmarket Range based on Region Market Value" src=/images/normalmarket_graph.png width=50%/>
