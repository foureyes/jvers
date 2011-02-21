MDL - Minimum Description Length Principle
====

* some way to rep hypothesis in bits, some way to rep data in bits
* hypothesis can be very simple or complicated

example
H = decision trees
D = training data labels



fixed D
1 0 1 +
1 1 1 -
1 1 0 +

LC1(h) - # bits to describe tree h
LC2(D|h) - # bits to describe D given h

Trade off is complexity of hypothesis with something like the "accuracy" on training set
                                                                 |
                                                               exceptions on training set

for example:
    hMDL = argmin LC1(h)      + LC2(D|h)
                    |             |
                  bigger tree,  less exceptions


for example... trees

        x1
     0 /   \1
      -    +

small tree, one exception


        x3
     0 /   \1
      +     x2
        0 /   \1
         +     -

big tree, less exceptions


Map Hypothesis
----
Hypothesis that is most likely given the data (maximum a posteriori)


Most probable classification of new instances
----
Example:
 3 possible hypothesis
    P(h1|D) = 0.4
    P(h2|D) = 0.3
    P(h3|D) = 0.3

h1 is the MAP hypothesis... has highest probability after we've seen the data

    h1(x) = +
    h2(x) = -
    h3(x) = -

What's the most probable classification of x
it's -....


    P(label of x is + | D)?
     = 0.4
    
    P(label of x is - | D) = 0.6

h1, h2 and h3 are disjoint events

The most porbable classification of x is called the Bayes optimal classification (it's the label most likely for x, given the data)

Naive Bayes Classifier
----

* simple and fast
* moderate/large training set available
* attributes that describe insances are independent?

what's the most likely probability of the label given the attributes/data


example:

2 attributes:

a1           a2    label (or v)
yellow       y     +
yellow       n     +
red          y     +
red          n     -
red          n     -
red          n     -
yellow       y     -
red          y     -


probability of + is 3/8ths
best estimate for prior proability is 3/8ths
P(+) = 3/8
P(-) = 5/8

P(yellow | +) = 2/3
8 total to compute...

if we just want to predict, we don't have to go through all, just the ones needed for prediction



yellow no

P^(+)P^(a1=yellow | +)P^(a2=no | +)

3/8 * 2/3 * 1/3 = 1/12
P^(-)P^(a1=yellow | -)P^(a2=no | -)
5/8 * 1/5 * 3/5 = 3/40


1/12 is larger

quantity is maximized when label is plus...

so yellow no would be labeled plus

Issues
----
* why is this reasonable, should this work?  this relies on independance, but usually doesn't matter
* a 0 term could come in if we don't see label/attribute combo... this happens with sparse data.  we might not want exact frequency for our analysis
* 0 probabilities give naive bayes BIG problems
* one strategy to counter this is to smooth the frequency.  interpolate between prior belief and what is observed in data

P(ai|vj) ... nc + mp
             -------
              n + m

Use "virtual" sample... which is made of examples based on prior belief

For example... "prime" counts with prior belief
Y   N
2   2

Then do counts from training data

Standard choice for m, m = # attr values.

m = #attr values / p uniform

p = 1 / #attributes

P(ai|vj)

initializiing all "counters" to 1.

This way of setting m and p is referred to as "Add-1" smoothing.

Another issue....

If there are a lot of aattributes... you'll get underflow
Probabilities will look like 0
Take the log

Learning to Classify Text
----
We want to classify as +,- (interesting, not interesting... to user)

1. Represent each doc by a vector of words, w/ one attribute per word position in doc
2. Learning: use training examples to estimate
P(+)
P(-)
P(doc|+)
P(doc|-)

     w1 | w2 | w3 | ....
        |    |    |

P(doc|vj) = 
