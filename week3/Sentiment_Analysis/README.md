# Sentiment Analysis
1. how to get data from twitter using Twitter API
2. create a .rds file
3. read a .rds file
4. use function `get_nrc_sentiment()`

## packages
```r
library(rtweet) # this package collects tweet data
library(dplyr)  # we will use the filter function from this package
library(syuzhet) # this package performs sentiment analysis
library(DataExplorer)
```

## Authentication (Twitter)
```r
twitter_tokens <- 
  create_token(app = "S326",
               consumer_key = "Z9yJu2xgTrcTqCHJvOkn8vz6E",
               consumer_secret = "H9IySsPPZE5GbjdSJYNyzprS80LfvXuuOTCOLSu0IjkpCUW2zo"
               access_token = NULL,
               access_secret = NULL,
               set_renv = TRUE
              )
```
|||
|:---:|:---|
|**app**.           | Name of the user created Twitter application |
|**consumer_key**   | Application API key |
|**consumer_secret**| Application API secret User-owned application must have `Read and write` access level and `Callback URL` of `http://127.0.0.1:1410` |
|**access_token**   | Access token as supplied by Twitter |
|**access_secret**  | Access secret as supplied by Twitter |
|**set_renv**       | TRUE, is to save token as ".rtweet_token.rds" to home directory |

## Create .rds file
```r
climate_tweets <- search_tweets("climate change", n = 200, includes_rts = FALSE)
saveRDS(climate_tweets, file = "climate_tweets.rds")
```

## Read .rds file
```r
climate_tweets <- readRDS( file = "climate_tweets.rds" )
```

## Generate a subset of dataframe
create sub dataframe, 
with values: 
||||||
|---|---|---|---|---|
|status_id|screen_name|text|source|display_text_width|
|reply_to_status_id|is_quote|is_retweet|favorite_count||
```r
sub_climate_tweets=climate_tweets[,c("status_id","screen_name","text","source","display_text_width","reply_to_status_id","is_quote","is_retweet","favorite_count")]

head(sub_climate_tweets)
```
```cml
status_id           screen_name     text                source displ…¹ reply…² is_qu…³ is_re…⁴ favor…⁵
  <chr>               <chr>           <chr>               <chr>    <dbl> <chr>   <lgl>   <lgl>     <int>
1 1566875699000090624 PatDevl27789617 "Always thought th… Twitt…      96 NA      TRUE    FALSE         0
2 1566875685972475912 Schawn          "@ISASaxonists @Ve… Twitt…      27 156687… FALSE   FALSE         0
3 1566875672898838533 sallymclain1    "@Mollyploofkins N… Twitt…      86 156674… FALSE   FALSE         0
4 1566875647602999297 Spultinate      "@guy_courier @k_m… Twitt…      17 156685… FALSE   FALSE         0
5 1566875616997253120 DisciplePOV     "Given this unbeli… Twitt…     234 NA      TRUE    FALSE         0
6 1566875558642057216 rjohnson_ca     "A portion of the … Twitt…     271 NA      FALSE   FALSE         0
```

## Explore Dataframe
- what is the data type for status_id?
- what is the data type for text?
- what is the data type for is_tweet?
```r
str(sub_climate_tweets) # shows detail of the dataframe
```
```cml
tibble [200 × 9] (S3: tbl_df/tbl/data.frame)
 $ status_id         : chr [1:200] "1566875699000090624" "1566875685972475912" "1566875672898838533" "1566875647602999297" ...
 $ screen_name       : chr [1:200] "PatDevl27789617" "Schawn" "sallymclain1" "Spultinate" ...
 $ text              : chr [1:200] "Always thought this. Free energy for cars doesn’t make a profit much nor promote climate change. https://t.co/7sO4H3Ryk5" "@ISASaxonists @VeronicaSixsmi1 Climate change hahahahahaha" "@Mollyploofkins No, more worried about climate change. It's killing more, and costing more than Trump." "@guy_courier @k_monty22 Climate change 👀😳" ...
 $ source            : chr [1:200] "Twitter Web App" "Twitter for iPhone" "Twitter for Android" "Twitter for Android" ...
 $ display_text_width: num [1:200] 96 27 86 17 234 271 108 212 279 74 ...
 $ reply_to_status_id: chr [1:200] NA "1566873282808356871" "1566749854566588417" "1566851567520710658" ...
 $ is_quote          : logi [1:200] TRUE FALSE FALSE FALSE TRUE FALSE ...
 $ is_retweet        : logi [1:200] FALSE FALSE FALSE FALSE FALSE FALSE ...
 $ favorite_count    : int [1:200] 0 0 0 0 0 0 0 0 0 0 ...
```
> status_id: chr (string) <br>
> text: chr (string) <br>
> is_tweet: logi (boolean) <br>

- what source types are available? (unique())
```r
# show all unique values (elimnates the duplicate values)
unique(sub_climate_tweets$source)
```
```cml
 [1] "Twitter Web App"          
 [2] "Twitter for iPhone"       
 [3] "Twitter for Android"      
 [4] "Hootsuite Inc."           
 [5] "Sprout Social"            
 [6] "CoSchedule"               
 [7] "Global Citizen Mobile App"
 [8] "TweetDeck"                
 [9] "Buffer"                   
[10] "Cheap Bots, Done Quick!"  
[11] "TweetDeck Web App"        
[12] "IFTTT"                    
[13] "Tweetbot for iΟS"         
[14] "SocialFlow"               
[15] "Twitter for iPad" 
```
- is source type a nominal or ordinal categorical variable?
```r
table(sub_climate_tweets$source)
```
```cml
                   Buffer   Cheap Bots, Done Quick!                CoSchedule Global Citizen Mobile App 
                        1                         2                         1                         2 
           Hootsuite Inc.                     IFTTT                SocialFlow             Sprout Social 
                        1                         1                         1                         1 
         Tweetbot for iΟS                 TweetDeck         TweetDeck Web App       Twitter for Android 
                        1                         1                         1                        47 
         Twitter for iPad        Twitter for iPhone           Twitter Web App 
                        4                        70                        66 
```

## Visualize
- plot_bar()
```r
plot_bar(sub_climate_tweets)
```
- plot_histogram()
```r
plot_histogram(sub_climate_tweets)
```
- plot_missing()
```r
plot_missing(sub_climate_tweets)
```
- plot_correlation()
```r
plot_correlation(sub_climate_tweets)
```

## Summarise the data
- what is the mean, median, max, sd(standard deviation) of favorite_count?
```r
sum_cli <- summarise(sub_climate_tweets, 
                     cli_mean = mean(favorite_count),
                     cli_median = median(favorite_count),
                     cli_max = max(favorite_count),
                     cli_sd = sd(favorite_count))

sum_cli
```
```cml
# A tibble: 1 × 4
  cli_mean   cli_median   cli_max    cli_sd
     <dbl>        <dbl>     <int>     <dbl>
1     1.23            0        92      7.48
```

- follow the question, what if group_by criteria "is_quote"

## Sentiment
use `get_nrc_sentiment()` to generate sentiment score
```r
tweets=climate_tweets$text
sentiment <- get_nrc_sentiment(tweets)

head(sentiment)
```
```cml
  anger  anticipation  disgust   fear   joy  sadness  surprise  trust  negative  positive
1     0             1        0      1     0        0         0      0         0         0
2     0             0        0      1     0        0         0      0         0         0
3     1             0        0      2     0        2         1      0         2         0
4     0             0        0      1     0        0         0      1         0         0
5     1             1        1      4     0        2         0      1         3         2
6     0             0        0      1     0        1         1      0         2         0
```
### visualize in bar plot
```r
barplot(colSums(sentiment),   # this is the value for every bar, 
                              # colSums is a function to calculate the sum of each column
        las = 2,   # make label text perpendicular to axis
        col = rainbow(10),
        ylab = 'Count',
        main = 'Sentiment Scores Tweets'
        )
```

## Linear Regression about how sentiment affect favor_count

1. bind sentiment & favorite_count as favorite
```r
combined=cbind(sentiment,favorite=climate_tweets$favorite_count) 
#we add a label 'favorite' for data favorite_count
#function cbind combines the columns
head(combined)
```
```cml
    anger anticipation  disgust   fear  joy  sadness surprise   trust negative positive favorite
1       0            1        0      1    0        0        0       0        0        0        0
2       0            0        0      1    0        0        0       0        0        0        0
3       1            0        0      2    0        2        1       0        2        0        0
4       0            0        0      1    0        0        0       1        0        0        0
5       1            1        1      4    0        2        0       1        3        2        0
6       0            0        0      1    0        1        1       0        2        0        0
```
2. do linear regression 
let `favorite` be dependent
and `others` be independent
```r
relation=lm(Favorite ~ anger + anticipation + disgust + fear + joy + sadness + surprise + trust + negative + positive, data=combined)
summary(relation)
```
```cml
Call:
lm(formula = favorite ~ anger + anticipation + disgust + fear + 
    joy + sadness + surprise + trust + negative + positive, data = combined)

Residuals:
   Min     1Q Median     3Q    Max 
-7.268 -1.498 -0.935  0.333 85.263 

Coefficients:
             Estimate Std. Error t value Pr(>|t|)  
(Intercept)    1.4950     1.1088   1.348   0.1792  
anger         -1.1386     1.0208  -1.115   0.2661  
anticipation  -0.4714     0.9765  -0.483   0.6299  
disgust       -0.6662     1.1180  -0.596   0.5520  
fear          -0.2122     0.9133  -0.232   0.8166  
joy            0.0552     1.3269   0.042   0.9669  
sadness       -1.0059     1.0072  -0.999   0.3192  
surprise       2.6538     1.0835   2.449   0.0152 *
trust          0.0186     0.7951   0.023   0.9814  
negative       0.8918     0.7726   1.154   0.2498  
positive      -0.3477     0.5180  -0.671   0.5029  
---
Signif. codes:  0 ‘***’ 0.001 ‘**’ 0.01 ‘*’ 0.05 ‘.’ 0.1 ‘ ’ 1

Residual standard error: 7.468 on 189 degrees of freedom
Multiple R-squared:  0.05296,	Adjusted R-squared:  0.002848 
F-statistic: 1.057 on 10 and 189 DF,  p-value: 0.3979
```

3. Interprete the result
```r
```

