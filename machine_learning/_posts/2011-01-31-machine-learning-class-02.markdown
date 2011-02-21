Using Weka
Open Source ML package
Java Based
Data Mining by Witten and Frank (on the web for free)

Some hypothesis spaces have two candidates for most specific hypothesis


Inductive Bias
----
* what is the hypothesis space?
* which candidate hypothesis is chosen?

Three learners with different Biases
----
1. Rote learner: Store exmaples, Classify x iff it matches previously observed example
2. List-then-eliminate (H=conjuncions):
3. Find-S

Some issues in Machine Learning
----
* what hypothesis space works well?
* for these spaces, what learning algoithms work well
* how can we optimize accuracy of unseen data points?
* how does the # of training example influence accuracy?
* high dimension data
  * computaiton limits
  * amount of training data
* noise
* limits of learnability
* prior knowledge

Decision Tree Learning
----
j48 is Weka's implementaiton of C4.5

When to consider decision trees
* instances describable by attrib-value
* target func is discrete value (classification)
* disjunctive hypothesis may be required (can capture and/or)
* possibly noisy training data

How to make trees 
----
* Choose attribute as root
* This should split training data
* Recurse over both sides

Choosing which attribute as root
----

Entropy
----
It's good if I end up with nodess with mostly +'s or only -'s
* S is a sample of training examples
* p+ the proportion of positive examples
* p- the proportion of negative examples
* entropy measures the "impurity' of S (how far away from being either all plus or all minus)

Decision trees would not do well with one-sided data; they would just classify to that side.

However, Find-S may still be valid for one-sided data.... that is, it can still distinguish between + and - because it can bound all of the positive

Gain(S training set, A attribute) = expected reduction in entropy due to splitting on A

Expected reduction in entropy by seeing A (entropy is reduced as we go down branches, more info, less entropy)

Pick attribute that has highest gain (maximize gain).  That will help us classify!

When you have to choose a node:
A1 A2 A3
Compute 
	Gain(S, A1)
	Gain(S, A2)
	Gain(S, A3)

Choose the one with highest gain


ID3
----
* Uses gain
* Hypothesis space is complete, target function surely in there
* 2 examples with opposite labels
* Outputs a single hypothesis
* no backtracking!
* statistically base, but robust to noisy data
* inductive bias: approx "prefer shortest tree"
