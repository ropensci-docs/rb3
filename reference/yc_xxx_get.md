# Retrieve Yield Curve Data

These functions retrieve yield curve data, either for all available
curves (`yc_get`) or specifically for:

- the nominal rates curve (`yc_brl_get`).

- the nominal rates curve for USD in Brazil - Cupom Cambial Limpo
  (`yc_usd_get`).

- the real rates curve (`yc_ipca_get`).

## Usage

``` r
yc_get()

yc_brl_get()

yc_ipca_get()

yc_usd_get()
```

## Value

An `arrow_dplyr_query` or `ArrowObject`, representing a lazily evaluated
query. The underlying data is not collected until explicitly requested,
allowing efficient manipulation of large datasets without immediate
memory usage. To trigger evaluation and return the results as an R
`tibble`, use `collect()`.

The returned data includes the following columns:

- `curve_name`: Identifier of the yield curve (e.g., "PRE", "DOC",
  "DIC").

- `refdate`: Reference date of the curve.

- `forward_date`: Maturity date associated with the interest rate.

- `biz_days`: Number of business days between `refdate` and
  `forward_date`.

- `cur_days`: Number of calendar days between `refdate` and
  `forward_date`.

- `r_252`: Annualized interest rate based on 252 business days.

- `r_360`: Annualized interest rate based on 360 calendar days.

## Details

The yield curve data is downloaded from the B3 website
<https://www2.bmf.com.br/pages/portal/bmfbovespa/lumis/lum-taxas-referenciais-bmf-ptBR.asp>.
See the Curve Manual in this link
<https://www.b3.com.br/data/files/8B/F5/11/68/5391F61043E561F6AC094EA8/Manual_de_Curvas.pdf>
for more details.

## Examples

``` r
if (FALSE) { # \dontrun{
df <- yc_get() |>
  filter(curve_name == "PRE") |>
  collect()
} # }
if (FALSE) { # \dontrun{
df_yc <- yc_brl_get() |>
  filter(refdate == Sys.Date()) |>
  collect()
head(df_yc)
} # }
if (FALSE) { # \dontrun{
df_yc_ipca <- yc_ipca_get() |>
  filter(refdate == Sys.Date()) |>
  collect()
head(df_yc_ipca)
} # }
if (FALSE) { # \dontrun{
df_yc_usd <- yc_usd_get() |>
  filter(refdate == Sys.Date()) |>
  collect()
head(df_yc_usd)
} # }
```
