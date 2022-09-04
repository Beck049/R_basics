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

------

## Summary the Data_Frame

### add column to data_frame
```r
# add a column directly
fb$CTR = (fb$Clicks / fb$Impressions) * 100 
fb$CPC = fb$Spent / fb$Clicks 

head(fb)
```
```cml
   ad_id xyz_campaign_id fb_campaign_id   age gender interest Impressions  Clicks Spent Total_Conversion Approved_Conversion         CTR   CPC 
1 708746             916         103916 30-34      M       15        7350       1  1.43                2                   1   0.01360544 1.43
2 708749             916         103917 30-34      M       16       17861       2  1.82                2                   0   0.01119758 0.91
3 708771             916         103920 30-34      M       20         693       0  0.00                1                   0   0.00000000  NaN
4 708815             916         103928 30-34      M       28        4259       1  1.25                1                   0   0.02347969 1.25
5 708818             916         103928 30-34      M       28        4133       1  1.29                1                   1   0.02419550 1.29 
6 708820             916         103929 30-34      M       29        1915       0  0.00                1                   1   0.00000000  NaN 
```
> we can find out that `CRT`, `CPC` are automatically added into `fb` <br>
> > `CTR`: Clicks per Impression <br>
> > `CPC`: Cost per Click <br>

> why there're `NaN` in CPC <br>
> if the `Click` value is `0`, divide 0 will cause `NaN`, which means **Not-a-Number**

#### what if we want to change `NaN` to 0, since click is 0, then CPC is 0
```r
fb$CPC = ifelse( fb$Clicks != 0, fb$Spent / fb$Clicks, 0 )

head(fb)
```
`CPC` is now changed
```cml
   ad_id xyz_campaign_id fb_campaign_id   age gender interest Impressions  Clicks Spent Total_Conversion Approved_Conversion         CTR   CPC 
1 708746             916         103916 30-34      M       15        7350       1  1.43                2                   1   0.01360544 1.43
2 708749             916         103917 30-34      M       16       17861       2  1.82                2                   0   0.01119758 0.91
3 708771             916         103920 30-34      M       20         693       0  0.00                1                   0   0.00000000    0
4 708815             916         103928 30-34      M       28        4259       1  1.25                1                   0   0.02347969 1.25
5 708818             916         103928 30-34      M       28        4133       1  1.29                1                   1   0.02419550 1.29 
6 708820             916         103929 30-34      M       29        1915       0  0.00                1                   1   0.00000000    0 
```

### calculate some values
now we have values `CTR`, `CPC`
we can summarise the data by calculating maximun, mean, etc...

```r
mean(fb$CTR)
```
```cml
[1] 0.01641967
```

### make multiple value into table
```r
ctr_cal <- summarise(fb, CTR_mean = mean(CTR)
            , CTR_median = median(CTR)
            , CTR_max = max(CTR)
            , CTR_min = min(CTR))
            
ctr_cal
```
```cml
 CTR_mean     CTR_median    CTR_max     CTR_min
 0.01641967	  0.0159809	    0.1059322	    0	
```
> `summary()` needs `dplyr` library

### What else can we do
|method|code|description|
|:---:|:---:|:---|
|mean|mean(x)||
|median|median(x)||
|sum|sum(x)||
|standard deviation|sd(x)||
|interquartile|IQR(x)||
|maximum|max(x)||
|minimun|min(x)||
|quantile|quantile(x)||
|first observation|first(x)||
|last observation|last(x)||
|nth observation|nth(x, n)||
|number of occurrence|n(x)||
|number of distinct occurrence|n_distinct(x)||

------

## make a table

### examine the non-repetitive values
check the non-repetitive values, usually used in `character` or `farctor` data type
```r
unique(fb$gender)
unique(fb$age)
```
```cml
[1] "M" "F"
[1] "30-34" "35-39" "40-44" "45-49"
```

### categorize the data
How many Male/Female and the age range
```r
table(fb$age, fb$gender)
```
```cml
          F   M
  30-34 197 229
  35-39 109 139
  40-44 107 103
  45-49 138 121
```
it's easy, but what if we want "M" at the first row
and change the "M" label into "Male"...
```r
uni_gen <- unique(fb$gender)
fb$gender_factor=factor(fb$gender,
                        levels=uni_gen, 
                        labels = c("Male", "Female"))
str(fb$gender_factor)
table(fb$age, fb$gender_factor)
```
```cml
Factor w/ 2 levels "Male","Female": 1 1 1 1 1 1 1 1 1 1 ...

        Male Female
  30-34  229    197
  35-39  139    109
  40-44  103    107
  45-49  121    138
```
> we'll need `factors` <br>
> `levels` = the value in data_frame <br>
> `labels` = the display value corresponding to `levels` <br>
> > always remember to check `factor` by using `str()` <br>

------



[DataExplorer]
