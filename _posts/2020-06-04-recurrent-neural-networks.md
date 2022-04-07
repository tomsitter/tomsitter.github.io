---
title: "Visualizing geospatial data"
date: 2022-01-15
categories:
  - blog
tags:
  - artificial intelligence
  - rnn
  - visualization
---


As a recent transplant to Vancouver Island, I've become aware of the controveries around Salmon farming here in the Pacific Northwest. Across British Columbia wild salmon populations are falling and there is an [open question](https://www.ctvnews.ca/sci-tech/sea-lice-outbreaks-put-b-c-s-salmon-population-at-risk-1.4429185) about whether, or how much, the sea lice on farmed salmon are transferring to wild salmon and contributing to this decline. Further searches showed that the predicting the prevalance and growth rates of sea lice in farmed salmon and the wild is difficult to model. I was curious about the data available to understand this relationship, and whether modern AI techniques have been used to study it. A scan through the literature didn't show anyone else using neural networks yet.

There are many papers in the literature trying to predict abundance using mathematical models, so I can read around to see what parameters others are using. From first glance the three that stand out to me are:
* Ocean temperature (which increases the rate of maturation of sea lice)
* Ocean salinity (higher salinity is correlated with decreased mortality)
* Salmon density (higher densities allow them to move from fish-to-fish more easily)

{% include figure image_path="/assets/images/salmonlouse.jpg" alt="And Salmon don't even have arms to pick them off" caption="Salmon louse -- gross" class="half" %}

I decided to poke around at the data sources to see if I can find something to train a neural network to predict sea lice populations, and discovered the follwing:
* The DFO regular posts sea lice populations at salmon farms across BC
* Lighthouses across the coast publish ocean temperature and salinity data


## Finding the fish farms and temperature readings

Doing a bit of googling, I was able to location the coordinates of all of the fish farms, as well as the location of a number of lighthouses across the coast of BC and Vancouver island. Fortunately, lighthouses report temperature and salinity data so they would be an excellent source of data. 

The first thing I need to do is see if the locations of the fish farms and lighthouses overlap enough that I can use some of them. I brought the coordinates into pydeck and plotted heatmaps around the points to get an idea of overlap. 

{% include figure image_path="/assets/images/lightstation_vs_farm_overlap.PNG" alt="Locations of fish farms in BC" caption="Locations of fish farms in BC. Lighthouses are in red and fish farms are in blue" %}

Unfortunately, it isn't great.  Lighthouses tend to be located on islands and points reaching out into the ocean, whereas fish farms are in sheltered inlets and in the Discovery Islands. Clearly I will need another source of data.

## Satellites to the rescue?

Another source of temperature and salinity data could be from satellite surveillance provided by the NASA PODAAC website. These are promising since there are freely available high resolution global temperature datasets (I am using one called [MUR-JPL-L4-GLOB-v4.1](https://doi.org/10.5067/GHGMR-4FJ04)). Browing through the literature indicates that these [may not be most accurate measures](https://www.frontiersin.org/articles/10.3389/fmars.2018.00121/full), but other [researchers have used them for predictions](https://podaac.jpl.nasa.gov/dataset/MUR-JPL-L4-GLOB-v4.1), so I'll have to give them a try.

{% include figure image_path="/assets/images/sst_example.PNG" alt="Sea Surface Temperature obtained from the " caption="Locations of fish farms in BC. Lighthouses are in red and fish farms are in blue" %}

## What's next?

My next step is to start processing this temperature and salinity data into a useful format so I can match it particular farms. I've also begun to look at the reported sea lice numbers, but work will be needed to get this into a readily analyzable format. Another question I have is what other metrics I can include in my dataset to help give my model a fighting chance. Stay tuned.

As for neural network architecture, I'm looking at a many-to-many recurrent neural network looks like both a fun and [powerful](https://karpathy.github.io/2015/05/21/rnn-effectiveness/) architecture. Furthermore, it caused me more issues than any other architecture during my class work, so it is work get more experience with. Yes, I know that most problems don't start with a solution.. but I'm doing this for my own learning as a primary goal, and to solve the sea lice problem as a hopeful outcome.

You can view my repository where I extracted and produced this data [here](https://github.com/tomsitter/sea-lice)