# Data Exploration
```r
library(DataExplorer)
```

## Plot Bar
```r
plot_bar(fb)
```
<img src="https://github.com/Beck049/R_basics/tree/main/week2/DataExplorer/plot_bar.png" width="50%">

## Histogram
```r
plot_histogram(fb)
```
<img src="https://github.com/Beck049/R_basics/tree/main/week2/DataExplorer/histogram.png" width="50%">

## Missing Value
```r
fb$missing <- fb$Total_Conversion/fb$Clicks
plot_missing(fb)
```
<img src="https://github.com/Beck049/R_basics/tree/main/week2/DataExplorer/missing.png" width="50%">

## Correlation
```r
plot_correlation(fb[,c("age","gender","Clicks","Impressions","Spent","Total_Conversion","Approved_Conversion")])
```
<img src="https://github.com/Beck049/R_basics/tree/main/week2/DataExplorer/correlation.png" width="50%">
