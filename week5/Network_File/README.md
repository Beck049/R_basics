# Network_File


## Read File into Network
```r
fb <- read.csv(file = 'facebook_data.csv') 
net=network(fb,matrix.type="edgelist",loops=TRUE)
```

## Centrality Measures
```r
#In-Degree and Out-Degree 
InDegree <- degree(net, cmode="indegree")     #Computing the in-degree of each node
#set.vertex.attribute(net, "InDegree", InDegree)
OutDegree <- degree(net, cmode="outdegree")   #Computing the out-degree of each node
#set.vertex.attribute(net, "OutDegree", OutDegree)
Closeness <- closeness(net,  cmode="directed")
#set.vertex.attribute(net, "Closeness", Closeness)
Betweenness <- betweenness(net, cmode="directed") 
#set.vertex.attribute(net, "Betweenness", Betweenness)
Egenvector <- evcent(net)
#Sset.vertex.attribute(net, "Egenvector", Egenvector)
#will have to change the cmode from directed to undirected if we are doing undirected 
```

### Combine the attributes above
```r
facebook_centrality <- data.frame(InDegree,OutDegree,Closeness,Betweenness,Egenvector) 

head(facebook_centrality, 10)
```
```cml
   InDegree OutDegree Closeness  Betweenness   Egenvector
1         1         2 0.2039513     2.991667 0.0003358296
2         5        32 0.3050746   550.646820 0.0460419395
3         2        19 0.3210807  2893.975922 0.0203613636
4         5        18 0.3689531  1738.462042 0.1022714530
5         3        20 0.3379630  1740.128272 0.0487541099
6         7        42 0.3765660  4829.283854 0.0662261110
7        20        13 0.3096970  3121.721080 0.0218889077
8         1         9 0.2862745   336.475414 0.0112473155
9         4         1 0.0000000     6.824242 0.0000000000
10       36        27 0.3717716 23569.771057 0.0706553413
```

### Add Name column to `facebook_centrality` by the origin node names
```r
facebook_centrality$username<- get.vertex.attribute(net,"vertex.names") 
head(facebook_centrality)
```
```cml
   InDegree OutDegree Closeness  Betweenness   Egenvector                username
1         1         2 0.2039513     2.991667 0.0003358296               supergoop
2         5        32 0.3050746   550.646820 0.0460419395 DPWorldTourChampionship
3         2        19 0.3210807  2893.975922 0.0203613636           LangLangPiano
4         5        18 0.3689531  1738.462042 0.1022714530              royhibbert
5         3        20 0.3379630  1740.128272 0.0487541099         stevenjackson39
6         7        42 0.3765660  4829.283854 0.0662261110      CarliLloydOfficial
7        20        13 0.3096970  3121.721080 0.0218889077                     CP3
8         1         9 0.2862745   336.475414 0.0112473155              akbargbaja
9         4         1 0.0000000     6.824242 0.0000000000             FastCompany
10       36        27 0.3717716 23569.771057 0.0706553413                    Kobe
```
> get.vertex.attribute( graph, name )
> > graph = the net name
> > name = values in `Vertex attributes`, which can be found by `summary()`

### Which node have the highest level of eigenvector? (Besides Nike) 
### Which node has the highest level of degree? (Besides Nike)

## Combine network centrality data with other node attributes

### read another file (facebook_node_attributes.csv)
```r
fb_attribute <- read.csv(file = 'facebook_node_attributes.csv',header=TRUE) 
head(fb_attribute, 6)
```
```cml
     X         name      username          label           category post_activity fan_count talking_about_count users_can_post
1  695 1.240000e+14 1brianroberts  Brian Roberts            Athlete          0.00      5601                   0              no
2 1087 4.000000e+14     22RudyGay       Rudy Gay            Athlete          0.00    375770                 131              no
3  634 1.337282e+10       23andMe        23andMe    Product/Service          0.29    452384                9030             yes
4  587 1.270000e+14 3DSkateboards 3d Skateboards    Product/Service          0.00     22625                  12             yes
5  943 1.680000e+14  3GerardPique   Gerard Piqué            Athlete          0.01  18913264                9758             yes
6  447 1.540000e+15     60SecDocs 60 Second Docs Media/News Company          0.04   1060661               37802             yes
```

### merge
```r
fb_merge <- merge(fb_attribute, facebook_centrality, by = "username")
head(fb_merge, 6)
```
```cml
       username    X         name          label           category post_activity fan_count talking_about_count
1 1brianroberts  695 1.240000e+14  Brian Roberts            Athlete          0.00      5601                   0
2     22RudyGay 1087 4.000000e+14       Rudy Gay            Athlete          0.00    375770                 131
3       23andMe  634 1.337282e+10        23andMe    Product/Service          0.29    452384                9030
4 3DSkateboards  587 1.270000e+14 3d Skateboards    Product/Service          0.00     22625                  12
5  3GerardPique  943 1.680000e+14   Gerard Piqué            Athlete          0.01  18913264                9758
6     60SecDocs  447 1.540000e+15 60 Second Docs Media/News Company          0.04   1060661               37802

  users_can_post InDegree OutDegree Closeness Betweenness   Egenvector
1             no        2         0 0.0000000       0.000 0.0000000000
2             no        3         0 0.0000000       0.000 0.0000000000
3            yes        4         3 0.2577554       7.100 0.0016032468
4            yes        5         1 0.1738391       0.250 0.0000337897
5            yes        8         3 0.3380748    1697.807 0.0087172868
6            yes        1         0 0.0000000       0.000 0.0000000000
```

## Linear Regression

### create a binary(boolean) variable, `user_can_post`
```r
fb_merge$user_post_binary=ifelse(fb_merge$users_can_post=="yes",1,0)
```

### predict the dependent variable of "fan_count" based on the centrality measures
```r
relation=lm( log(fan_count+1) ~ InDegree + OutDegree + Closeness + Betweenness + Egenvector, data = fb_merge)
summary(relation)
```
```cml
Call:
lm(formula = log(fan_count + 1) ~ InDegree + OutDegree + Closeness + 
    Betweenness + Egenvector, data = fb_merge)

Residuals:
    Min      1Q  Median      3Q     Max 
-9.0732 -1.6645  0.2125  1.6516  6.9659 

Coefficients:
              Estimate Std. Error t value Pr(>|t|)    
(Intercept)  1.126e+01  1.473e-01  76.458  < 2e-16 ***
InDegree     1.926e-01  1.383e-02  13.930  < 2e-16 ***
OutDegree   -1.209e-03  1.060e-02  -0.114    0.909    
Closeness    4.458e-01  6.811e-01   0.655    0.513    
Betweenness -5.351e-05  1.095e-05  -4.885  1.2e-06 ***
Egenvector   2.272e+00  4.033e+00   0.564    0.573    
---
Signif. codes:  0 ‘***’ 0.001 ‘**’ 0.01 ‘*’ 0.05 ‘.’ 0.1 ‘ ’ 1

Residual standard error: 2.447 on 1017 degrees of freedom
Multiple R-squared:  0.2164,	Adjusted R-squared:  0.2125 
F-statistic: 56.17 on 5 and 1017 DF,  p-value: < 2.2e-16
```

### predict the dependent variable of "user_post_binary" based on the centrality measures?

## Adding attributes from internal sources

> list.vertex.attributes()

> set.vertex.attributes()

### check current net's vertex
```r
list.vertex.attributes(net)
```
```cml
[1] "na"           "vertex.names"
```

### Add Indegree, Outdegree, Closeness
```r
set.vertex.attribute(net, "InDegree", InDegree)
set.vertex.attribute(net, "OutDegree", OutDegree)
set.vertex.attribute(net, "Closeness", Closeness)

list.vertex.attributes(net)
```
```cml
[1] "Closeness"    "InDegree"     "na"           "OutDegree"   
[5] "vertex.names"
```

### Add Egenvector, Betweenness
```r
set.vertex.attribute(net, "Egenvector", Egenvector)
set.vertex.attribute(net, "Betweenness", Betweenness)

list.vertex.attributes(net)
```
```cml
[1] "Betweenness"  "Closeness"    "Egenvector"   "InDegree"    
[5] "na"           "OutDegree"    "vertex.names"
```

## Adding attributes from external sources

### add `talking_about_count`, `users_can_post`, `category` from data `fb_merge`
```r
set.vertex.attribute(net, "talking_about_count", 
                          fb_merge$talking_about_count)
set.vertex.attribute(net, "users_can_post", 
                          fb_merge$user_post_binary)
                          
# set category be sub dataframe of fb_merge$category
# if fb_merge$category not found, set its data be "others"
category<-ifelse(fb_merge$category!="", fb_merge$category, "Others")
set.vertex.attribute(net, "category", category)

list.vertex.attributes(net)
```
```cml
[1] "Betweenness"         "category"            "Closeness"           "Egenvector"         
[5] "InDegree"            "na"                  "OutDegree"           "talking_about_count"
[9] "users_can_post"      "vertex.names" 
```

### add `fan_count` from `fb_merge`
```r
set.vertex.attribute(net, "fan_count", 
                          fb_merge$fan_count)
list.vertex.attributes(net)
```
```cml
[1] "Betweenness"         "category"            "Closeness"           "Egenvector"         
[5] "fan_count"           "InDegree"            "na"                  "OutDegree"
[9] "talking_about_count" "users_can_post"      "vertex.names" 
```

## Filter Network
```r
#filter based on attributes
n1F <- get.inducedSubgraph(net,  which(net %v% "fan_count" >30000000)) #20000000

#attempt 1
gplot(n1F,displaylabels=TRUE) 


#attempt 2
par(mar=c(2,2,2,2))
gplot(n1F,displaylabels=TRUE,displayisolates = FALSE,
      label.pos=1,label.col="blue", mode = "fruchtermanreingold",
      vertex.cex = get.vertex.attribute(n1F,"fan_count")/100000000) 

#attempt 3
gplot(n1F,displaylabels=TRUE,displayisolates = FALSE,
      label.pos=1,label.col="blue", mode = "fruchtermanreingold",
      vertex.cex = get.vertex.attribute(n1F,"fan_count")/100000000
      ,vertex.col=factor(get.vertex.attribute(n1F,"category")) ) 


#different modes of displaying the network
# mode = "fruchtermanreingold"
# mode = "circle"
# mode = "kamadakawai"
# mode = "mds"
# mode = "spring"
```
