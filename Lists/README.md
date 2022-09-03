# Lists

## assign a list
```R
my_list <- list(a = c(1, 4, 2, 7),
                b = 555,
                c = "hello")
# get the whole list
my_list

# get the length of the list
length(my_list)
```
```cml
$a
[1] 1 4 2 7

$b
[1] 555

$c
[1] "hello"

[1] 3
```
## get the element in vector
```R
my_list[1]
```
```cml
$a
[1] 1 4 2 7
```
## change the element
```R
my_list[3] <- "pear"
my_list
```
```cml
$a
[1] 1 4 2 7

$b
[1] 555

$c
[1] "hello"
```

## add element into list
```R
my_list <- list(a = c(1, 4, 2, 7),
                b = 555,
                c = "hello")
vec = c(1, 2, 3)

my_list <- append(my_list, vec)

my_list <- append(my_list, "third", after = 2)

my_list
```
```cml
$a
[1] 1 4 2 7

$b
[1] 555

[[3]]
[1] "third"

$c
[1] "hello"

[[5]]
[1] 1

[[6]]
[1] 2

[[7]]
[1] 3
```

## remove element in list
```R
my_list <- list(a = c(1, 4, 2, 7),
                b = 555,
                c = "hello")
my_list <- my_list[-2]

my_list

```
```cml
$a
[1] 1 4 2 7

$c
[1] "hello"

```

## check if element exists
```R
fruits <- list("banana", "apple", "orange", "mango")

"apple" %in% fruits
```
```cml
[1] True
```
