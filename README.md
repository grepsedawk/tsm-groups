# Grepsedawk's TSM Groups

These are my TSM groups. They are split so you can pick and choose which groups you want and so the import goes smoothly.

## Installation/Import

1. Create a new profile (Optional)
1. (If you are using the attached operation) Add [normalmarket](/docs/custom_sources/normalmarket.md) Custom Source via `/tsm` -> Settings -> Custom Sources:

    ```tsm
    max(min(dbmarket, 125%dbregionmarketavg), 85%dbregionmarketavg)
    ```

1. Copy the entire contents of any .tsm file and paste into "Import/Export" -> Import

## Contributing

Due to the single-line nature of TSM strings, it is very hard to see the difference between 2 TSM strings. For this reason I will not be accepting any PRs to any .tsm files.

If I missing an item, you have an issue, I leave my mailing operation on the group, etc [make an issue here](https://github.com/grepsedawk/tsm-groups/issues/new).

## Groups

[Trasnmog with Operations](/transmog.tsm)

[Recipes with Operations](/recipes.tsm)

[Mats with Operations](/mats.tsm)

## Operation Explanations

[Transmog](/docs/operations/transmog.md)
