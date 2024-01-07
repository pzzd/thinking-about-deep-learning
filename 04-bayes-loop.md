# Figuring out a Bayes Loop by Hand

I had a lot of trouble understanding how to use Bayes Theorem in a loop according to the description in Chapter 4. The idea that you pick a probability that you have a fair coin makes sense. And it makes sense that you use the outcome of test (posterior) as a parameter in the next test (the prior to be  exact). But I wasn't sure how to start off.

What if I start out assuming the coin is fair? Let's try some flips, and use Bayes Theorem `P(F|H) = P(H|F) P(F) / P(H)` to find the probability that we are using a fair coin. F means "it is a fair coin" and H means "the result of a flip is heads". From _Deep Learning_, one way to write out Bayes Theoreom is `Posterior = Likelihood * Prior / Evidence`.

You are supposed to use the version of the theorem that matches the outcome of the flip. When the outcome is heads, we use `P(F|H) = P(H|F) P(F) / P(H)` and for tails we use `P(F|T) = P(T|F) P(F) / P(T)`.


1. I flip heads. Likelihood is 1/2, prior is 1, evidence is 1/2. Then:

Posterior = 1/2 * 1 / 1/2 = 1

The value for posterior is my new prior.

2. I flip heads. Likelihood is 1/2, prior is 1, evidence is 1/2. Then: 

Posterior = 1/2 * 1 / 1/2 = 1

The value for posterior is my new prior.

3. I flip heads. Likelihood is 1/2, prior is 1, evidence is 1/2. Then: 

Posterior = 1/2 * 1 / 1/2 = 1

The value for posterior is my new prior.

4. I flip tails. Likelihood (this time P(T|F) is 1/2, prior is 1, evidence (this time P(T) is 1/2. Then: 

Posterior = 1/2 * 1 / 1/2 = 1

The value for posterior is my new prior.

5. I flip heads. Likelihood (this time P(T|H) is 1/2, prior is 1, evidence (this time P(H) is 1/2. Then: 

Posterior = 1/2 * 1 / 1/2 = 1

The value for posterior is my new prior.

```
 # Flip   Equation                       Posterior calculation
 1 Heads  P(F|H) = P(T|H) * P(F) / P(H)  Posterior = 0.5 * 1 / 0.5   = 0.5
```

The number of heads doesn't seem to have any bearing on the posterior at all. WTH? It looks like you could get heads a million times and the posterior will always be 1: over time this math shows you have a fair coin when clearly no normal human would be very suspicious.

I think my mistake was that I assumed the coin is fair, and so I never initiated the first trial with any doubt. To introduce doubt you have give a probability that the coin is biased. 

We can use our first set of flips to just make on some kind of bias. 4 heads out of 5 flips is a bias of .8. We use this for P(H), the evidence.

1. I flip heads. Likelihood is 1/2, prior is 1, evidence is 0.8. Then:

Posterior = 0.5 * 1 / 0.8 = 0.625

The value for posterior is my new prior.

2. I flip heads. Likelihood is 0.5, prior is 0.625, evidence is 0.8. Then: 

Posterior = 0.5 * 0.625 / 0.8 = 0.39

The value for posterior is my new prior.

3. I flip heads. Likelihood is 1/2, prior is 1, evidence is 1/2. Then: 

Posterior = 0.5 * .39 / 0.8 = 0.24

The value for posterior is my new prior.

4. I flip tails. Because the result is tails, we use P(T|F), which is is 0.5 (we have half a chance of tails with a fair coin). The prior comes from our previous posterior: 0.24. The evidence comes from our first set of flips: we found we got 1 tails out of 5, so P(T) is 0.2. Then: 

Posterior = 0.5 * 0.24 / 0.2 = 0.6

The value for posterior is my new prior. And you can see the tails pushes up the probability that we have a fair coin after all.

5. I flip heads. Likelihood (this time P(T|H) is 0.5, prior is 0.6, evidence (this time P(H) is 0.8. Then: 

Posterior = 0.5 * 0.6 / 0.8 = 0.375

The value for posterior is my new prior.

Can I recreate the chart in 4-23 with this method?

In this situation we have two coins: one is fair and the other has a bias of 0.2 (meaning 20% of flips will result in heads). The point here is to try to select one of the two coins randomly and find out which coin we picked, knowing the bias of the rigged coin: we are supposed to find P(F|H).

The probability of flipping heads is the sum of probabilities of flipping heads with either coin, divided by the number of coins: `P(H) = 0.5 + 0.2 / 2 = 0.35`. The probability of flipping tails is figured similarly: `P(T) = 0.5 + 0.8 / 2 = 0.65`. I will use P(H) or P(T) for the evidence, depending on the result of the flip.


The first prior P(F) is 0.5. I think this is right because we have a 50% chance of picking the fair coin. 

Likelihoods P(H|F) and P(T|F) are always 0.5. 

Now we have all the pieces need to figure the posterior P(F|H) repeatedly, hopefully helping decide if we picked the fair or biased coin.f

```
 # Flip   Equation                       Posterior calculation
 1 Tails  P(F|T) = P(T|F) * P(F) / P(T)  Posterior = 0.5 * 0.5 / 0.65   = 0.385 
 2 Tails  P(F|T) = P(T|F) * P(F) / P(T)  Posterior = 0.5 * 0.385 / 0.65 = 0.296
 3 Tails  P(F|T) = P(T|F) * P(F) / P(T)  Posterior = 0.5 * 0.296 / 0.65 = 0.228
 4 Tails  P(F|T) = P(T|F) * P(F) / P(T)  Posterior = 0.5 * 0.228 / 0.65 = 0.175
 5 Tails  P(F|T) = P(T|F) * P(F) / P(T)  Posterior = 0.5 * 0.175 / 0.65 = 0.135
 6 Tails  P(F|T) = P(T|F) * P(F) / P(T)  Posterior = 0.5 * 0.135 / 0.65 = 0.104
 7 Tails  P(F|T) = P(T|F) * P(F) / P(T)  Posterior = 0.5 * 0.104 / 0.65 = 0.08
 8 Tails  P(F|T) = P(T|F) * P(F) / P(T)  Posterior = 0.5 * 0.08 / 0.65  = 0.062
 9 Tails  P(F|T) = P(T|F) * P(F) / P(T)  Posterior = 0.5 * 0.062 / 0.65 = 0.048
10 Tails  P(F|H) = P(H|F) * P(F) / P(H)  Posterior = 0.5 * 0.048 / 0.35 = 0.069
11 Tails  P(F|H) = P(H|F) * P(F) / P(H)  Posterior = 0.5 * 0.069 / 0.35 = 0.099
12 Tails  P(F|T) = P(T|F) * P(F) / P(T)  Posterior = 0.5 * 0.099 / 0.65 = 0.076
```


This doesn't quite match the chart in 4-23 but it does sort of track the chart. Let's try that again but round the posterior to two decimal places. 


```
 # Flip   Equation                       Posterior calculation
 1 Tails  P(F|T) = P(T|F) * P(F) / P(T)  Posterior = 0.5 * 0.5 / 0.65  = 0.38 
 2 Tails  P(F|T) = P(T|F) * P(F) / P(T)  Posterior = 0.5 * 0.38 / 0.65 = 0.29
 3 Tails  P(F|T) = P(T|F) * P(F) / P(T)  Posterior = 0.5 * 0.29 / 0.65 = 0.22
 4 Tails  P(F|T) = P(T|F) * P(F) / P(T)  Posterior = 0.5 * 0.22 / 0.65 = 0.17
 5 Tails  P(F|T) = P(T|F) * P(F) / P(T)  Posterior = 0.5 * 0.17 / 0.65 = 0.13
 6 Tails  P(F|T) = P(T|F) * P(F) / P(T)  Posterior = 0.5 * 0.13 / 0.65 = 0.1
 7 Tails  P(F|T) = P(T|F) * P(F) / P(T)  Posterior = 0.5 * 0.1 / 0.65  = 0.08
 8 Tails  P(F|T) = P(T|F) * P(F) / P(T)  Posterior = 0.5 * 0.08 / 0.65 = 0.06
 9 Tails  P(F|T) = P(T|F) * P(F) / P(T)  Posterior = 0.5 * 0.06 / 0.65 = 0.04
10 Tails  P(F|H) = P(H|F) * P(F) / P(H)  Posterior = 0.5 * 0.04 / 0.35 = 0.06
11 Tails  P(F|H) = P(H|F) * P(F) / P(H)  Posterior = 0.5 * 0.06 / 0.35 = 0.09
12 Tails  P(F|T) = P(T|F) * P(F) / P(T)  Posterior = 0.5 * 0.09 / 0.65 = 0.07
```

This time the values seems to match the chart better.


So some lessons:

You have to capture your doubt in the evidence value in the Bayes Theorem. And evidence can be picked out of think air, or you can create some evidence with your intuition or observations.
