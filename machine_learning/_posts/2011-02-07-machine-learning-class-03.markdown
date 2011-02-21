02/07 Class 03
====

Avoiding Overfitting
----
 * Don't wait until your leaves are pure, for example... if a node winds up overwhelmingly positive or negative, stop growing there. (stop growing when the data split is not statistically significant).
 * Post prune



Regression Trees
---

take all real values of labels

check variance of of labels

at each node, choose variable that causes most decrease in impurity (variance)
 
Bayesian Learning
====
Appealing to statisticians

Two approaches to supervised machine learning
1. Discriminative - just learn to discriminate different kinds of examples
2. Generative - learn a model of how data was generated

Bayesian methods are generative

h = hypothesis
D = Data
P(h) - prior probability of hypothesis.  before you see any data
P(D) - prior probability of data D
P(h|D) - probability of h given D
P(D|h) - probability of D given h

P(h|D)  = P(D|h)P(h)
          ----------
             P(D)

which hypothesis fits data best?  which hypothesis was most likely to produce that data

maximum after you see the datat hypothesis - hmap

Example

Data - I was late for class
h1 - I was kidnapped by martians
h2 - I forgot my laptop

before you see data (i was late for class), the two hypotheses have a "prior" probability

.000....1
.9999...

Once you see the data, does it may
P(D|h1) = what's the probability of me being late to class if I'm kidnapped by martians = 1
P(D|h2) = what's the probability of me being late to class if I forgot my laptop = 0.5


from slide...

P(cancer) = 0.008 									P(^cancer) = 0.992
P(+|cancer) = .98 positive test if has cancer		P(-|cancer) = 0.02
P(+|^cancer) = 0.03 positive test if no cancer		P(-|^cancer) =

which is more likely?
D = +
P(cancer|+)
P(^cancer|+)

hmap = argmap         P(D|h)P(h) .... product of probability of hypothesis and probability of data given hypothesis
       h element H

For h = cancer
P(D|h)P(h)
 = 0.98 * 0.008


h = ^ cancer
 = 0.03 * 0.992

Brute for hypothesis learner
----


