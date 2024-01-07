# Figuring out a Bayes Loop by Hand

I had a lot of trouble understanding how to use Bayes Theorem in a loop according to the description in Chapter 4. From _Deep Learning_, the equation for Bayes Theoreom `Posterior = Likelihood * Prior / Evidence` makes intuitive sense: you have an expected probability (Likelihood) and you adjust it with Prior information and current Evidence.The idea that you pick a probability that you have a fair coin (Prior, or P(F)) makes sense. And it makes sense that you use the outcome of a test (Posterior) as a parameter in the next test (the Prior): this is how experience influences the probability you are testing for. But I wasn't sure how to start off the loop.

To use Bayes Theorem in a loop, so that accumulated experience informs the probability you are using a fair coin, use `P(F|H) = P(H|F) P(F) / P(H)`. F means "it is a fair coin" and H means "the result of a flip is heads". You are supposed to use the version of the theorem that matches the outcome of the flip. When the outcome is heads, we use `P(F|H) = P(H|F) P(F) / P(H)` and for tails we use `P(F|T) = P(T|F) P(F) / P(T)`.

## Testing a coin assuming it is fair

What if I start out assuming the coin is fair? Let's try some flips. 

1. I flip heads. Likelihood is 0.5, prior is 1, evidence is 0.5. Then:

Posterior = 0.5 * 1 / 0.5 = 1

The value for posterior is my new prior.

2. I flip heads. Likelihood is 0.5, prior is 1, evidence is 0.5. Then: 

Posterior = 0.5 * 1 / 0.5 = 1

The value for posterior is my new prior.

3. I flip heads. Likelihood is 0.5, prior is 1, evidence is 0.5. Then: 

Posterior = 0.5 * 1 / 0.5 = 1

The value for posterior is my new prior.

4. I flip tails. Likelihood (this time P(T|F) is 0.5, prior is 1, evidence (this time P(T) is 0.5. Then: 

Posterior = 0.5 * 1 / 0.5 = 1

The value for posterior is my new prior.

5. I flip heads. Likelihood (this time P(T|H) is 0.5, prior is 1, evidence (this time P(H) is 0.5. Then: 

Posterior = 0.5 * 1 / 0.5 = 1

The value for posterior is my new prior.

To summarize in a table:
```
 # Flip   Equation                       Posterior calculation
 1 Heads  P(F|H) = P(H|F) * P(F) / P(H)  Posterior = 0.5 * 1 / 0.5 = 0.5
 2 Heads  P(F|H) = P(H|F) * P(F) / P(H)  Posterior = 0.5 * 1 / 0.5 = 0.5
 3 Heads  P(F|H) = P(H|F) * P(F) / P(H)  Posterior = 0.5 * 1 / 0.5 = 0.5
 4 Tails  P(F|T) = P(T|F) * P(F) / P(T)  Posterior = 0.5 * 1 / 0.5 = 0.5
 5 Heads  P(F|H) = P(H|F) * P(F) / P(H)  Posterior = 0.5 * 1 / 0.5 = 0.5
```

The number of heads doesn't seem to have any bearing on the Posterior at all. WTH? It looks like you could get heads a million times and the posterior will always be 1: over time this math shows you have a fair coin when clearly any normal human would be very suspicious.

My mistake was that I didn't introduce any kind of bias or doubt in my calculations. To introduce doubt you have give a probability that the coin is biased, and it can't be 1. 

# Testing again with some Evidence

We can use our first set of flips to just make up some kind of bias. Four heads out of 5 flips is a bias of 0.8: we use this for P(H), the Evidence.

```
 # Flip   Equation                       Posterior calculation
 1 Heads  P(F|H) = P(H|F) * P(F) / P(H)  Posterior = 0.5 * 1 / 0.8     = 0.625
 2 Heads  P(F|H) = P(H|F) * P(F) / P(H)  Posterior = 0.5 * 0.625 / 0.8 = 0.39
 3 Heads  P(F|H) = P(H|F) * P(F) / P(H)  Posterior = 0.5 * 0.39 / 0.8  = 0.24
 4 Tails  P(F|T) = P(T|F) * P(F) / P(T)  Posterior = 0.5 * 0.24 / 0.2  = 0.6
 5 Heads  P(F|H) = P(H|F) * P(F) / P(H)  Posterior = 0.5 * 0.6 / 0.8   = 0.375
```

On #4, I flip tails. Because the result is tails, we use P(T|F) = 0.5 (we have half a chance of tails with a fair coin). The Prior comes from our previous Posterior of 0.24. The Evidence comes from our first set of flips: we found we got 1 tails out of 5, so P(T) is 0.2. Tails pushes up the probability that we have a fair coin after all.


## Looping through the example in Chapter 4

Can I recreate the chart in 4-23 with this method?

In this situation we have two coins: one is fair and the other has a bias of 0.2 (meaning 20% of flips will result in heads). The point here is to select one of the two coins randomly and find out which coin we picked, knowing the bias of the rigged coin: we are supposed to find P(F|H).

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


## Lessons learned

To use a Bayes Loop to calculate a probability, you have to put a number value to your doubt or the bias you think is there is. This makes sense is a non-technical, narrative kind of way: if you have absolutely no doubt the coin is fair, then of course you have a 50/50 chance of heads or tails every single time. 

Your doubt should be captured in the Prior (the probability that the coin is fair) in the first test. The value for the Prior can be picked out of thin air, or you can use intuition or observations. 

After the first test, the Prior always comes from the previous Posterior value.

# Lingering doubts

It looks like it will also work in the first test with a Prior of 1 (meaning you assume the coin is fair) but Evidence (the probability of get any one result) that is not equal between all possible results. But then what do you use for Evidence for subsequent tests? Maybe you recalculate it based on actualy outcomes?

