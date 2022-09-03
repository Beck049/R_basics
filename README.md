# R_basics

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

> **numeric** is for all types of real number
> **integer** needs to add "L" in the end 
> **complex** is the imaginary number

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

## Operators

|numeric|description|examples|
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

