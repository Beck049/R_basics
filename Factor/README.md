# Factor

## assign a factor
```R
blood=c("O","AB","A","B","B","A","O")
blood
blood_factor=factor(blood)
blood_factor
```
```cml
[1] "O"  "AB" "A"  "B"  "B"  "A"  "O" 
[1] O  AB A  B  B  A  O 
Levels: A AB B O
```
> the **factor** has meta data of the not repeating data

## what is really in a factor
```R
str(blood_factor)
```
```cml
Factor w/ 4 levels "A","AB","B","O": 4 2 1 3 3 1 4
```

## get the element
```R
blood[2]
blood[3]
blood[4]

blood_factor[2]
blood_factor[3]
blood_factor[4]
```
```cml
[1] "AB"
[1] "A"
[1] "B"

[1] AB
Levels: A AB B O
[1] A
Levels: A AB B O
[1] B
Levels: A AB B O
```
> blood & blood_factor actually points to the same object <br>
> but represent in "character" type or "factor" type

## get not repeating data
```R
blood=c("O","AB","A","B","B","A","O") #character
blood_factor=factor(blood)

blood_lvl = levels(blood_factor)
blood_lvl
```
```cml
[1] "A"  "AB" "B"  "O" 
```
> blood_lvl is actually a "vector" type
