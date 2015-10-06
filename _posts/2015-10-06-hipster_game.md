---
layout: post
title: The Hipster Game, or, a Very Serious Introduction to Core Concepts in Supervised Learning
---

[<img src="/assets/hipstergame_banner.jpg" title="The Hipster Game, or, a Very Serious Introduction to Core Concepts in Supervised Learning"/>](https://github.com/GarrettHoffman/garretthoffman.github.io/tree/master)

A quick [Wikipedia](https://en.wikipedia.org/wiki/Hipster_(contemporary_subculture) "Hipster (contemporary subculture)") search for "Hipster" describes a person belonging to "The subculture described as a 'mutating, trans-Atlantic melting pot of styles, tastes and behavior' and that is broadly associated with indie and alternative music, a varied non-mainstream fashion sensibility (including vintage and thrift store-bought clothes), generally progressive political views, organic and artisanal foods, and alternative lifestyles."  But can we identify a Hipster based solely on appearance?  We asked this question to illustrate the core concepts of Supervised Learning.

**Supervised Learning** is is a machine learning technique where an algorithm is developed based on information that you already know.  That is, we have a set of data available to us where we know our input values (also known as **features**) and the outcome value (refered to as the **supervisory signal**) that we use to train our model.  In this case we were given 15 pictures of potential Hipsters and were told which ones did in fact reside in Williamsburg.  

[<img src="/assets/hipstergame_trainset.jpg" title="Hipster Training Set"/>](https://github.com/GarrettHoffman/garretthoffman.github.io/tree/master)

[<img src="/assets/hipstergame_trainhipsters.jpg" title="True Training Set Hipsters"/>](https://github.com/GarrettHoffman/garretthoffman.github.io/tree/master)

With this knowledge we can train a Supervised Learning algorithm (where the "machine" of machines learning is simply our brains), or set of rules.  Different groups took different approaches, some constructing a + or - points based system for Hipster and Non-Hipster qualities (such as clothes/style, facial hair, accessories, general "Hipsterness", etc.) and others using a classification technique to first identify the definite Hipsters and Non-Hipsters and then drilling down further on the tweeners.  Our group opted to construct a set of rules that systematically rules out the Non-Hipsters and classfies the leftovers as Hipsters.  The algorithm centered around style and demeanor and captured all of our known Hipsters and one known Non-Hipster (A6 above) which we decided not to add an additional rule to exclude (more on this later!).

[<img src="/assets/hipstergame_alg.jpg" title="Hipster Algorithm"/>](https://github.com/GarrettHoffman/garretthoffman.github.io/tree/master)

Now that we had our algorithm, we needed to test our model's fit using our test set.  A **test set** is a set of data that is used to assess the strength of a predictive relationship.

[<img src="/assets/hipstergame_testset.jpg" title="Hipster Test Set"/>](https://github.com/GarrettHoffman/garretthoffman.github.io/tree/master)

The test set is kept completely separate from the training set to insure that the model was fit independly of the data used to assess the model's utility (using your test set to train the model should elicit a feeling that all [GoT fans will recognize](https://media.giphy.com/media/l41lOCS45UvxvGsOQ/giphy.gif "Shame.")).  We applied our algorithm to the test set and got our results.

[<img src="/assets/hipstergame_alg_results.jpg" title="Hipster Algorithm Results"/>](https://github.com/GarrettHoffman/garretthoffman.github.io/tree/master)

Our model identified three Hipsters, but was it accurate?  

[<img src="/assets/hipstergame_testhipsters.jpg" title="True Training Set Hipsters"/>](https://github.com/GarrettHoffman/garretthoffman.github.io/tree/master)

We classified 2 Hipsters and 10 Non-Hipsters correctly, but misclassified 1 Non-Hipster as a Hipster (false positive) and 2 Hipsters as Non-Hipsters (false negatives).  The algorithm predicted Hipsters with 80% success, which appears pretty good at face value and slightly outperforms the most basic model of simply classifying everyone as Non-Hipster (73% success).  On the other end of the spectrum, if we added a 5th rule to our algorithm (e.g. has a forearm tattoo) to exclude the known Non-Hipster while training the model we could have miss-classified another Hipster in our test set.  This demonstrates examples of underfitting (not considering information we know about Hipsters' appearance) vs. Overfitting (creating a model that is too specific to our training set).

[<img src="/assets/hipstergame_results.jpg" title="Class Results"/>](https://github.com/GarrettHoffman/garretthoffman.github.io/tree/master)

After a very amusing exercise we came out with a few key takeaways:

* Supervised Learning involves creating a model based on information that we already know.
* When thinking about features that we want to include in our model, we have to consider how well something can be objectively quantified (e.g. how can we objectively define "general Hipsterness"?)
* The model should **always** be trained with one set of data and tested for accuracy on a separate set of data.
* As Data Scientists, we need to make design choices need to be made regarding the fit of the model. We have to consider underfitting and overfitting, between which lies a potential model that outperforms each extreme.