---
title: "Uncertainity"
date: 2025-12-01
draft: false
ai_tags: ["cs50", "ai", "notes"]
summary: "Deriving Results from Probabilities  - Notes on CS50AI Lecture 2"
---

Have you ever thought how Artificial Intelligence ranks websites on a browser, how genetics of a child are predicted? Week 2 of CS50’s AI course dives right into this idea, teaching us how to draw inferences from events which are not certain to happen or not happen, but have a probability to them.

### CS50AI-Lecture2 by David J.Milan and Bryan Yu
<iframe style="aspect-ratio: 16 / 9; height: 100% !important; width: 45vw;" src="https://www.youtube.com/embed/D8RRq3TbtHU?si=Ve-FAnv7ZX2hyXct" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>

<br>

In these notes, I discuss the key concepts from the course, from probability and its mathematical base, to bayesian networks, drawing inferences from them, sampling, markov models, etc. We also will look at how drawing inferences from probabilities allowed the co-founders of Google to create an algorithm to rank pages in their search results.


# Index
---
1. [The Concept of Probability](#what-is-a-search-problem)
2. [Bayesian Networks](#bayesian-networks)
3. [Inference](#inference)
4. [Sampling](#sampling)
5. [Markov Models](#markov-models)
6. [Hidden Markov Models](#hidden-markov-models)
7. [Page Rank System](#pagerank)
8. [Ending Note](#ending-note)
<br><br>

Usually, AI has to deal with uncertain variables from which it must draw inferences. It has certain environments where you can't know for sure, but you have certain probabilities for that event to happen in the environment.

If you look around, such situations exist everywhere, and these are the usual situations that AI has to work in. An example would be weather prediction, where the AI doesn't know for sure that certain events like rain, or cloudy skies will happen, but it has a sense of probability derived from past day's data and from which it can reason and draw what kind of weather would happen.

For this, we must first know about Probability, amd its mathematical base. 


# The Concept of Probability
---
 The base idea behind probability is that there are certain possible worlds for every situation. An example for this would be say a roll of dice, then a world would be where it comes up with 1, in another it comes up with 5, and so on. A possible world is denoted by ω. There is a certain chance that this possible world would exist is shown by P(ω).

 Now, certain rules that probabilities must follow are present. The first one being, 0 <= P(ω) <= 1. In other words, an event's chance of happening is always between 0 and 1. So, an event may happen for sure (1), and may not happen at all (0). All chances exist between them.

 Further, sum of the chances of each the possible worlds in the environment always results in 1. To understand it intuitively, we can understand this by saying that one of the worlds in the environment will happen for sure (1).

 The possibility for any ω to occur is shown by:
 > P(ω) = (Number of Worlds where ω occurs) / (Total number of possible worlds)

 When we consider such probabilities in an abstract, they are known as **Unconditional Probabilities**

 > Unconditional probability is the degree of belief in a proposition in the absence of any other evidence.

 But when we talk about AI, usually certain factors have to influence the probabilities. Thus, we are mainly dealing in **Conditional Probabilities**. 

 > Conditional probability is the degree of belief in a proposition given some evidence that has already been revealed.

 So, we have some evidence about the world. It can be expressed as **P(a | b)**

 Here, a is the event that we need probability of considering b has already occurred. Some examples include *P(it will rain today | it rained yesterday)*, or *P( the patient will have the disease | the patient's test results are there)*. 

 > Calculating Conditional Probability:
 >
 > **P(a | b) = P(a ∧ b) / P(b)**
 >
 >Intuitively, we can think of it in this way: we see all the worlds where both a and b are true, but only out of the worlds where b is true. 
 > 
 > Further, we can derive the following from this: <br>
 > **P(a ∧ b) = P(b)P(a | b)** or **P(a ∧ b) = P(a)P(b | a)** 
 > 
 > These equations represent join probability.

 Now, most of the time, we are not dealing in Boolean probabilities, we deal with probabilities faring between 0 and 1, leading to the creation of *random variable*.

 A random variable is a variable in Probability Theory with a domain of possible values it can take on. 

 For example: for a dice roll, the random variable *roll* can have a value of any number in the set {1,2,3,4,5,6}. 

 Or, for a random variable *weather*, it may be {sun, cloud, rain, wind, snow} in which each may have a different probability of happening. 

 A probability distribution is the probability for each of the random variable in its domain. The sum of all value in a probability distribution is 1.

 A probability distribution can be represented like this: **P(flight) = <0.6, 0.3, 0.1>** where the probabilities correspond to the flight being on time, delayed, or cancelled. So, there is a 60% chance that the flight will be on time, a 30% chance that it will be delayed, and a 10% chance that the flight will be cancelled. 

 ### Independent Events
 Independent events are the events in which knowing the result of one event doesn't change the result of another event. For example, we need to roll a die twice, now, we know that in the first roll we have a 5, that won't change the probability of getting a 5 in the second event.

 Now, we know that P(a   b) = P(a)P(b | a), but if a and b were independent, then a's result won't be influencing b, so P(b | a) would be equal to P(b), thus, we get that in independent events:

 **P(a ∧ b) = P(a)P(b)**

 ### Bayes' Rule
 A very important rule, Bayes' Rule is used for deriving inferences from Probabilities. 
 
 For deriving it we know that **P(a ∧ b) = P(b)P(a | b)** and **P(a ∧ b) = P(a)P(b | a)**, so, 

 **P(b)P(a | b) = P(a)P(b | a)**

 > Thus, 
 > 
 > **P(b | a) = P(b)P(a | b) / P(a)**

 Thus, if we know the probability of a, of b, and of a happening considering b has already happened, we can derive the probability of b happening, considering a has already happened. 

For example, we would like to compute the probability of it raining in the afternoon if there are clouds in the morning, or P(rain | clouds). We start with the following information:

- 80% of rainy afternoons start with cloudy mornings, or P(clouds | rain).
- 40% of days have cloudy mornings, or P(clouds).
- 10% of days have rainy afternoons, or P(rain).
Applying Bayes’ rule, we compute (0.1)(0.8)/(0.4) = 0.2. That is, the probability that it rains in the afternoon given that it was cloudy in the morning is 20%.

Knowing P(a | b), in addition to P(a) and P(b), allows us to calculate P(b | a). This is helpful, because knowing the conditional probability of a visible effect given an unknown cause, P(visible effect | unknown cause), allows us to calculate the probability of the unknown cause given the visible effect, P(unknown cause | visible effect). For example, we can learn P(medical test results | disease) through medical trials, where we test people with the disease and see how often the test picks up on that. Knowing this, we can calculate P(disease | medical test results), which is valuable diagnostic information.
 
### Joint Probability
Joint probability is the likelihood that multiple events happen. These are quite useful to compute the probability of an event which is influenced by multiple probability. 

Looking at this from the perspective of an example:
Let us consider the following example, concerning the probabilities of clouds in the morning and rain in the afternoon.

| C = cloud | C = ¬cloud |
| --- | --- |
| 0.4 | 0.6 |

| R = rain | R = ¬rain |
| --- | --- |
| 0.1 | 0.9 |

Looking at these data, we can’t say whether clouds in the morning are related to the likelihood of rain in the afternoon. To be able to do so, we need to look at the joint probabilities of all the possible outcomes of the two variables. We can represent this in a table as follows:

 
| | R = rain | R = ¬rain |
| --- | --- | --- |
| C = cloud | 0.08 | 0.32 |
| C = ¬cloud | 0.02 | 0.58 |

Now we are able to know information about the co-occurrence of the events. For example, we know that the probability of a certain day having clouds in the morning and rain in the afternoon is 0.08. The probability of no clouds in the morning and no rain in the afternoon is 0.58.

Using joint probabilities, we can deduce conditional probability. For example, if we are interested in the probability distribution of clouds in the morning given rain in the afternoon. P(C | rain) = P(C, rain)/P(rain) (a side note: in probability, commas and ∧ are used interchangeably). Thus, P(C, rain) = P(C ∧ rain)). In words, we divide the joint probability of rain and clouds by the probability of rain.

In the last equation, it is possible to view P(rain) as some constant by which P(C, rain) is multiplied. Thus, we can rewrite P(C, rain)/P(rain) = αP(C, rain), or α<0.08, 0.02>. Factoring out α leaves us with the proportions of the probabilities of the possible values of C given that there is rain in the afternoon. Namely, if there is rain in the afternoon, the proportion of the probabilities of clouds in the morning and no clouds in the morning is 0.08:0.02. Note that 0.08 and 0.02 don’t sum up to 1; however, since this is the probability distribution for the random variable C, we know that they should sum up to 1. Therefore, we need to normalize the values by computing α such that α0.08 + α0.02 = 1. Finally, we can say that P(C | rain) = <0.8, 0.2>.

### Some Miscellaneous Concepts
Now, we have certain rules of probability that are to be understood to efficiently solve and create probability algorithms.

The first one is **Negation**. When we talk about some probabilities, it is quite important that we know what would be the probability of the event not happening. This is what negation gives us. Negation is the concept that P(¬a) = 1 - P(a). This stems from the fact that the sum of the probabilities of all the possible worlds is 1, and the complementary literals a and ¬a include all the possible worlds.

The second one is **Inclusion-Exclusion**. When we want to know the probability of getting a world in which either of the events a or b, or both happen, we have the notation: P(a ∨ b) = P(a) + P(b) - P(a ∧ b). This can be interpreted in the following way: the worlds in which a or b are true are equal to all the worlds where a is true, plus the worlds where b is true. However, in this case, some worlds are counted twice. These worlds are the ones in which both a and b are true as they are included in both times. So, we subtract once the worlds where both a and b are true (as they were counted twice).
*Here is an example from outside lecture that can elucidate this. Suppose I eat ice cream 80% of days and cookies 70% of days. If we’re calculating the probability that today I eat ice cream or cookies P(ice cream ∨ cookies) without subtracting P(ice cream ∧ cookies), we erroneously end up with 0.7 + 0.8 = 1.5. This contradicts the axiom that probability ranges between 0 and 1. To correct for counting twice the days when I ate both ice cream and cookies, we need to subtract P(ice cream ∧ cookies) once.*

The third one is **Marginalization**. P(a) = P(a, b) + P(a, ¬b). The idea here is that b and ¬b are disjoint probabilities. That is, the probability of b and ¬b occurring at the same time is 0. We also know b and ¬b sum up to 1. Thus, when a happens, b can either happen or not. When we take the probability of both a and b happening in addition to the probability of a and ¬b, we end up with simply the probability of a.

Finally, we have **Conditioning**. P(a) = P(a | b)P(b) + P(a | ¬b)P(¬b). This is a similar idea to marginalization. The probability of event a occurring is equal to the probability of a given b times the probability of b, plus the probability of a given ¬b time the probability of ¬b.
<br><br>

# Bayesian Networks
---
When we want to consider structures formed by different events influencing the probabilities of other events, we use a Bayesian Network.

A Bayesian network is a data structure that represents the dependencies among random variables. It has certain properties as follows:
- They are directed graphs
- Each node on the graph represents a random variable
- An arrow from X to Y represents that X is a parent of Y. That is, the probability distribution of Y depends on the value of X.
- Each node X has Probability distribution P(X | Parents(X))
<br>

Let’s consider an example of a Bayesian network that involves variables that affect whether we get to our appointment on time.
<image src="/image/BayesianNetwork.png" style="width: 30vw;">

Let’s describe this Bayesian network from the top down: 
<br>

##### 1. Root Node: Rain
Rain is the root node in this network. This means that its probability distribution is not reliant on any prior event. In our example, Rain is a random variable that can take the values {none, light, heavy} with the following probability distribution:

| Rain  | Probability |
|-------|-------------|
| none  | 0.7         |
| light | 0.2         |
| heavy | 0.1         |
<br>

##### 2. Maintenance
Maintenance, in our example, encodes whether there is train track maintenance, taking the values {yes, no}. Rain is a parent node of Maintenance, which means that the probability distribution of Maintenance is affected by Rain.

| Rain  | Maintenance = yes | Maintenance = no |
|-------|------------------|-----------------|
| none  | 0.4              | 0.6             |
| light | 0.2              | 0.8             |
| heavy | 0.1              | 0.9             |
<br>

##### 3. Train
Train is the variable that encodes whether the train is on time or delayed, taking the values *{on time, delayed}*. Note that Train has arrows pointing to it from both Maintenance and Rain. This means that both are parents of Train, and their values affect the probability distribution of Train.

| Rain  | Maintenance | Train = on time | Train = delayed |
|-------|-------------|----------------|-----------------|
| none  | yes         | 0.8            | 0.2             |
| none  | no          | 0.9            | 0.1             |
| light | yes         | 0.6            | 0.4             |
| light | no          | 0.7            | 0.3             |
| heavy | yes         | 0.4            | 0.6             |
| heavy | no          | 0.5            | 0.5             |
<br>

##### 4. Appointment
Appointment is a random variable that represents whether we attend our appointment, taking the values {attend, miss}. Note that its only parent is Train. This point about Bayesian network is noteworthy: parents include only direct relations. It is true that maintenance affects whether the train is on time, and whether the train is on time affects whether we attend the appointment. However, in the end, what directly affects our chances of attending the appointment is whether the train came on time, and this is what is represented in the Bayesian network. For example, if the train came on time, it could be heavy rain and track maintenance, but that has no effect over whether we made it to our appointment.

| Train    | attend | miss |
|----------|--------|------|
| on time  | 0.9    | 0.1  |
| delayed  | 0.6    | 0.4  |
<br>

For example, if we want to find the probability of missing the meeting when the train was delayed on a day with no maintenance and light rain, or P(light, no, delayed, miss), we will compute the following: P(light)P(no | light)P(delayed | light, no)P(miss | delayed). The value of each of the individual probabilities can be found in the probability distributions ,above, and then these values are multiplied to produce P(no, light, delayed, miss).
<br><br>

# Inference
---
In Week-1 of CS50AI, we looked at inference through entailment. This means we could definitively conclude new information based on the information that we already had. But majority of the times, we dont have access to certain information and our model must deal with uncertainty. The method in discussion helps us to know information, not for certain, but backed by probability distributions for some values. This gives us the most probable outcomes for a certain set of events. Inference has multiple properties.

- Query X: the variable for which we want to compute the probability distribution.
- Evidence variables E: one or more variables that have been observed for event e. For example, we might have observed that there is light rain, and this observation helps us compute the probability that the train is delayed.
- Hidden variables Y: variables that aren’t the query and also haven’t been observed. For example, standing at the train station, we can observe whether there is rain, but we can’t know if there is maintenance on the track further down the road. Thus, Maintenance would be a hidden variable in this situation.
- The goal: calculate P(X | e). For example, compute the probability distribution of the Train variable (the query) based on the evidence e that we know there is light rain.

We are doing **Inference by Enumeration**.
<br><br>

# Sampling
---
Sampling is one technique of approximate inference. In sampling, each variable is sampled for a value according to its probability distribution. We will start with an example from outside lecture, and then cover the example from lecture.

To generate a distribution using sampling with a die, we can roll the die multiple times and record what value we got each time. Suppose we rolled the die 600 times. We count how many times we got 1, which is supposed to be roughly 100, and then repeat for the rest of the values, 2-6. Then, we divide each count by the total number of rolls. This will generate an approximate distribution of the values of rolling a die: on one hand, it is unlikely that we get the result that each value has a probability of 1/6 of occurring (which is the exact probability), but we will get a value that’s close to it.

> Here is an example from lecture: if we start with sampling the Rain variable, the value none will be generated with probability of 0.7, the value light will be generated with probability of 0.2, and the value heavy will be generated with probability of 0.1. Suppose that the sampled value we get is none. When we get to the Maintenance variable, we sample it, too, but only from the probability distribution where Rain is equal to none, because this is an already sampled result. We will continue to do so through all the nodes. Now we have one sample, and repeating this process multiple times generates a distribution. Now, if we want to answer a question, such as what is P(Train = on time), we can count the number of samples where the variable Train has the value on time, and divide the result by the total number of samples. This way, we have just generated an approximate probability for P(Train = on time).

We can also answer questions that involve conditional probability, such as P(Rain = light | Train = on time). In this case, we ignore all samples where the value of Train is not on time, and then proceed as before. We count how many samples have the variable Rain = light among those samples that have Train = on time, and then divide by the total number of samples where Train = on time.
<br><br>

# Markov Models
---
So far, we have looked at questions of probability given some information that we observed. In this kind of paradigm, the dimension of time is not represented in any way. However, many tasks do rely on the dimension of time, such as prediction. To represent the variable of time we will create a new variable, X, and change it based on the event of interest, such that Xₜ is the current event, Xₜ₊₁ is the next event, and so on. To be able to predict events in the future, we will use Markov Models.

**The Markov Assumption**

The Markov assumption is an assumption that the current state depends on only a finite fixed number of previous states. This is important to us. Think of the task of predicting weather. In theory, we could use all the data from the past year to predict tomorrow’s weather. However, it is infeasible, both because of the computational power this would require and because there is probably no information about the conditional probability of tomorrow’s weather based on the weather 365 days ago. Using the Markov assumption, we restrict our previous states (e.g. how many previous days we are going to consider when predicting tomorrow’s weather), thereby making the task manageable. This means that we might get a more rough approximation of the probabilities of interest, but this is often good enough for our needs. Moreover, we can use a Markov model based on the information of the one last event (e.g. predicting tomorrow’s weather based on today’s weather).

**Markov Chain**

A Markov chain is a sequence of random variables where the distribution of each variable follows the Markov assumption. That is, each event in the chain occurs based on the probability of the event before it.

To start constructing a Markov chain, we need a transition model that will specify the the probability distributions of the next event based on the possible values of the current event.

<image src="/image/Markov1.png" style="width: 30vw;"><br>

In this example, the probability of tomorrow being sunny based on today being sunny is 0.8. This is reasonable, because it is more likely than not that a sunny day will follow a sunny day. However, if it is rainy today, the probability of rain tomorrow is 0.7, since rainy days are more likely to follow each other. Using this transition model, it is possible to sample a Markov chain. Start with a day being either rainy or sunny, and then sample the next day based on the probability of it being sunny or rainy given the weather today. Then, condition the probability of the day after tomorrow based on tomorrow, and so on, resulting in a Markov chain:

<image src="/image/Markov2.png" style="width: 30vw;"><br>

Given this Markov chain, we can now answer questions such as “what is the probability of having four rainy days in a row?”.
<br><br>

# Hidden Markov Models
---
A hidden Markov model is a type of a Markov model for a system with hidden states that generate some observed event. This means that sometimes, the AI has some measurement of the world but no access to the precise state of the world. In these cases, the state of the world is called the hidden state and whatever data the AI has access to are the observations. Here are a few examples for this:

- For a robot exploring uncharted territory, the hidden state is its position, and the observation is the data recorded by the robot’s sensors.
- In speech recognition, the hidden state is the words that were spoken, and the observation is the audio waveforms.
- When measuring user engagement on websites, the hidden state is how engaged the user is, and the observation is the website or app analytics.


For our discussion, we will use the following example. Our AI wants to infer the weather (the hidden state), but it only has access to an indoor camera that records how many people brought umbrellas with them. Here is our sensor model (also called emission model) that represents these probabilities:

<image src="/image/Markov3.png" style="width: 30vw;"><br>

In this model, if it is sunny, it is most probable that people will not bring umbrellas to the building. If it is rainy, then it is very likely that people bring umbrellas to the building. By using the observation of whether people brought an umbrella or not, we can predict with reasonable likelihood what the weather is outside.

**Sensor Markov Assumption**

The assumption that the evidence variable depends only on the corresponding state. For example, for our models, we assume that whether people bring umbrellas to the office depends only on the weather. This is not necessarily reflective of the complete truth, because, for example, more conscientious, rain-averse people might take an umbrella with them everywhere even when it is sunny, and if we knew everyone’s personalities it would add more data to the model. However, the sensor Markov assumption ignores these data, assuming that only the hidden state affects the observation.

A hidden Markov model can be represented in a Markov chain with two layers. The top layer, variable X, stands for the hidden state. The bottom layer, variable E, stands for the evidence, the observations that we have.

<image src="/image/Markov4.png" style="width: 30vw;"><br>

Based on hidden Markov models, multiple tasks can be achieved:

- Filtering: given observations from start until now, calculate the probability distribution for the current state. For example, given information on when people bring umbrellas form the start of time until today, we generate a probability distribution for whether it is raining today or not.
- Prediction: given observations from start until now, calculate the probability distribution for a future state.
- Smoothing: given observations from start until now, calculate the probability distribution for a past state. For example, calculating the probability of rain yesterday given that people brought umbrellas today.
- Most likely explanation: given observations from start until now, calculate most likely sequence of events.


The most likely explanation task can be used in processes such as voice recognition, where, based on multiple waveforms, the AI infers the most likely sequence of words or syllables that brought to these waveforms.
<br><br>

# PageRank
---
When search engines like Google display search results, they do so by placing more “important” and higher-quality pages higher in the search results than less important pages. But how does the search engine know which pages are more important than other pages?

One heuristic might be that an “important” page is one that many other pages link to, since it’s reasonable to imagine that more sites will link to a higher-quality webpage than a lower-quality webpage. We could therefore imagine a system where each page is given a rank according to the number of incoming links it has from other pages, and higher ranks would signal higher importance.

But this definition isn’t perfect: if someone wants to make their page seem more important, then under this system, they could simply create many other pages that link to their desired page to artificially inflate its rank.

For that reason, the PageRank algorithm was created by Google’s co-founders (including Larry Page, for whom the algorithm was named). In PageRank’s algorithm, a website is more important if it is linked to by other important websites, and links from less important websites have their links weighted less. This definition seems a bit circular, but it turns out that there are multiple strategies for calculating these rankings.

#### **Random Surfer Model**

One way to think about PageRank is with the random surfer model, which considers the behavior of a hypothetical surfer on the internet who clicks on links at random. Consider the corpus of web pages below, where an arrow between two pages indicates a link from one page to another.

<image src="/image/PageRank1.png" style="width: 30vw;"><br>

The random surfer model imagines a surfer who starts with a web page at random, and then randomly chooses links to follow. If the surfer is on Page 2, for example, they would randomly choose between Page 1 and Page 3 to visit next (duplicate links on the same page are treated as a single link, and links from a page to itself are ignored as well). If they chose Page 3, the surfer would then randomly choose between Page 2 and Page 4 to visit next.

A page’s PageRank, then, can be described as the probability that a random surfer is on that page at any given time. After all, if there are more links to a particular page, then it’s more likely that a random surfer will end up on that page. Moreover, a link from a more important site is more likely to be clicked on than a link from a less important site that fewer pages link to, so this model handles weighting links by their importance as well.

One way to interpret this model is as a Markov Chain, where each page represents a state, and each page has a transition model that chooses among its links at random. At each time step, the state switches to one of the pages linked to by the current state.

By sampling states randomly from the Markov Chain, we can get an estimate for each page’s PageRank. We can start by choosing a page at random, then keep following links at random, keeping track of how many times we’ve visited each page. After we’ve gathered all of our samples (based on a number we choose in advance), the proportion of the time we were on each page might be an estimate for that page’s rank.

However, this definition of PageRank proves slightly problematic, if we consider a network of pages like the below.

<image src="/image/PageRank2.png" style="width: 30vw;"><br>

Imagine we randomly started by sampling Page 5. We’d then have no choice but to go to Page 6, and then no choice but to go to Page 5 after that, and then Page 6 again, and so forth. We’d end up with an estimate of 0.5 for the PageRank for Pages 5 and 6, and an estimate of 0 for the PageRank of all the remaining pages, since we spent all our time on Pages 5 and 6 and never visited any of the other pages.

To ensure we can always get to somewhere else in the corpus of web pages, we’ll introduce to our model a damping factor d. With probability d (where d is usually set around 0.85), the random surfer will choose from one of the links on the current page at random. But otherwise (with probability 1 - d), the random surfer chooses one out of all of the pages in the corpus at random (including the one they are currently on).

Our random surfer now starts by choosing a page at random, and then, for each additional sample we’d like to generate, chooses a link from the current page at random with probability d, and chooses any page at random with probability 1 - d. If we keep track of how many times each page has shown up as a sample, we can treat the proportion of states that were on a given page as its PageRank.

#### **Iterative Algorithm**
We can also define a page’s PageRank using a recursive mathematical expression. Let PR(p) be the PageRank of a given page p: the probability that a random surfer ends up on that page. How do we define PR(p)? Well, we know there are two ways that a random surfer could end up on the page:

With probability 1 - d, the surfer chose a page at random and ended up on page p.
With probability d, the surfer followed a link from a page i to page p.
The first condition is fairly straightforward to express mathematically: it’s 1 - d divided by N, where N is the total number of pages across the entire corpus. This is because the 1 - d probability of choosing a page at random is split evenly among all N possible pages.

For the second condition, we need to consider each possible page i that links to page p. For each of those incoming pages, let NumLinks(i) be the number of links on page i. Each page i that links to p has its own PageRank, PR(i), representing the probability that we are on page i at any given time. And since from page i we travel to any of that page’s links with equal probability, we divide PR(i) by the number of links NumLinks(i) to get the probability that we were on page i and chose the link to page p.

This gives us the following definition for the PageRank for a page p.

<image src="/image/PageRank3.png" style="width: 30vw;"><br>

In this formula, d is the damping factor, N is the total number of pages in the corpus, i ranges over all pages that link to page p, and NumLinks(i) is the number of links present on page i.

How would we go about calculating PageRank values for each page, then? We can do so via iteration: start by assuming the PageRank of every page is 1 / N (i.e., equally likely to be on any page). Then, use the above formula to calculate new PageRank values for each page, based on the previous PageRank values. If we keep repeating this process, calculating a new set of PageRank values for each page based on the previous set of PageRank values, eventually the PageRank values will converge (i.e., not change by more than a small threshold with each iteration). **This way, the inference by enumeration and bayesian networks allow the working of the browsers that we use everyday.**
<br><br>

# Ending Note
---
This post is part of my ongoing deep dive into **CS50’s Introduction to Artificial Intelligence with Python**, where I’m documenting my learnings, insights, and interpretations in a practical, simplified form.

If you’re also exploring AI — whether as a student, researcher, or just a curious mind — I’d love to connect and exchange ideas.

📬 Let’s connect on LinkedIn: [linkedin](https://www.linkedin.com/in/soham-gupta-b567b2274/)

More coming soon from future weeks of CS50AI. Stay tuned — and stay curious.
— *Soham Gupta*

> This post is based on ***[CS50’s Introduction to Artificial Intelligence with Python](https://cs50.harvard.edu/ai/2024/)*** — an open course by Harvard University taught by **[David J. Malan](https://cs.harvard.edu/malan/)** and **[Brian Yu](https://pll.harvard.edu/instructor/brian-yu/)**.
>
> You can explore the course materials **[here on GitHub](https://github.com/cs50)**.
