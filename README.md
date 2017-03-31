# Decision_tree
Building Decision tree classifier on a dataset.

In order to run the code:
The assignment has been done in R using Rpart package. In order to run the file through the command line please use the following commands:

> r

> source("mlDecisionTree.R") 

There is no need to load any files and the paths are not hardcoded. All that needs to be done is ensure that the command line is running in the directory that contains all the files.
Instead of running Rscript, source() would be a better command for my code as there are six files to be passed as attributes and it also outputs graphs. But if it is necessary that it has to be run with arguments, use the following command:

> Rscript mlDecisionTreewithargs.R training_set1.csv test_set1.csv validation_set1.csv training_set2.csv test_set2.csv validation_set2.csv

NOTE:There are two R files one works with source command and the other (mlDecisionTreewithargs) works with Rscript.

The package Rpart was used to create the required and to plot trees and print the summaries. Various functions were used but the most important was the rpart function and split was made on the basis of information gain using parms = list(split = 'information'), minsplit = 2, minbucket = 1 parameters in the rpart function.


Results:

Training set 1:

> print(cfit1)
n= 600 

node), split, n, loss, yval, (yprob)
      * denotes terminal node

1) root 600 300 0 (0.5000000 0.5000000)  
  2) Class< 0.5 300   0 0 (1.0000000 0.0000000) *
  3) Class>=0.5 300   0 1 (0.0000000 1.0000000) *



> printcp(cfit1)

Classification tree:
rpart(formula = part1 ~ ., data = train1, method = "class", parms = list(split = "information"), 
    minsplit = 2, minbucket = 1)

Variables actually used in tree construction:
[1] Class

Root node error: 300/600 = 0.5

n= 600 

    CP nsplit rel error xerror    xstd
1 1.00      0         1    1.1 0.04062
2 0.01      1         0    0.0 0.00000

>plot(cfit1)
>text(cfit1)



>plotcp(cfit1)
>text(cfit1)



> summary(cfit1)
Call:
rpart(formula = part1 ~ ., data = train1, method = "class", parms = list(split = "information"), 
    minsplit = 2, minbucket = 1)
  n= 600 

    CP nsplit rel error xerror       xstd
1 1.00      0         1    1.1 0.04062019
2 0.01      1         0    0.0 0.00000000

Variable importance
Class    XO    XI    XM    XT    XR 
   61    10     9     7     7     6 

Node number 1: 600 observations,    complexity param=1
  predicted class=0  expected loss=0.5  P(node) =1
    class counts:   300   300
   probabilities: 0.500 0.500 
  left son=2 (300 obs) right son=3 (300 obs)
  Primary splits:
      Class < 0.5 to the left,  improve=415.888300, (0 missing)
      XO    < 0.5 to the left,  improve=  8.765052, (0 missing)
      XI    < 0.5 to the left,  improve=  6.621767, (0 missing)
      XM    < 0.5 to the left,  improve=  3.450181, (0 missing)
      XT    < 0.5 to the right, improve=  3.445968, (0 missing)
  Surrogate splits:
      XO < 0.5 to the left,  agree=0.585, adj=0.170, (0 split)
      XI < 0.5 to the left,  agree=0.573, adj=0.147, (0 split)
      XM < 0.5 to the left,  agree=0.553, adj=0.107, (0 split)
      XT < 0.5 to the right, agree=0.553, adj=0.107, (0 split)
      XR < 0.5 to the right, agree=0.548, adj=0.097, (0 split)

Node number 2: 300 observations
  predicted class=0  expected loss=0  P(node) =0.5
    class counts:   300     0
   probabilities: 1.000 0.000 

Node number 3: 300 observations
  predicted class=1  expected loss=0  P(node) =0.5
    class counts:     0   300
   probabilities: 0.000 1.000


After pruning:

> prune(cfit1, cp = cfit1$cptable[which.min(cfit1$cptable[,"xerror"]),"CP"])
n= 600 

node), split, n, loss, yval, (yprob)
      * denotes terminal node

1) root 600 300 0 (0.5000000 0.5000000)  
  2) Class< 0.5 300   0 0 (1.0000000 0.0000000) *
  3) Class>=0.5 300   0 1 (0.0000000 1.0000000) *


> print(cfit1)
n= 600 

node), split, n, loss, yval, (yprob)
      * denotes terminal node

1) root 600 300 0 (0.5000000 0.5000000)  
  2) Class< 0.5 300   0 0 (1.0000000 0.0000000) *
  3) Class>=0.5 300   0 1 (0.0000000 1.0000000) *



> plot(cfit1)
> text(cfit1)


> summary(cfit1)
Call:
rpart(formula = part1 ~ ., data = train1, method = "class", parms = list(split = "information"), 
    minsplit = 2, minbucket = 1)
  n= 600 

    CP nsplit rel error xerror       xstd
1 1.00      0         1    1.1 0.04062019
2 0.01      1         0    0.0 0.00000000

Variable importance
Class    XO    XI    XM    XT    XR 
   61    10     9     7     7     6 

Node number 1: 600 observations,    complexity param=1
  predicted class=0  expected loss=0.5  P(node) =1
    class counts:   300   300
   probabilities: 0.500 0.500 
  left son=2 (300 obs) right son=3 (300 obs)
  Primary splits:
      Class < 0.5 to the left,  improve=415.888300, (0 missing)
      XO    < 0.5 to the left,  improve=  8.765052, (0 missing)
      XI    < 0.5 to the left,  improve=  6.621767, (0 missing)
      XM    < 0.5 to the left,  improve=  3.450181, (0 missing)
      XT    < 0.5 to the right, improve=  3.445968, (0 missing)
  Surrogate splits:
      XO < 0.5 to the left,  agree=0.585, adj=0.170, (0 split)
      XI < 0.5 to the left,  agree=0.573, adj=0.147, (0 split)
      XM < 0.5 to the left,  agree=0.553, adj=0.107, (0 split)
      XT < 0.5 to the right, agree=0.553, adj=0.107, (0 split)
      XR < 0.5 to the right, agree=0.548, adj=0.097, (0 split)

Node number 2: 300 observations
  predicted class=0  expected loss=0  P(node) =0.5
    class counts:   300     0
   probabilities: 1.000 0.000 

Node number 3: 300 observations
  predicted class=1  expected loss=0  P(node) =0.5
    class counts:     0   300
   probabilities: 0.000 1.000


Training set2:


> summary(cfit2)
Call:
rpart(formula = part2 ~ ., data = train2, method = "class", parms = list(split = "information"), 
    minsplit = 2, minbucket = 1)
  n= 600 

    CP nsplit rel error   xerror       xstd
1 1.00      0         1 1.153333 0.04034206
2 0.01      1         0 0.000000 0.00000000

Variable importance
Class    XI    XB    XK    XF    XJ 
   59    12     8     7     7     6 

Node number 1: 600 observations,    complexity param=1
  predicted class=0  expected loss=0.5  P(node) =1
    class counts:   300   300
   probabilities: 0.500 0.500 
  left son=2 (300 obs) right son=3 (300 obs)
  Primary splits:
      Class < 0.5 to the left,  improve=415.888300, (0 missing)
      XI    < 0.5 to the left,  improve= 11.679450, (0 missing)
      XB    < 0.5 to the right, improve=  5.952079, (0 missing)
      XK    < 0.5 to the right, improve=  4.889959, (0 missing)
      XF    < 0.5 to the left,  improve=  4.589902, (0 missing)
  Surrogate splits:
      XI < 0.5 to the left,  agree=0.598, adj=0.197, (0 split)
      XB < 0.5 to the right, agree=0.570, adj=0.140, (0 split)
      XK < 0.5 to the right, agree=0.563, adj=0.127, (0 split)
      XF < 0.5 to the left,  agree=0.562, adj=0.123, (0 split)
      XJ < 0.5 to the left,  agree=0.555, adj=0.110, (0 split)

Node number 2: 300 observations
  predicted class=0  expected loss=0  P(node) =0.5
    class counts:   300     0
   probabilities: 1.000 0.000 

Node number 3: 300 observations
  predicted class=1  expected loss=0  P(node) =0.5
    class counts:     0   300
   probabilities: 0.000 1.000


After Pruning:
> summary(cfit2)
Call:
rpart(formula = part2 ~ ., data = train2, method = "class", parms = list(split = "information"), 
    minsplit = 2, minbucket = 1)
  n= 600 

    CP nsplit rel error   xerror       xstd
1 1.00      0         1 1.153333 0.04034206
2 0.01      1         0 0.000000 0.00000000

Variable importance
Class    XI    XB    XK    XF    XJ 
   59    12     8     7     7     6 

Node number 1: 600 observations,    complexity param=1
  predicted class=0  expected loss=0.5  P(node) =1
    class counts:   300   300
   probabilities: 0.500 0.500 
  left son=2 (300 obs) right son=3 (300 obs)
  Primary splits:
      Class < 0.5 to the left,  improve=415.888300, (0 missing)
      XI    < 0.5 to the left,  improve= 11.679450, (0 missing)
      XB    < 0.5 to the right, improve=  5.952079, (0 missing)
      XK    < 0.5 to the right, improve=  4.889959, (0 missing)
      XF    < 0.5 to the left,  improve=  4.589902, (0 missing)
  Surrogate splits:
      XI < 0.5 to the left,  agree=0.598, adj=0.197, (0 split)
      XB < 0.5 to the right, agree=0.570, adj=0.140, (0 split)
      XK < 0.5 to the right, agree=0.563, adj=0.127, (0 split)
      XF < 0.5 to the left,  agree=0.562, adj=0.123, (0 split)
      XJ < 0.5 to the left,  agree=0.555, adj=0.110, (0 split)

Node number 2: 300 observations
  predicted class=0  expected loss=0  P(node) =0.5
    class counts:   300     0
   probabilities: 1.000 0.000 

Node number 3: 300 observations
  predicted class=1  expected loss=0  P(node) =0.5
    class counts:     0   300
   probabilities: 0.000 1.000
