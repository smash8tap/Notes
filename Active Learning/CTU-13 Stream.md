## Combination of categorical and numerical data
- Alternative is to use generalized additive models (GAM's)
-  Distance metrics that can be used:
	- Levenshtien distance (or any form of "edit distance")

	- Longest common subsequence metric

	- Gower distance
	- cosine distance

## To do's

- Extract botnet data points and check the accuracy on just the botnet class
- Have a minimum number of botnet labels in the initial learning set **done**
- Maybe we have to sort the initial training set according to time
- Convert the test data into the distinc classes fo labels and then test the accuracy on each of the class


## Conclusions Drawn

- Dont use a ratio to manually split the data
- Going sequentially (temporally) is not a good idea when we are extracting first 100 botnet, 1000 normal, 10000 bg data points. because when we start training the AL model it will just have Backgorund data
- Choosing data points with highest entropy is  better then Randomly choosing data points for query (because the amount of bg data is much more) 


## QUestions

- Is it a good idea to make test and pool split?



## Scenario 1

Initial dataset ratio- Normal (1000), Background (10000), Botnet (100)

- Initial Accuracy:

  - Accuracy on normal: 0.006739323651488088
  - Accuracy on background: 0.0003923695102557007
  - Accuracy on botnet: 1.0
  - Overall Accuracy: 0.006232740324687235

- After Iterating over 10k points:
  - Accuracy on normal: 0.006747952747072579
  - Accuracy on background: 0.0022657491293557727
  - Accuracy on botnet: 1.0
  - Overall Accuracy: 0.008050493772982333

Model was only seeing background data and hence only querying botnet class
