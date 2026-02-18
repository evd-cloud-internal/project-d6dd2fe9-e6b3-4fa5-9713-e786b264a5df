---
name: Home
assetId: 2ea455ae-b2b4-4f4f-a553-54fc4c552255
type: page
---

# Demo Sales Dashboard

{% big_value
    data="demo_daily_orders"
    value="sum(total_sales)"
    fmt="usd0m"
    title="Total Sales"
    sparkline={
        type="area"
        x="date"
        date_grain="month"
    }
/%}

{% big_value
    data="demo_daily_orders"
    value="sum(transactions)"
    fmt="#,##0"
    title="Total Orders"
    sparkline={
        type="area"
        x="date"
        date_grain="month"
    }
/%}

{% big_value
    data="demo_daily_orders"
    value="avg(avg_transaction_value)"
    fmt="usd2"
    title="Avg Transaction Value"
/%}

## Sales Trends

{% line_chart
    data="demo_daily_orders"
    x="date"
    y="sum(total_sales)"
    series="category"
    y_fmt="usd0m"
    date_grain="month"
    title="Monthly Sales by Category"
/%}

## Category Breakdown

{% bar_chart
    data="demo_daily_orders"
    x="category"
    y="sum(total_sales)"
    y_fmt="usd0m"
    order="sum(total_sales) desc"
    title="Total Sales by Category"
/%}

## Yearly Performance

{% bar_chart
    data="demo_daily_orders"
    x="date"
    y="sum(total_sales)"
    series="category"
    y_fmt="usd0m"
    date_grain="year"
    title="Annual Sales by Category"
/%}

## Seasonality

{% bar_chart
    data="demo_daily_orders"
    x="date"
    y="sum(total_sales)"
    y_fmt="usd0m"
    date_grain="month of year"
    title="Sales by Month of Year"
    subtitle="Aggregated across all years"
/%}

## Sales Detail

{% table
    data="demo_daily_orders"
    title="Sales by Category & Year"
%}
    {% dimension
        value="category"
    /%}
    {% pivot
        value="date"
        date_grain="year"
    /%}
    {% measure
        value="sum(total_sales)"
        fmt="usd1m"
        viz="bar"
    /%}
    {% measure
        value="sum(transactions)"
        fmt="#,##0"
    /%}
{% /table %}