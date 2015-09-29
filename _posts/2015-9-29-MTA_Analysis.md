---
layout: post
title: MTA Exploratory Analysis and Agile Design
---

Week 1 @ [Metis](http://www.thisismetis.com/data-science "Metis Data Science Bootcamp") and our first project are in the books. Project benson (each project is cleverly named after a famous detective; the firsts' namesake being Oliva Benson of perennial NBC cop drama Law & Order: SVU) centered around using [MTA turnstile data](http://web.mta.info/developers/turnstile.html "Turnstile Data") as a vehicle to explore python's data exploration capabilities and the iterative design process.

#### The Problem

For project benson we were approached by WomenTechWomenYes (WTWY), a fictitious non-profit organization located in New York City whose mission is to increase the participation of women and technology.  The engagement centers around optimizing the deployment of their street marketing teams.  These teams serve dual purposes, to build reach and awareness for their cause and collect email addresses to distribute free tickets to their summer gala.  

#### Our Approach

Outside of the instructions to use the freely available MTA turnstile data, the assignment was fairly ambiguous (a common trend among data science problems).  Because of this, we approached this project using an agile/iterative design process. Contrary to the linear design process of 0. data > 1. problem > 2. analysis > 3. interface, an agile approach involves continual communication with clients, frequent deployment of software and rapid response to change.  The iterative design process starts with discussions with the client/user and understanding what problem they want to solve.  This is followed by brainstorming ideas for data sources/analysis methods and prototyping (the rougher the better to start) a solution which is then brought back to the user for feedback. Rinse and repeat.  Not only does this approach assure that we are providing the user/client with a product that they like, it also ensures that we are considering the product and user experience throughout every step of the analysis.

#### Data

We collected MTA turnstile data for 12 weeks (sprin through early summer) for our initial exploratory analysis.  The data consisted of snapshot cumulative entry and exit data for every turnstile for approximately every 4 hour period.  After a considerable amount of data munging was performed in python, we reviewed the data for reasonableness and dropped any nonsensical data points.  We also considered high-level/annecdotal data regarding the density of NYC tech companies.

#### Exploratory Analysis

We started with a macro view of total volume (measured by turnstile entries) over the entire 12 week period to examine which stations see the most foot traffic.  A bar chart of total volume **(displayed in full deck below)** reveals that the anecdotal major NYC “hotspots” that one may expect to be busy (ala Grand Central, Times Sq., Union Sq.) do have the most traffic flowing through the subways, however, some known NYC "tech hubs" such as FiDi and Flatiron are not represented.

From there we examined traffic by weekday.  Despite the amorphous blob of tourists that one might experience in NYC on the weekends, this analysis revealed that the heavy flow of commuter traffic into the city results in a higher volume of foot traffic.

Continuing to drill down, we wanted to see if there was a general peak time of day for subway use.  It turns out that there is no one-size fits all model for time.  Looking at an hourly time series for a typical day for 42nd - Times Sq. shows a spike from 4PM-8PM while the same timeseries for 34th - Penn Sta results in dual peaks from 8AM-10PM and 4PM-6PM.  Annecdotally, this makes sense.  Very few people actually live in Time Sq. so we wouldn't expect to see them getting on the subway there in the morning, but we would in the evening when they are returning home.  Penn Station is a major commuter hub so we do expect to see traffic flowing through in the AM (commuters from NJ or other parts of NY arriving and taking the subway to work) and the PM (commuters coming from other parts of NYC who work within walking distance of 34th St.).  The key takeaway here is that the most effective approach for choosing the most effect times to deploy a street team at a specific station is to follow the natural flow of the commuter.  

#### Where Can We Go From Here?

We presented a prototype for an interactive dashboard application that WTWY can utilize for their street team deployment planning/stategy **(displayed in full deck below)**.  The main page is a play off of the traditional subway map where station volume is displayed by the size of it's "stop dot".

What our subway volume analysis doesn't consider is WTWY's **target market**.  We want to make sure that the street marketing teams are reaching an audience who is interested in WTWY's cause.  Using data from digitalNYC, LinkedIn, Google Maps, etc. we can develop a heatmap for the density of tech companies and women's advocacy groups throughout the city to overlay over our subway map.

Combining these two data sets, we can drill into each station to get all of the metrics we need (avg. volume, volatility of volume, peak days, peak hours) along with lists of local tech and advocacy.  We can continue to drill into these local target markets to get information on the organization, a map showing the shortest distance from the station to it's location, and external links for more information.  These features can help WTWY plan for optimal street team placement (maybe it's more effective to approach someone a few blocks away from the station exit) as well as train their staff on their target market which can lead to more compelling conversations when approaching people on the streets.

Here is the full deck!  Enjoy!

<iframe src="https://docs.google.com/presentation/d/1TEaKuyUUKK1udw7p9WXhpaMkl53a8fdCrG45uoCJZpA/embed?start=false&loop=false&delayms=30000" frameborder="0" width="720" height="426.75" allowfullscreen="true" mozallowfullscreen="true" webkitallowfullscreen="true"></iframe>
