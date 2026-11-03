# Supply Chain & ESG analytics

An interactive Power BI dashboard that combines supply chain performance and environmental, social, and governance insights. Built from an Excel dataset containing 75,000 orders, 150 suppliers, and 800 products, it helps users monitor revenue, supplier ESG scores, carbon footprints, delivery delays, and defect rates.

## Report pages

- **Overview:** four KPIs and recent trends, supplier ESG versus shipping delay, monthly carbon emissions, the ten suppliers with the highest quantity-weighted defect rates, and delivery-delay history.
- **Geography:** a static offline world map showing full-dataset supplier-country coverage, plus interactive country revenue and exposure. The source has countries, not shipment routes or supplier-site coordinates.
- **Operations:** defect and delay histories, category revenue, and supplier-level operational performance.
- **Supplier history:** hidden report-page tooltip with the latest 12 months of weighted defect history.

Use Year, Country, and Risk dropdowns to filter each page. Select points or bars to cross-filter. In Desktop edit mode, use Ctrl+click on sidebar navigation buttons.

## Metric definitions

- Total revenue = sum of order quantity × related product sale price. The workbook supplies no currency; the report intentionally uses no currency symbol.
- Average ESG = unweighted average of scores for distinct suppliers with orders in the current filter context, on the source's 0–100 scale. ESG scores are supplier attributes; their trends show the mix of active suppliers, not historical score changes.
- Carbon footprint = sum of order quantity × related product Carbon_Footprint_kg, divided by 1,000 for tonnes. Assumes the product footprint represents kg per unit; this is product-associated carbon, not a separately measured shipment-emissions inventory.
- Critical suppliers = distinct suppliers with orders in the current context and source Risk_Rating exactly Critical. High is a separate category.
- Weighted defect rate = sum(quantity × DefectRate_Pct) / sum(quantity). Estimated defective units can be fractional because the source provides rates, not exact defect counts.
- Shipping delay = arithmetic average of ShippingDelay_Days across orders.
- Worst suppliers = descending weighted defect rate; supplier ID breaks ties, giving ten rows when at least ten suppliers are in scope.
- KPI sparklines use the 90 days ending at the latest date in the entire source dataset (31 October 2026). Filters can reduce the displayed history; filters outside this window yield no sparkline data.
- Supplier tooltip uses the latest 12 months ending at the same data date.

## Refresh and portability

Power Query currently refers to the copied workbook using this machine's absolute path. If you move this project, update the File.Contents paths in Transform data > Advanced Editor for Fact_Orders, Dim_Suppliers, and Dim_Products, then Refresh. To include later years beyond 2026, extend the Calendar end date and change the LatestDataYear filter on the four sparkline visuals. Refresh also picks up changes to source supplier and product attributes.

Measures.dax contains a readable copy of all model measures. Measures and relationships remain editable in Power BI Desktop.
