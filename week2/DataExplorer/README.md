# Data Exploration
```r
library(DataExplorer)
```

## Plot Bar
```r
plot_bar(fb)
```

![](https://github.com/Beck049/R_basics/tree/main/week2/DataExplorer/plot_bar.png)

## Histogram
```r
plot_histogram(fb)
```

![](https://github.com/Beck049/R_basics/tree/main/week2/DataExplorer/histogram.png)

## Missing Value
```r
fb$missing <- fb$Total_Conversion/fb$Clicks
plot_missing(fb)
```

![](https://github.com/Beck049/R_basics/tree/main/week2/DataExplorer/missing.png)

## Correlation
```r
plot_correlation(fb[,c("age","gender","Clicks","Impressions","Spent","Total_Conversion","Approved_Conversion")])
```

![](https://github.com/Beck049/R_basics/tree/main/week2/DataExplorer/correlation.png)
