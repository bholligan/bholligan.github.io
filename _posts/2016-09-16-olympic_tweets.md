---
layout: splash
title: "NLP with Olympics Tweets"
excerpt: "Applying topic and sentiment analysis to the closing ceremonies of the 2016 Summer Olympics."
author_profile: false
category: "projects"
tags: "nlp, metis, tfidf, svd, d3, twitter" 
bg: yellow
header:
  overlay_color: "#000"
  overlay_filter: "0.5"
  overlay_image: rio-small.jpg
---

At Metis we learned about natural language processing (NLP) and were given an opportunity to apply NLP concepts to a topic of our choice. With the Olympics in full swing at the time and dominating my Twitter feed, I was interested in seeing what an analysis of Olympic tweets would produce. I tend to follow comedians and sports bloggers on Twitter, and prior to this project I was inundated with jokes about Rio's unique brand of Olympic preparation that involved unfinished venues, sewage water, athlete robberies, and dead bodies washing ashore. On top of that, the time period I collected data was the final weekend that included the closing ceremonies, Usain Bolt running away with another 3 golds, USA basketball finally getting their act together, and Ryan Lochte bringing his lovable brand of public urination to Brazil. My expectation was to see the negative sentiment that populated my Twitter feed reflected among the a broader sample of Olympic-related tweets. I am aware that my Twitter experience is an echo chamber of people with similar beliefs, and I've long been intrigued to see how that compares to the greater public.  

The result of my project is a [d3 visualization](https://bholligan.github.io/olympicd3/ "d3") that shows the most popular topics on Twitter during the closing ceremonies of the games and their associated sentiment. Here are a few highlights:  
- You can clearly see when Tokyo 2020 was announced on the live broadcast and on the NBC tape-delay.
- It was interesting to see "sad" pick up in usage towards the end of the live broadcast.
- The laughing emoji stayed relatively constant, leading me to believe there were no particularly funny moments.
- The Brits use more positive terms than Americans when discussing their nation's Olympic team.

In summary, the pervasive negative sentiment I was expecting to see was not present during the closing ceremonies among tweeters using Rio hashtags. When aggregating tweets, generic subjects and feelings inevitability prevail, but mapping their relevance over time can provide insight about how the broad viewership is reacting. The sentiment analysis tool I used is a rudimentary system that struggled to provide value, especially when the topics themselves were defined by emotions such as "love" or "sad".

Here's [a link](https://github.com/bholligan/olympic_NLP/blob/master/Tweet%20Text.ipynb "Notebook") to my Jupyter Notebook showing how I used TF-IDF, truncated singular value decomposition, and sentiment analysis to acquire my results.

The javascript to build the d3 visual is [here](https://github.com/bholligan/bholligan.github.io/blob/master/olympicd3/index.html "Javascript").
