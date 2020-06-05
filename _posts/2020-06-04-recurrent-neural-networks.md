---
title: "Choosing a real world project to learn AI"
date: 2020-06-03
categories:
  - blog
tags:
  - artificial intelligence
  - rnn
  - learning
  - coursera
---

I've completed some course work, I've tinkered with tutorials, and now it is time to do a project that I can complete from start to finish. I want to get experience:
* Collecting data from various sources
* Cleaning, labelling, and transforming the data in an appropriate format
* Choosing an appropriate neural network archictecture
* Training and tuning a model
* Deploying a model

I want to choose a problem that hasn't been done before, and is sufficiently complex that it will take time to puzzle over. A more difficult problem will lead to greater learnings. My field of work is health informatics, so medical data would be the logical next step. However, medical data has two key problems for an experimental project : 1) is not the easiest to acquire due to privacy laws and 2) it often requires a medical professional to understand. I need a problem with data that is published online, and where I have access to experts that I can work with. 

My wife works for the Department of Fisheries and Oceans in Canada, working in regulation of farmed salmon, and she had mentioned that a hot issue in her field is the abundance of sea lice -- an aquatic parasite that can be found on both farmed and wild salmon. Across British Columbia wild salmon populations are falling and there is an [open question](https://www.ctvnews.ca/sci-tech/sea-lice-outbreaks-put-b-c-s-salmon-population-at-risk-1.4429185) about whether, or how much, the sea lice on farmed salmon are transferring to wild salmon and contributing to this decline. Perhaps I could create a neural network to help predict spikes in sea lice population so that farms have more advanced knowledge about when to treat for it. Okay, sure not the sexiest or hottest topic in the world.. but it seems to meet all the criteria: 
* Salmon farms publish data on sea lice populations on a regular basis
* I don't see any use of neural networks to predict abundance in the literature
* I can probe her colleagues for more information to help guide my work

{% include figure image_path="/assets/images/salmonlouse.jpg" alt="And Salmon don't even have arms to pick them off" caption="Salmon louse -- gross" class="half" %}

I'll need to decide what kinds of data to feed into my neural network to make predictions, and I'll need to choose an appropriate neural network architecture that can predict population growth. Fortunately, there are many papers in the literature trying to predict abundance using mathematical models, so I can read around to see what parameters others are using. From first glance the two that stand out to me are:
* Ocean temperature (which increases the rate of maturation of sea lice)
* Ocean salinity (higher salinity is correlated with decreased mortality)
* Salmon density (higher densities allow them to move from fish-to-fish more easily)

As for neural network architecture, I'm looking at a many-to-many recurrent neural network looks like both a fun and [powerful](https://karpathy.github.io/2015/05/21/rnn-effectiveness/) architecture. Furthermore, it caused me more issues than any other architecture during my class work, so it is work get more experience with. Yes, I know that most problems don't start with a solution.. but I'm doing this for my own learning as a primary goal, and to solve the sea lice problem as a hopeful outcome.