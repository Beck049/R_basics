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

## Adding attributes from internal sources

## Adding attributes from external sources

## Filter Network
