# Lists

## assign a list
```R
fruits <- c("banana", "apple", "orange", "mango")

# get the length of the vector
length(fruits)

# get the whole vector
fruits

# get the element in vector
fruits[3]

# change the element
fruits[3] <- "pear"
fruits

# add element into list
append(fruits, "cherry")
fruits
append(fruits, "melon", after = 2)
fruits
```
```cml
[1] 4
[1] "banana" "apple" "orange" "mango"
[1] "orange"
[1] "banana" "apple" "pear" "mango"
[1] "banana" "apple" "pear" "mango" "cherry"
```
