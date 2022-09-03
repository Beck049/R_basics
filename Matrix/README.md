# Matrix

## assign a list
```R
thismatrix <- matrix(c(1,2,3,4,5,6), nrow = 3, ncol = 2)
thismatrix
```
```cml
     [,1] [,2]
[1,]    1    4
[2,]    2    5
[3,]    3    6
```

## get the element from matrix
access a cell
```R
thismatrix <- matrix(c(1,2,3,4,5,6), nrow = 3, ncol = 2)

thismatrix[1, 2]
```
```cml
[1] "cherry"
```
access a row
```R
thismatrix <- matrix(c(1,2,3,4,5,6), nrow = 3, ncol = 2)

thismatrix[2,]
```
```cml
[1] 2 5
```
access a column
```R
thismatrix <- matrix(c(1,2,3,4,5,6), nrow = 3, ncol = 2)

thismatrix[, 2]
```
```cml
[1] 4 5 6
```

## add col & row name
```R
netmat <- rbind(c(0,1,1,0,0),  c(0,0,1,1,0), c(0,1,0,0,0),  c(0,0,0,0,0),  c(0,0,1,0,0))
rownames(netmat) <- c("A","B","C","D","E") 
colnames(netmat) <- c("A","B","C","D","E")
```
```cml
  A B C D E
A 0 1 1 0 0
B 0 0 1 1 0
C 0 1 0 0 0
D 0 0 0 0 0
E 0 0 1 0 0
```

-----

## add a row or column
```R
thismatrix <- matrix(c("apple", "banana", "cherry", "orange","grape", "pineapple", "pear", "melon", "fig"), nrow = 3, ncol = 3)
thismatrix
```
```cml
     [,1]     [,2]        [,3]   
[1,] "apple"  "orange"    "pear" 
[2,] "banana" "grape"     "melon"
[3,] "cherry" "pineapple" "fig"
```
add a column
```R
newmatrix <- cbind(thismatrix, c("strawberry", "blueberry", "raspberry"))
newmatrix
```
```cml
     [,1]     [,2]        [,3]    [,4]        
[1,] "apple"  "orange"    "pear"  "strawberry"
[2,] "banana" "grape"     "melon" "blueberry" 
[3,] "cherry" "pineapple" "fig"   "raspberry"
```
add a row
```R
newmatrix <- rbind(thismatrix, c("strawberry", "blueberry", "raspberry"))
newmatrix
```
```cml
[1,] "apple"      "orange"    "pear"     
[2,] "banana"     "grape"     "melon"    
[3,] "cherry"     "pineapple" "fig"      
[4,] "strawberry" "blueberry" "raspberry"
```

## remove a row or column
remove a row
```R
newmatrix <- thismatrix[-c(1),]
newmatrix
```
```cml
     [,1]     [,2]        [,3]   
[1,] "banana" "grape"     "melon"
[2,] "cherry" "pineapple" "fig"  
```
remove a column
```R
newmatrix <- thismatrix[, -c(2)]
newmatrix
```
```cml
     [,1]     [,2]   
[1,] "apple"  "pear" 
[2,] "banana" "melon"
[3,] "cherry" "fig" 
```

## size of the matrix
```R
dim(thismatrix)

length(thismatrix)
```
```cml
[1] 3 3
[1] 9
```

## loop through the matrix
```R
for (rows in 1:nrow(thismatrix)) {
  for (columns in 1:ncol(thismatrix)) {
    print(thismatrix[rows, columns])
  }
}
```

## combine two matrix
```R
# Combine matrices
Matrix1 <- matrix(c("apple", "banana", "cherry", "grape"), nrow = 2, ncol = 2)
Matrix2 <- matrix(c("orange", "mango", "pineapple", "watermelon"), nrow = 2, ncol = 2)

# Adding it as a rows
Matrix_Combined_r <- rbind(Matrix1, Matrix2)
Matrix_Combined_r

# Adding it as a columns
Matrix_Combined_c <- cbind(Matrix1, Matrix2)
Matrix_Combined_c
```
