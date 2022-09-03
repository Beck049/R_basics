# Vectors

## assign a vector
```R
fruits <- c("banana", "apple", "orange", "mango", "lemon")

# get the length of the vector
length(fruits)

# get the whole vector
fruits

# get the element in vector
fruits[3]

# sort
sort(fruits)

# change the element
fruits[5] <- "pear"
fruits
```
```cml
[1] 5
[1] "banana" "apple" "orange" "mango" "orange"
[1] "orange"
[1] "apple" "banana" "lemon" "mango" "orange"
[1]"banana" "apple" "orange" "mango" "pear"
```

## Repeat Vector
```R
repeat_each <- rep(c(1,2,3), each = 3)

repeat_each
```
```cml
[1] 1 1 1 2 2 2 3 3 3
```
```R
repeat_times <- rep(c(1,2,3), times = 3)

repeat_times
```
```cml
[1] 1 2 3 1 2 3 1 2 3
```
```R
repeat_indepent <- rep(c(1,2,3), times = c(5,2,1))

repeat_indepent
```
```cml
[1] 1 1 1 1 1 2 2 3
```
```R
numbers <- seq(from = 0, to = 100, by = 20)

numbers
```
```cml
[1]   0  20  40  60  80 100
```
