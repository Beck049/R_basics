# Sentiment Analysis

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

