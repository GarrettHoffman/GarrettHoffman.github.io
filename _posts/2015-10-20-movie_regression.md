---
layout: post
title: As Seen on TV, Predicting Box Office Outcomes for Film Adaptations of TV Shows
---

Back in 2011, a very popular TV show called [Friday Night Lights](https://en.wikipedia.org/wiki/Friday_Night_Lights_(TV_series) "Friday Night Lights") was wrapping up it's final season.  As with all shows that rally cult followings, fans cried out for a follow up movie; but this one was different.  What this meant is that in it's lifetime as a story "Friday Night Lights" was a real life situation that inspired a book, which was turned into a movie, which became a TV show which could potentially become a movie again.  This is when I personally became interested in the "cross section" of pop culture.  I found myself thinking about questions like which shows are best suited to make the transition to the big screen?  I decided to examine this question for [Project Luther](https://en.wikipedia.org/wiki/Luther_(TV_series) "Luther") during weeks two and three @ [Metis](http://www.thisismetis.com/data-science "Metis Data Science Bootcamp").

[<img src="/assets/the_fugitive.jpg" title="The Fugitive"/>](https://github.com/GarrettHoffman/garretthoffman.github.io/tree/master)

#### Why Should We Care?

The Friday Night Lights anecdote is more than just a funny thing to think about; it makes a statement regarding the malleability of art.  Art can be squeezed into different mediums.  This is important to the film industry (studios, investors, producers, etc.) for a couple of reasons.  From a content perspective, the consumer market for movies has historically embraced transformation of pop culture.  In "Novels into Film: The Metamorphosis of Fiction into Cinema", George Bluestone expresses that 58% of top grossing films between 1994 and 2013 were adaptations.  From a marketing perspective, it is reasonable to believe that adaptations have a significantly smaller customer acquisition cost. Loyal fans' admiration of the characters and intrigue in plot arcs can be leveraged to gain a swift following for an adaptation.  

Many movies have been adapted in the past; some with great success (see "The Fugitive", "Star Trek: Into the Darkness", or "The Simpsons Movie") while others not so much (a la "Mystery Science Theatre 3000", "The Honeymooners" or "Leave it to Beaver"). So which ones should we choose to adapt?  Is it possible that we can predict which TV shows will make succesfull movies?

#### How Can We Do This?

For our first pass, we can approach this problem using **linear regression**, a [supervised learning](http://garretthoffman.github.io/hipster_game/ "The Hipster Game, or, a Very Serious Introduction to Core Concepts in Supervised Learning") technique, where our predictive relationship is defined using a function of the form **y** = **B<sub>0</sub>** + **B<sub>1</sub>** * f(X<sub>1</sub>) + **B<sub>2</sub>** * f(X<sub>2</sub>) + ... + **B<sub>n</sub>** * f(X<sub>n</sub>).  f(X*<sub>i</sub>*) is traditionally equal to X*<sub>i</sub>*, however, in some cases a different function may be a better fit (e.g. log(X*<sub>i</sub>*) or X*<sub>i</sup>*<sup>2</sup>). 

#### What Do We Know Already? (The Data)

Approximately 65 TV show adaptations were sampled.  This is a smaller sample size than we would normally like, however, it is not uncommon to come across problems with limited information available for analysis.  Data on the movies and corresponding TV shows was collected from Box Office Mojo, IMDB and Wikipedia using python web scraping tools such as **requests** and **beautiful soup**.

#### What Features Should We Consider? (Model Design)

First we need to define "success" for an adaptation.  Since linear regression is most effective on scalar variables, domestic box office gross was selected to quantify this.  This figure was inflation adjusted to 2015 movie ticket prices so that movies from all years can be compared with parity.

Now we need to consider which features or characteristics of the TV Show may be correlated with generating box office gross.  Additionally, we need to identify ways that we can quantify these as model inputs.  The following features were chosen:

* **Consumer Exposure**.  If someone is more aware of a TV show it can imply that they are more likely to buy a ticket to the movie.  Additionally, a long running show probably has a dedicated fan base who will see the movie despite the critical reception or expectations.  We can quantify this with the **number of episodes**.  We will use the log of this since it has a nicer distribution.  A scatter plot of log(episodes) against domestic gross, along with the distribution of each, is shown below.

[<img src="/assets/ep_scatter.jpg" title="The Fugitive"/>](https://github.com/GarrettHoffman/garretthoffman.github.io/tree/master)

* **Content Quality**.  It is reasonable to assume that the quality of content is a major reason that people indulge in the shows that they like.  If a critically acclaimed show is adapted into a movie, it will likely be accompanied by the perception of high quality.  Since so few shows win awards we will use **award nominations** to quantify quality (graph in full deck below).

* **Motivation Vehicle**.  One question I was always curious about surrounding adaptations is what feeling compels someone to see a movie more, nostalgia or hype/velocity?  Is it more effective for a studio to tug at the fondness of childhood memories or ride the momentum of a recent hit.  We can quantify this with a metric I'm calling **"distance"**, which is the length of time between the show premiere and the movie release (graph in full deck below).

* **Brand Perception**.  If a consumer has a certain perception of the network that distributes a TV show it can potentially impact their opinion of it.  Therefore, there may be an advantage of choosing shows from a certain network if popular opinion of it's quality is favorable.  For this reason we can explore **network** as a variable in our model.  A violin plot showing the distribution of domestic gross by distributor of the original TV show is shown below.

[<img src="/assets/net_violin.jpg" title="The Fugitive"/>](https://github.com/GarrettHoffman/garretthoffman.github.io/tree/master)

* **Animated vs. Live Action**. Are **animated** shows more successful on the big screen than live action?  This is an interesting feature as there can potentially be a few underlying drivers at play.  Shows geared towards children would generally fall into the animated category, however, some of the most succesfull animated TV adaptations are made for adults (South Park, The Simpsons).  It is also possible that the lack of necessity for plot continuity for an animated TV show may allow for easier development of a viable movie plot (graph in full deck below). 

#### So What Happened? (Model Results)

A single regression model containing all of these features resulted in the following coefficients:

[<img src="/assets/mod1_results.jpg" title="The Fugitive"/>](https://github.com/GarrettHoffman/garretthoffman.github.io/tree/master)

For our numeric variables this can be interpreted as the change in domestic gross for a unit increase in our variable (based on the fit of our training data).  For instance, for each award nomination, we would expect that domestic gross will increase by approximately 200K.  The coefficients of the categorical variables can be interpreted as the change in domestic gross based on the presence of that variable.  For example, a movie based on a show that was on HBO is expected to earn about 5.5M more at the box office than a show distributed by one of our "non-major" networks.

While this model gives us insights as to the trend of our historical data, it is not a particularly good model for predictive purposes.  The model has a **R<sup>2</sup>** value of .226, which means that only about 23% of the variation in domestic gross is explained by the model.  Expanding on this, when we consider the amount of features we are using the **adjusted R<sup>2</sup>** (adjusted for model complexity) is only .056.  Additionally, the only variable that is statistically significant is ABC (at a 90% confidence level) so we cannot say with any certainty that the variation in domestic gross due to any of the other variables is due to anything more than random chance.

As an alternative model, we can use **Lasso (or L1) Regularization** to refine our fit.  Regularization is a process of introducing an additional penalty for model complexity when fitting our model.  This is used to solve an ill-posed  problem or prevent overfitting (which we see when we have a large number of model features and few data points).  A unique result of Lasso Regularization is that the penalty will cause parameters of weaker predictors to be driven to zero and only the most relevant features remain.  Running the model with an L1-regularization results in the following coefficients:

[<img src="/assets/mod2_results.jpg" title="The Fugitive"/>](https://github.com/GarrettHoffman/garretthoffman.github.io/tree/master)

All of the parameters for our other predictors were reduced to zero, implying that episodes, awards, "distance" and ABC are the strongest model features.  This model performs slightly better with an adjusted R<sup>2</sup> of .121 but is still not great.  Despite the poor predictive power of our models, we shouldn't get discouraged; we can still extract some useful insights from our analysis.

#### What Do We Know Now and What Can We Do Next? (Key Takeaways and Potential Further Analysis)

So what can we take away from this analysis?

1. **ABC shows have historically been more successful.** The model suggests that movies adapted from ABC shows have historically been more successful in the box offices.  Of all the features examined this proved to be the only characteristic that was found to have a significant relationship.  While there are no guarantees, when comparing two projects it may be more effective to go with the ABC adaptation if all else is equal.

2. **Other key features show a positive relationship.**  The fit of the historic data implies that there is a positive relationship between consumer exposure, content quality and motivation vehicle.  This confirms what intuition tells us, however, there is not enough evidence to suggest that this isn't random.  

3. **Movies are complex.** There are many factors that go into a movie and financial success of an adaptation depends on more than simply the characteristics of the underlying TV show.

To refine this model we should consider incorporating features related to the movies themselves, such as budget, cast, director, etc.  Additionally, we may want to consider exploring other models.  It is likely that domestic gross has a non-linear relationship to our features so a different supervised learning technique, such regression trees (we will touch on these in a later post!) may be more appropriate.

Here is the full deck!  Enjoy!

<iframe src="https://docs.google.com/presentation/d/1zKbnIw1a6_vCtkgKDqLKiUhnlP52nPGaOC2tlIiNctE/embed?start=false&loop=false&delayms=3000" frameborder="0" width="720" height="426.75" allowfullscreen="true" mozallowfullscreen="true" webkitallowfullscreen="true"></iframe>