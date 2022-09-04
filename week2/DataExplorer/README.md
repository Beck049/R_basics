# Data Exploration
```r
library(DataExplorer)
```

## Plot Bar
```r
plot_bar(fb)
```

## Histogram
```r
plot_histogram(fb)
```

## Missing Value
```r
fb$missing <- fb$Total_Conversion/fb$Clicks
plot_missing(fb)
```

## Correlation
```r
plot_correlation(fb[,c("age","gender","Clicks","Impressions","Spent","Total_Conversion","Approved_Conversion")])
```
