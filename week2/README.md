# First Project

use Facebook_conversions.csv to do some analyze

## Packages

first, we should install some useful packages
```r
install.packages("tidyverse")
install.packages("dplyr")
install.packages("ggplot2")
install.packages("DataExplorer")
```

then load the library
```r
library(tidyverse)
library(dplyr)
library(ggplot2)
library(DataExplorer)
```

## Import Data
```r
#import data
fb=read.csv("Facebook_conversion_data.csv")
head(fb)
```
```cml
   ad_id xyz_campaign_id fb_campaign_id   age gender interest Impressions  Clicks Spent Total_Conversion Approved_Conversion
1 708746             916         103916 30-34      M       15        7350       1  1.43                2                   1
2 708749             916         103917 30-34      M       16       17861       2  1.82                2                   0
3 708771             916         103920 30-34      M       20         693       0  0.00                1                   0
4 708815             916         103928 30-34      M       28        4259       1  1.25                1                   0
5 708818             916         103928 30-34      M       28        4133       1  1.29                1                   1
6 708820             916         103929 30-34      M       29        1915       0  0.00                1                   1
```

