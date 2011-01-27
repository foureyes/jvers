

Machine Learning CS 6923
========================

Textbook: Machine Learning by Tom Mitchell (1997)
1st chapter of 2nd edition is on Tom Mitchell's website

Course work
* 4 homeworks
* course project - apply machine learning to a problem that you are interested in
* in class mid term
* in class final

Pre reqs
* 5403, 6003, 6033 (data structures, discrete math, algorithms)
* probability
* statistics
* calculus, multivariate calculus
* linear algebra

Logistics
* blackboard

Class Notes
========================
Chapters 1 and 2

Machine Learning Applications
========================
* Data mining
** Recommendations
** Search engines
* Applications that we don't know how to program by hand (expert systems)
** Speech recognition
** Autonomous driving
* Customized programs
** Spam filter
** Ads 

Early Applications of Machine learning
========================

Loan Risk
------------------------
Data
* Given 5000 lending records
* For each loan, characteristics of borrower
* Whether the loan was repaid

Extract Rules
if other-delinguent-accounts > 2 and num-late-payments > 1
	paid-back-loan = no


What Kind of People by Your Product
------------------------

Customer Retention
------------------------

Types of Learning
========================
* Supervised Learning (focus of course)
* Unsupervised Learning
* Reinforcement Learning

Learning From Data / Supervised Learning
========================
* Data provides the right answer 
* "Label Data"
* The data comes with labels/values
* Task is to predict labels/values

Classification Problems (focus of course)
------------------------
*Predict discrete value
*Small finite set
*Example: yes/no (spam)

Regression Problems
------------------------
*Predict real value (continuous values)

Unsupervised Learning
========================
* No labels
* Discover Patterns
* Clustering (data mining)

Supervised Learning Detail
========================
Given: Examples <x, f(x)>
Spam filtering:
	x is an email
	f(x) is yes or no

Examples are called "training examples"

This is for some unknown function f.

Task: is to learn f, or at least learn some good approximation of f.

Goal: is to output hypothesis h that is a good approximation of f (or equal to f!)

Supervised learning is a form of inductive learning.

Inductive Learning
	Learn rule (hypothesis)
	based on observations (training)

Data
------------------------
<x, f(x)>
x -> examples
f(x) ->
an example is broken down into different pieces x1, x2, x3, etc
these are the features or attributes of x

different types of features
* categorical (discrete and unordered)
** ex sex: male, female
* discrete and ordered
** ex age: 26
* continuous
** teperature: 20.6 degrees
* relational
** ex. borther of:Alex

How are they related?
------------------------
* independent
* time series

Concept Learning
------------------------
* Label - binar value (Ex, spam... yes, no or 0, 1)

ex   x1 x2 x3 x4 y
----------------------
1    0  0  1  0  0
2    0  1  0  0  0
3    0  0  1  1  1
4    1  0  0  1  1
5    0  1  1  0  0
6    0  1  0  0  0
7    0  1  0  1  0

* x has 4 features 
* binary features
* 2^4 possibilitites
* binary label

What types of rules are we willing to accept?
High chance of collision for small number of attributes

* expand out all possibiities
* 9 are not in data set
