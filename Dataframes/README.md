# Dataframe

## assign a dataframe
```R
Data_Frame <- data.frame (
  Training = c("Strength", "Stamina", "Other"),
  Pulse = c(100, 150, 120),
  Duration = c(60, 30, 45)
)

Data_Frame
summary(Data_Frame)
```
```cml
  Training Pulse Duration
1 Strength   100       60
2  Stamina   150       30
3    Other   120       45

     Training     Pulse          Duration   
 Other   :1   Min.   :100.0   Min.   :30.0  
 Stamina :1   1st Qu.:110.0   1st Qu.:37.5  
 Strength:1   Median :120.0   Median :45.0  
              Mean   :123.3   Mean   :45.0  
              3rd Qu.:135.0   3rd Qu.:52.5  
              Max.   :150.0   Max.   :60.0
```


## get the element from dataframe
```R
Data_Frame[1]

Data_Frame[["Training"]]

Data_Frame$Pulse
```
```cml
  Training
1 Strength
2  Stamina
3    Other

[1] Strength Stamina  Other   
Levels: Other Stamina Strength

[1] 100 150 120
```
## add col & row name
add rows
```R
New_row_DF <- rbind(Data_Frame, c("Strength", 110, 110))

New_row_DF
```
```cml
  Training Pulse Duration
1 Strength   100       60
2  Stamina   150       30
3    Other   120       45
4 Strength   110      110
```

add columns
```R
New_col_DF <- cbind(Data_Frame, Steps = c(1000, 6000, 2000))

New_col_DF
```
```cml
  Training Pulse Duration Steps
1 Strength   100       60  1000
2  Stamina   150       30  6000
3    Other   120       45  2000
```

## remove col & row name
```R
Data_Frame <- data.frame (
  Training = c("Strength", "Stamina", "Other"),
  Pulse = c(100, 150, 120),
  Duration = c(60, 30, 45)
)

Data_Frame_New <- Data_Frame[-c(2), -c(2)]

Data_Frame_New
```
```cml
  Training Duration
1 Strength       60
3    Other       45
```

## size of the dataframe
```R
dim(Data_Frame)

ncol(Data_Frame)
nrow(Data_Frame)

length(Data_Frame)
```
```cml
[1] 3 3
[1] 3
[1] 3
[1] 3
```
> `length()` is similar to `ncol()`

## combine two dataframes
rbind
```R
Data_Frame1 <- data.frame (
  Training = c("Strength", "Stamina", "Other"),
  Pulse = c(100, 150, 120),
  Duration = c(60, 30, 45)
)

Data_Frame2 <- data.frame (
  Training = c("Stamina", "Stamina", "Strength"),
  Pulse = c(140, 150, 160),
  Duration = c(30, 30, 20)
)

New_Data_Frame <- rbind(Data_Frame1, Data_Frame2)
New_Data_Frame
```
```cml
  Training Pulse Duration
1 Strength   100       60
2  Stamina   150       30
3    Other   120       45
4  Stamina   140       30
5  Stamina   150       30
6 Strength   160       20
```
cbind
```R
Data_Frame3 <- data.frame (
  Training = c("Strength", "Stamina", "Other"),
  Pulse = c(100, 150, 120),
  Duration = c(60, 30, 45)
)

Data_Frame4 <- data.frame (
  Steps = c(3000, 6000, 2000),
  Calories = c(300, 400, 300)
)

New_Data_Frame1 <- cbind(Data_Frame3, Data_Frame4)
New_Data_Frame1
```
```cml
  Training Pulse Duration Steps Calories
1 Strength   100       60  3000      300
2  Stamina   150       30  6000      400
3    Other   120       45  2000      300
```
