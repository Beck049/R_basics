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
import the data, and we use `head()` to examine some data
```r
#import data
fb = read.csv("Facebook_conversion_data.csv")
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

also use `str()` to see the details
```r
str(fb)
```
```cml
'data.frame':   1143 obs. of  11 variables:
 $ ad_id              : int  708746 708749 708771 708815 708818 708820 708889 708895 
708953 708958 ...
 $ xyz_campaign_id    : int  916 916 916 916 916 916 916 916 916 916 ...
 $ fb_campaign_id     : int  103916 103917 103920 103928 103928 103929 103940 103941 
103951 103952 ...
 $ age                : Factor w/ 4 levels "30-34","35-39",..: 1 1 1 1 1 1 1 1 1 1 ...
 $ gender             : Factor w/ 2 levels "F","M": 2 2 2 2 2 2 2 2 2 2 ...
 $ interest           : int  15 16 20 28 28 29 15 16 27 28 ...
 $ Impressions        : int  7350 17861 693 4259 4133 1915 15615 10951 2355 9502 ... 
 $ Clicks             : int  1 2 0 1 1 0 3 1 1 3 ...
 $ Spent              : num  1.43 1.82 0 1.25 1.29 ...
 $ Total_Conversion   : int  2 2 1 1 1 1 1 1 1 1 ...
 $ Approved_Conversion: int  1 0 0 0 1 1 0 1 0 0 ...
```
> we can see the data_type of every column <br>

## add column to data_frame
```r
# add a column directly
fb$CTR = (fb$Clicks / fb$Impressions) * 100 
fb$CPC = fb$Spent / fb$Clicks 

head(fb)
```
```cml
```
> we can find out that `CRT`, `CPC` are automatically added into `fb`
> > CTR: Clicks per Impression
> > CPC: Cost per Click
