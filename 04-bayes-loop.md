I had a lot of trouble understanding how to use Bayes Theorem in a loop according to the description in Chapter 4.

F = we have a fair coin
H = we flip a heads

P(F|H) = P(H|F) P(F) / P(H)

Posterior = Likelihood * Prior / Evidence


These ideas make sense:
- you pick a probability that you have a fair coin
- you use the outcome of test (posterior) as a parameter in the next test (the prior to be  exact)

What if I start out assuming the coin is fair? Let's try some flips.

Posterior = Likelihood * Prior / Evidence

When I flip heads, I'll use this version:
P(F|H) = P(H|F) P(F) / P(H)

For tails, I'll use this version:
P(F|T) = P(T|F) P(F) / P(T)


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


The probability of flipping heads is the sum of probabilities of flipping heads with either coin, divided by the number of coins:

P(H) = 0.5 + 0.2 / 2 = 0.35

The probability of flipping tails is figured similarly:

P(T) = 0.5 + 0.8 / 2 = 0.65

0. Let's assume a 50% chance of flipping heads or tails on the first flip; or maybe it's just that we have a 50% chance of picking the fair coin, so P(F) is 0.5, which I use as the prior for my first flip. Likelihood P(H|F) is always 0.5. The evidence is either P(H) 0.35 or P(T) 0.65, depending on what the flip results in.

1. I flip tails. So: 

Posterior = 0.5 * 0.5 / 0.65 = 0.385

The value for posterior is my new prior. 


2. I flip tails. The prior is 0.385, the previous posterior. Then: 

Posterior = 0.5 * 0.385 / 0.65 = 0.296

3. I flip tails. Posterior = 0.5 * 0.296 / 0.65 = 0.228

4. I flip tails. Posterior = 0.5 * 0.228 / 0.65 = 0.175  

5. I flip tails. Posterior = 0.5 * 0.175 / 0.65 = 0.135
 
6. I flip tails. Posterior = 0.5 * 0.135 / 0.65 = 0.104

7. I flip tails. Posterior = 0.5 * 0.104 / 0.65 = 0.08

8. I flip tails. Posterior = 0.5 * 0.08 / 0.65 = 0.062

9. I flip tails. Posterior = 0.5 * 0.062 / 0.65 = 0.048
    
10. I flip heads. Now we use P(F|H) = P(H|F) * P(F) / P(H).

Posterior = 0.5 * 0.048 / 0.35 = 0.069

12. I flip heads. Posterior = 0.5 * 0.069 / 0.35 = 0.099
     
13. I flip tails, back to P(F|T) = P(T|F) * P(F) / P(H)

Posterior = 0.5 * 0.099 / 0.65 = 0.076




This doesn't quite match the chart in 4-23.


So some lessons:

You have to capture your doubt in the evidence value in the Bayes Theorem. And evidence can be picked out of think air, or you can create some evidence with your intuition or observations.
