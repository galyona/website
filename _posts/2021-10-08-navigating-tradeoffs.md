---
layout: post
title:  "Navigating fairness-accuracy tradeoffs via disqualification"
author: "Gal"
---

If you know a little bit about algorithmic fairness, you know that group fairness metrics are a popular way to quantify the extent to which a given classifier is supposedly "fair".  But there are qualitatively different ways in which you can improve how a classifier fares under such metrics.

Consider the metric of *imbalance for the positive class*, measured as the difference between the expected scores of members from the first group with a positive label and the expected scores of members from the second group with a positive label (this can be thought of as the extension of the better-known Equal Opportunity metric to classifiers that output scores, not binary predictions). It can be brought to zero by either (a) outputting perfect predictions, (b) simply increasing the predictions of the disadvantaged group by a constant value.

So when you implement a fairness intervention and see that your fairness metric of interest has improved, how can you tell in which of these two worlds are you? An obvious hint is to look at what happens to, say, global accuracy. If you managed to improve fairness without a cost to accuracy you’re probably closer to world (a). Obviously, if you must choose between using the original (unfair) classifier and the new classifier, this makes the choice an easy one. But what if you end up improving fairness at some cost to accuracy? Such tradeoffs are common (e.g. for the reason described above). But how to actually navigate them?

Here’s a simple but concrete scenario:  you train a logistic regression classifier on the Adult Income dataset. You evaluate its performance (say measured via squared error between the true labels and the predicted scores on the test set): it has a loss of 0.149. But you care about fairness, so you see that the test imbalance between men and women is 0.11. Since this seems high, you also train a regularized ERM (adding an imbalance penalty to the usual objective) - this gives you a second classifier, with an improved imbalance of 0.051 but a slightly higher loss of 0.15.

Let's summarize: you have two classifiers: h (ERM classifier) with loss 0.149 and unfairness 0.11, and h’ (regularized ERM) with loss 0.15 and unfairness 0.051. Between h and h’, which would you choose?

The economic perspective (I think) would be to say that both of these classifiers are Pareto efficient, and so choosing between them depends on how much you value fairness relative to accuracy – and should be left to the relevant stakeholders to decide. But I would say that this is still hard to answer: the fairness improvement (here 0.11-0.051) and the loss deterioration (0.15-0.149) are not on the same scale, so how should a stakeholder (let alone one that doesn’t know the technical definitions of imbalance and squared loss…) decide?



In our new work, [“Consider the Alternatives: Navigating Fairness-Accuracy Tradeoffs via Disqualification”](https://arxiv.org/abs/2110.00813?context=cs.CY){:target="_blank"}, we take a stab at how to go about this. As the title suggests, we define the notion of *disqualification*, which is meant to capture the situation in which the existence of one classifier (say h’) should “disqualify” the use of another classifier (say h). We were inspired by the “disparate impact” doctrine, which instructs us to consider whether there were less discriminatory measures to achieve the same outcome in judging whether this outcome is fair.

Intuitively, disqualification exactly formalizes the logic we discussed above: h’ should disqualify h if by using h’ instead of h, we gain in fairness more than we lose in accuracy. So the remaining difficulty is appropriately scaling these two quantities. In the paper we reason about how we should approach this scaling from a more theoretical perspective. We look at two case studies based on the notion of accuracy we care about. To end with the example we've discussed throughout: when measuring accuracy based on the squared loss, we show that there is a natural scaling function which you should use, and that in the above scenario it leads to the following simple conclusion: *you should prefer h’ over h only if fairness is 20 times as important as accuracy*. Check out the paper itself for more details!
