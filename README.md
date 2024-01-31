# Differential-Privacy

This is a sample implementation of a general procedure for generating synthetic marginals of several related columns in  a given dataset (I am using pandas).

## The Problem:
Want to write a method of generating accurate, differentially private synthetic data based on general columns. This is to say, I want this method to work regardless of the columns that have been requested, provided these columns are restricted to not contain uniquely identifying information such as SSN.

## Solution:
First, I implemented a function that generates a two-way marginal based off of the two columns given to the function, and the given epsilon. This function is basically identical to our HW application of the same function. It gets a two dimensional list of values from the adult dataset, and then turns those values into probabilities by dividing through by the size of the dataset.
	Next, I implemented a function general_syn_dat() that takes in ‘n’, the size of the desired synthetic dataset, epsilon, and ‘cols’, which is the list of the 4 columns the user desires their synthetic data to contain. If we say the columns passed in are c1-c4, the function uses the marginal generating function previously discussed to create three marginals that are sequentially generated from the columns. This means we get one marginal for the column pair (c1,c2), one for (c2,c3), and so on. This is different from a similar application we have done previously that created these marginals based off of just c1. I think that this is likely a better solution to creating robustly correlated synthetic data.
	Next the function uses the marginals to (again sequentially) generate synthetic data first by (c1,c2), and then the subsequent columns are generated based on the conditional probabilities of the columns that have already been generated. This gives us data that generally resembles the original data better than if we were to simply base every column off of the first column, because it preserves the correlations between subsequent columns.

In my test cases I have passed various different columns and categories through to the function and have found that it is almost always capable of generating synthetic data that is roughly 90-95% similar to the original dataset
