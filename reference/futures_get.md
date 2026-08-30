# Retrieves B3 Futures Settlement Prices

This function fetches settlement price data for B3 futures contracts.
This function retrieves futures settlement prices from the B3 dataset,
adding a `symbol` column that combines `commodity` and `maturity_code`.

## Usage

``` r
futures_get()
```

## Source

[B3 Market
Data](https://www.b3.com.br/en_us/market-data-and-indices/data-services/market-data/historical-data/derivatives/trading-session-settlements/)

## Value

An `arrow_dplyr_query` or `ArrowObject`, representing a lazily evaluated
query. The underlying data is not collected until explicitly requested,
allowing efficient manipulation of large datasets without immediate
memory usage. To trigger evaluation and return the results as an R
`tibble`, use `collect()`.

The returned data includes the following columns:

- `refdate`: Reference date for the prices.

- `symbol`: Futures contract symbol, created by concatenating the
  commodity code and the maturity code.

- `commodity`: Commodity code of the futures contract.

- `maturity_code`: Maturity code of the futures contract.

- `previous_price`: Closing price from the previous trading day.

- `price`: Current price of the futures contract.

- `price_change`: Price variation compared to the previous day.

- `settlement_value`: Settlement value of the futures contract.

## Examples

``` r
if (FALSE) { # \dontrun{
df_fut <- futures_get() |> filter(refdate == Sys.Date()) |> collect()
head(df_fut)
} # }
```
