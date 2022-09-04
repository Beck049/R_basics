# R_basics

[R_basics](https://github.com/Beck049/R_basics)
- Data Structure
  - [Vectors](https://github.com/Beck049/R_basics/tree/main/Vectors)
  - [Lists](https://github.com/Beck049/R_basics/tree/main/Lists)
  - [Matrix](https://github.com/Beck049/R_basics/tree/main/Matrix)
  - [Factor](https://github.com/Beck049/R_basics/tree/main/Factor)
  - [Dataframes](https://github.com/Beck049/R_basics/tree/main/Dataframes)
- Graphic
- Statistics
<br>

**Course**

- [week2](https://github.com/Beck049/R_basics/tree/main/week2)
  - [First Project](https://github.com/Beck049/R_basics/tree/main/week2/First_Project)
  - [DataExplorer](https://github.com/Beck049/R_basics/tree/main/week2/DataExplorer)
  - [Linear Regression](https://github.com/Beck049/R_basics/tree/main/week2/Linear_Regression)

## Data Types

### numeric
```R
# numeric
x <- 10.5
class(x)
x
```

```cml
[1] "numeric"
[1] 10.5
```

### integer
```R
# integer
x <- 1000L
class(x)
x
```
```cml
[1] "integer"
[1] 1000
```

### complex
```R
# complex
x <- 9i + 3
class(x)
x
```
```cml
[1] "complex"
[1] 3+9i
```

> **numeric** is for all types of real number <br>
> **integer** needs to add "L" in the end <br>
> **complex** is the imaginary number <br>

### character
```R
# character
x <- "its a string"
class(x)
x
```
```cml
[1] "character"
[1] "its a string"
```

### logical
```R
# logical
x <- TRUE
class(x)
x
```
```cml
[1] "logical"
[1] TRUE
```

### Array
```R
thisarray <- c(1:24)
thisarray

# An array with more than one dimension
multiarray <- array(thisarray, dim = c(4, 3, 2))
multiarray

multiarray[2, 3, 2]
```
```cml
 [1]  1  2  3  4  5  6  7  8  9 10 11 12 13 14 15 16 17 18 19 20 21 22 23 24
 
, , 1
     [,1] [,2] [,3]
[1,]    1    5    9
[2,]    2    6   10
[3,]    3    7   11
[4,]    4    8   12

, , 2
     [,1] [,2] [,3]
[1,]   13   17   21
[2,]   14   18   22
[3,]   15   19   23
[4,]   16   20   24

[1] 22
```

-----

## Operators

|number|description|examples|
|:---:|:---|:---:|
| + |  add  | 2 + 3 = 5 |
| - | minus | 5 - 4 = 1|
| * | times | 6 * 2 = 12|
| / | divide| 9 / 2 = 4.5|
| %%| modulus | 9 %% 2 = 1|
|%/%|divide in integer| 9 %/% 2 = 4|
| ^ |exponent|2 ^ 3 = 8|

|comparison|description|example|
|:---:|:---|:---:|
| == | Equal | x == y |
| != | Not Equal | x != y |
| > | Greater than | x > y |
| < | Less than | x < y |
| >= | Greater than or equal to | x >= y|
| <= | Less than or equal to | x <= y |

-----

## common functions

### math

**min() & max()**
```R
max(5, 10, 15)

min(5, 10, 15)
```
```cml
[1] 15
[1] 5
```

**sqrt()**
```R
sqrt(64)
```
```cml
[1] 8
```

**abs()**
```R
abs(-6.4)
```
```cml
[1] 6.4
```

**ceiling() & floor()**
```R
ceiling(9.4)

floor(9.4)
```
```cml
[1] 10
[1] 9
```

### character

```R
str <- "This is a string"

# lengh of a string
nchar(str)

# check substring
grepl("is", str)
grepl("srt", str)

# concat two string
paste(str, "or not ?")
```
```cml
[1] 16
[1] TRUE
[1] FALSE
[1] "This is a string or not ?"
```

## if else
```R
a <- 200
b <- 33

if (b > a) {
  print("b is greater than a")
} else if (a == b) {
  print("a and b are equal")
} else {
  print("a is greater than b")
}
```

## while loop

```R
i <- 1
cnt1 <- 0
while( i <= 6 ) {
  if( i == 4 ) {
    break
  }
  cnt <- cnt+1
  i <- i+1
}
cnt1
```
```cml
[1] 3
```

```R
i <- 1
cnt1 <- 0
while( i <= 6 ) {
  if( i == 4 ) {
    next
  }
  cnt <- cnt+1
  i <- i+1
}
cnt1
```
```cml
[1] 5
```
> break: stops the whole loop <br>
> next : immediatly go to the next loop

## for loop

```R
fruits <- list("apple", "banana", "cherry")

for(x in fruits) {
  print(x)
}
```
```cml
[1] "apple"
[1] "banana"
[1] "cherry"
```

## function

```R
my_func <- function(fn, ln) {
  paste(fn, ln)
}

my_func("Beck", "049")
```
```cml
[1] "Beck 049"
```
