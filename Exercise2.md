Exercise 2 - Fakebook Bus
================

## Loading the igraph library
library(igraph)

``` r
library(igraph)
```
载入程辑包：‘igraph’

The following objects are masked from ‘package:stats’:

    decompose, spectrum

The following object is masked from ‘package:base’:

    union
    
## Loading the tidyverse library
``` r
library(tidyverse)
```
-- Attaching packages ----------------------------------------------------------------------------------- tidyverse 1.3.1 --
v ggplot2 3.3.6     v purrr   0.3.4
v tibble  3.1.7     v dplyr   1.0.9
v tidyr   1.2.0     v stringr 1.4.0
v readr   2.1.2     v forcats 0.5.1
-- Conflicts -------------------------------------------------------------------------------------- tidyverse_conflicts() --
x dplyr::as_data_frame() masks tibble::as_data_frame(), igraph::as_data_frame()
x purrr::compose()       masks igraph::compose()
x tidyr::crossing()      masks igraph::crossing()
x dplyr::filter()        masks stats::filter()
x dplyr::groups()        masks igraph::groups()
x dplyr::lag()           masks stats::lag()
x purrr::simplify()      masks igraph::simplify()

Seats 1-6 have already been taken
Available choices: Seats A-D

``` r
nodes <- data.frame(nodes = c("1","2","3","4","5","6","A","B","C","D"))
nodes
```
nodes
1      1
2      2
3      3
4      4
5      5
6      6
7      A
8      B
9      C
10     D

## Creating the edges:
## The network is undirected
``` r
edges <- data.frame(from = 
                          c("1","2","2","3","3","3","3","3","4","4","5","5","5","6","6","6","A","A","A",
                            "B","B","B","B","B","C","C","C","C","C","D","D","D","D","D"), 
                        to =
                          c("2","1","A","4","5","B","C","D","3","3","3","6","D","5","B","D","2","B","C",
                            "3","6","A","C","D","3","4","A","B","D","3","5","6","B","C"))
edges %>% head()
```
  from to
1    1  2
2    2  1
3    2  A
4    3  4
5    3  5
6    3  B

``` r
data <- read.csv('/Users/Andy/Desktop/Exercise2.csv')

Graph = graph_from_data_frame(d=data,vertices=NULL ,directed=FALSE)
Graph

FB <- graph_from_data_frame(d = edges, vertices = nodeS, directed = FALSE)
FB
```
## IGRAPH 1b817d1 UN-- 10 17 -- 
## + attr: name (v/c), edge (e/n)
## + edges from 1b817d1 (vertex names):
##  [1] 1--2 2--A A--B A--C B--C B--D B--6 B--3 D--6 D--3 D--C D--5 5--6 5--3 C--3
## [16] C--4 3--4

``` r
degree(Graph, v=V(Graph))
```
## Various measures of centrality

``` r
betweenness(Graph)
```
##          1          2          A          B          D          5          C 
##  0.0000000  8.0000000 14.0000000  9.0333333  3.2666667  0.5333333  8.6000000 
##          3          6          4 
##  4.6333333  0.9333333  0.0000000

``` r
degree(Graph, v=V(Graph))
```
## 1 2 A B D 5 C 3 6 4 
## 1 2 3 5 5 3 5 5 3 2

``` r
evcent(Graph)$vector
```
##          1          2          A          B          D          5          C 
## 0.03059284 0.12661070 0.49339477 0.97394849 1.00000000 0.62726236 0.94139110 
##          3          6          4 
## 0.96744261 0.62852844 0.46122992

## Plot the network graph with labels and centrality values

``` r
ggraph(Graph) +
  geom_edge_link() +
  geom_node_point()
```

B seems to be the bst option I should choose. Choosing seat B would provide the best opportunity to connect with most of people nearby.
It has the highest degree centrality and closeness centrality, and relatively high betweeness centrality.

Using different centrality measures will provide various insights. As the result shows, Seats B, C and D seem to have degrees centrality of 5. 
B has the highest betweenness centrality, with C trailing slightly. While D scores lower in this metric in comparison.  

Concluding the results above, B appears to be the best option.
