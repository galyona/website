---
layout: post
title:  "The Tale of 1001 Black Boxes"
author: "Gal"
---


If you have internet access and a general interest in AI, you’ve stumbled upon the recent story of Amazon trying to build a machine learning algorithm (or the fancy term “AI”) to [automate its hiring process](https://www.reuters.com/article/us-amazon-com-jobs-automation-insight/amazon-scraps-secret-ai-recruiting-tool-that-showed-bias-against-women-idUSKCN1MK08G){:target="_blank"}, only to ditch it upon discovering that it penalized resumes that include the term “women’s” in it (e.g candidates who went to all women’s colleges).
<center>
https://twitter.com/mathbabedotorg/status/1050004919716106240
</center>

As with any seasonal “AI Gone Bad” news-story, it’s imperative to first bust some myths. The usual objection is typically of the following form: *“if graduates from women’s colleges really are less qualified, why should penalizing them count as discrimination?”*

Keeping in mind the context is crucial here. By using its own hiring records as the training data, Amazon wasn’t building an AI to learn how to hire successful candidates; all it could do, by definition, was build an AI that mimics it’s current hiring practices. This seems trivial, but this point is overlooked by many people. And this is where context comes in: Do we have any reason to believe that Amazon’s hiring practices are not biased?

It has long been established that as humans, our decision making is ridden with biases of all sorts. Specifically in the context of hiring in the tech industry, the common one is known as [“confirmation bias”](https://en.wikipedia.org/wiki/Confirmation_bias){:target="_blank"}. Early on we establish a few prototypes of success, and we tend to look for other people who fit these prototypes. When every “hire” is a costly investment, **tech companies are tempted to put much more emphasis on “exploiting” their current understanding of what makes successful candidates than “exploring”** (giving chances to other people, who don’t look like the prototypical successful candidate, to prove their skill).


Okay, we’ve established that ML is a black-box that will tend to perpetuate our own biases. What good could possibly come from this?

### Room for Optimism

My point is that real-world human decision making processes are *potentially* much worse than a *single* black box. The entity which we refer to as **“Amazon’s hiring process”** is composed of so many moving parts: it’s a hierarchy of recruiters, hiring mangers and interviewers — each with their own possible biases and quirks — who don’t necessarily follow one prescribed agenda. Figuratively speaking, **it’s a thousand black-boxes**.

This structure means that trying to tease out evidence of actual discrimination can be challenging; *every single hiring decision made by Amazon is always deniable on the basis of attributing it to one “faulty” box* (how many times have you read statements in the spirit of “it was just X,Y,Z; this doesn’t represent our companies’ policy”?).

And this is exactly why, with the right pair of glasses, the entrance of ML can be seen as a blessing in disguise. When human decision making becomes “algorithmic”, it *becomes* a well-specified mapping from inputs (individuals) to outcomes (decisions). Yes, this mapping could seem extremely complicated to us humans — a “black box”, for all we know — but at least it’s **one** such box.

By training a ML algorithm on its historical hiring decisions, Amazon captured the systematic aspects of it’s decision making process , those that go beyond a single decision. Amazon actually reduced its 1000 black boxes to just one. Now, careful inspection of this box (for example, by examining input-output pairs obtained by “feeding” individuals into the black-box, and observing the predicted outcome) can give a much more strong basis to hypotheses about the original, complicated entity which is Amazon’s hiring practices. In this case, it indeed revealed (or fulfilled speculation) that some aspects of it pose clear candidates of discrimination.

This is not to say that we should invoke machine learning in sensitive domains without care. Amazon’s story is one of many demonstrating that it is clearly a bad idea, and there’s a growing group of researchers (which I am extremely happy to be a part of) which are taking a closer look at these issues precisely. This was an attempt at saying that despite the plethora of negative results regarding all the “bad things” that ML can be an enabler of, we should remember that there’s a potential positive perspective: when used properly, algorithmification can serve as a tool to better understand and improve our own practices.
