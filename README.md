# hierarchical_power

`hierarchical_power` is an R function to calculate the 'hierarchical power' of individuals in a hierarchy. What's hierarchical power, you ask? It's a measure of control over subordinates. I define hierarchical power as the number of subordinates + 1. Here's an example:

![hp example](https://economicsfromthetopdown.files.wordpress.com/2019/08/finding_subordinates.png)

For example uses of this metric, see: 

*  *Personal Income and Hierarchical Power*. Journal of Economic Issues. 2019; 53(4): 928-945. [SocArXiv preprint](https://osf.io/preprints/socarxiv/pb475/).

* *[Energy, hierarchy and the origin of inequality](https://journals.plos.org/plosone/article?id=10.1371/journal.pone.0215692)*. PLOS ONE. 2019; 14(4):e0215692.


### Inputs

* `hierarchy_vec` = a vector of the employment (membership) in each rank of the hierarchy. Must be in order of ascending rank (i.e. from the bottom to the top of the hierarchy)



### Output
`hierarchical_power` returns a vector containing the average hierarchical power per person in each rank of the hierarchy. 

### Example:

```R
library(RcppArmadillo)
library(Rcpp)

sourceCpp("hierarchical_power.cpp")

# number of people in each hierarchical rank 
# (starting at the bottom of the hierarchy)
hierarchy_vec = c(100, 50, 25, 10, 5, 1)

# average hierarchical power by rank
hierarchical_power(hierarchy_vec)

      [,1]
[1,]   1.0
[2,]   3.0
[3,]   7.0
[4,]  18.5
[5,]  38.0
[6,] 191.0

```


### More complicated example

Go grab the [hierarchy](https://github.com/blairfix/hierarchy) function --- a function for (you guessed it) making hierarchies. It takes an inputted institution size and returns a vector of membership by rank. Then plug this into the `hierarchical_power` function:

```R
# get hierarchy function
sourceCpp("hierarchy.cpp")

# make hierarchy with 10,000 members, 
# with span of control = 5
hierarchy_vec = hierarchy(10000, 5)

# average hierarchical power by rank
hierarchical_power(hierarchy_vec)

             [,1]
[1,]     1.000000
[2,]     5.999375
[3,]    30.996875
[4,]   155.984375
[5,]   768.923077
[6,]  3333.000000
[7,] 10000.000000
```


### Installation
To use `hierarchical_power`, install the following R packages:
 * [Rcpp](https://cran.r-project.org/web/packages/Rcpp/index.html) 
 * [RcppArmadillo](https://cran.r-project.org/web/packages/RcppArmadillo/index.html) 

Put the source code (`hierarchical_power.cpp`) in the directory of your R script. Then source it with the command `sourceCpp('hierarchical_power.cpp')`.






