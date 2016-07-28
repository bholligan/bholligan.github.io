---
layout: splash
title: "Analyzing the Film Industry"
excerpt: "Practicing web scraping and linear regression."
author_profile: false
category: "projects"
tags: "linear regression, metis, web scraping" 
header:
  overlay_color: "#000"
  overlay_filter: "0.5"
  overlay_image: woods.jpg
---

Outline of this post:

- Goal of the project
- Defining Success
- Collecting Data
- Cleaning Data
- Features (what they are, why I wanted them) - Talk about this before regression?
  - Revisionist history with critic scores

A significant component of the curriculum at Metis is applying the skills learned in class to projects running concurrently. This post is a detailed explanation of one of the projects.

### Objective
The goal of the project was to obtain film industry data and apply regression models to identify correlations and trends. The skills required to pull this off are an understanding of web scraping and basic machine learning principles. When devising a project statment, the first challenge I discovered was that the scope of the project would need to be broad. I had aspirations to look at the relative success of Pixar films, but with only 17 major releases at the time, that's simply not enough data to build a halfway decent machine learning model. In order to give myself an ample number of data points to work with, I opted to investigate whether film genre had any correlation with hollywood successs. The question now becomes, what's the best way to define success?

### Defining Success
The simplest way to determine how well a movie does is by its total gross. Domestic gross figures are readily available for almost every movie, and the major releases have foreign gross values as well. Finding further financial information is where things become difficult. Box Office Mojo, the source of most of the data used in this project, has production budgets for about half of its major films. I could not find any repositories containing marketing budgets, merchandising revenue, after-theater sales, and other information that would be useful in determing actual profits. As such, I'm left with the fact that the only metrics I can be predict are gross theater revenue and the ratio of that revenue over the production budget. This is not optimal, but domestic gross should be a good proxy for many of the other financial aspects of a film, and should serve the purposes of this project.

### Determining Features
It was rather silly, but I found the use of the word "feature" to be initially non-intuitive during our first machine learning (ML) lecture. This is for anyone else who might be new to this field, but features are ML-speak for what I have traditionally thought of as variables or inputs. They are the attributes I will be using to predict the success of Hollywood films. Feature selection is an incredibly important part of building any regression or prediction model, and I won't elaborate on selection theory here, but the features I opted for are: genre, budget, domestic gross, MPAA rating, critical reception, runtime and release date. Since my objective statement is determining whether genre is a determining factor in revenue, it was important to include other, potentially  

### Collecting Data
"Scraping" is a term used to describe extracting data from websites. As a first time participant in this process, I was very thankful for the prebuilt tools and libraries that made the process manageable. All the data found on a website is embedded within its HTML code. Google Chrome has an incredibly handy "Inspect" feature (found via a right-click) that lets you browse through HTML and get a feel for how the site is organized. Within python there's a webscraping library called Beautiful Soup that creates Soup objects that can be quickly parsed through to isolate information. The main source of data I used was [Box Office Mojo](http://http://www.boxofficemojo.com/ "Mojo"). This site contains title, genre, revenue, release date, budget, director and more


