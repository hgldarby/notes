# How to properly clean input data

- Filter out any OrderID's spanning over multiple days
- Filter any empty SKUID's or utilise the replace_missing_values() function in the prototypes widget.
- Filter out any products which are lighter than air or heavier than osmium. - Add this option in the filter widget - otherwise there will be a lot of searches for density of air
- Check in SKU master data that there are no duplicate SKUs
- Qty per day check if data is there