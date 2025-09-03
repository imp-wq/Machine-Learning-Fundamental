[StatQuest-Cross Validation](https://www.youtube.com/watch?v=fSytzGwwBVw)

- Cross Validation allows us to compare different machine learning methods and get a sense of how well they will work in practice
- Two things we need to do with data:
	- estimate the parameters for the machine learning methods - Training
	- evaluate how well the machine learning methods work - Testing
### A Not Good Idea
- 75% data for training, 25% data for testing
- Problem: how do we know that using the 75% data for training and the last 25% data for testing is  the best way to divide up the data?
### Cross Validation
- For which block(25% of the data) would be best for testing - Cross validation use them all, one at a time, and summarizes the results at the end.
- We divide the data into 4 blocks - **Four-Fold** Cross Validation
- 