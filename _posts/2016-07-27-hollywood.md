---
layout: single
title: "Does Movie Genre Correlate to Revenue?"
excerpt: "Using machine learning on the film industry"
author_profile: false
category: 
  - projects
tags:
  - linear regression
  - metis
  - web scraping 
header:
  overlay_color: "#000"
  overlay_filter: "0.5"
  overlay_image: woods.jpg
---

The curriculum at Metis emphasizes applying the skills learned in class to projects that demand their use. This post is a detailed explanation of one of these projects.

## Part 1

### Objective
The goal of the project was to obtain film industry data and apply regression models to identify correlations and learn something about the industry. The skills required to execute this task are an understanding of web scraping and basic machine learning principles. When devising a problem statment, the first challenge I discovered was that the scope of the project would need to be broad. I had aspirations to look at the relative success of Pixar films, but with only 17 major releases at the time, that's simply not enough data to build a halfway decent machine learning model. In order to give myself an ample number of data points to work with, I opted to investigate whether film genre had any correlation with hollywood successs. The question now becomes, what's the best metric to rate success?

### Defining Success
The simplest way to determine how well a movie does is by its total gross. Domestic gross figures are readily available for almost every movie, and the major releases have foreign gross values as well. Finding further financial information is where things become difficult. Box Office Mojo, the source of most of the data used in this project, has production budgets for about half of its major films. I could not find any repositories containing marketing budgets, merchandising revenue, after-theater sales, and other information that would be useful in determing actual profits. As such, I'm left with the fact that the only metrics I can be predict are gross theater revenue and the ratio of that revenue over the production budget. This is not optimal, but domestic gross should be a good proxy for many of the other financial aspects of a film, and should serve the purposes of this project. I deemed it essential to convert past revenue figures to today's dollars. I did this by sticking to movies released since 1980 and converting the revenue figure based on average ticket price for each year. This method is slightly flawed, as a movie released on December 31st will get a different correction than one released on January 1st the following day,  but for the most part it should do well to normalize revenue data over the duration of time period examined.

### Determining Features
It was rather silly, but I found the use of the word "feature" to be non-intuitive during my first machine learning (ML) lecture. This is for anyone else who might be new to the field, but features are ML-speak for what I had traditionally thought of as variables or inputs. They are the attributes I will be using to predict the success of Hollywood films. Feature selection is an incredibly important part of building any regression or prediction model, and I won't elaborate on selection theory here, but the features I opted for are: genre, budget, domestic gross, MPAA rating, critical reception, runtime and release date. These features are relatively easy to acquire, which was a necessity given the two week time constraint on the project. Since my objective statement is determining whether genre is a predictive of revenue, it was critical to include a variety of other features to make sure genres were not serving as a surrogate for other, more important features.  
  
One feature inclusion that I debated was critical reception. I acquired and used movie ratings from Rotten Tomatoes, IMDB and Metacritic. There are interesting conclusions to be drawn from looking at the relationship between box office gross and reviews, but obviously you do not have this information prior to a film's release. Using this data was a personal admission that this project is for personal developement, and not for making geniune revenue predictions. As our teacher often stressed, "you'll never be able to tell me how exactly much a movie is going to make just by saying it's a PG-13 Action flick released in the summer." That sentiment nicely encapsualtes the limitations of this project, and would take on even greater meaning when I went about assessing regression models. However, no models can be built before the data is be acquired, and that proved to be a rather tricky proposition.

### Collecting Data
"Scraping" is a term used to describe extracting data from websites. As a first time participant in this process, I was very thankful for the prebuilt tools and libraries that made it manageable. All the data observed on a website is embedded within its HTML code. Google Chrome has an incredibly handy "Inspect" feature (found via a right-click) that lets you browse through HTML and get a feel for how the site is organized. A nice webscraping library called Beautiful Soup has been developed for python. Beautiful Soup creates Soup objects that can be parsed, searched, and maneuvered through conveniently to isolate and acquire information. The main source of data I used was [Box Office Mojo](http://http://www.boxofficemojo.com/ "Mojo"). This site contained all of the features I was looking to acquire outside of critical recepetion. The following is the bread-and-butter of retrieving HTML from a website and converting to a Soup object: 

```python  
response = requests.get(url) # requests a library for retrieving and reading HTML  
page = response.text  
soup = BeautifulSoup(page, "lxml") # BeautifulSoup stores the HTML in a soup object.  
```
My process for iterating through films on the Mojo website was based on the fact that the website is built through url templates. All I needed to do was acquire the unique movie title id located in each movie page's url. This process went as follows:  

  1. Get the list of genres sorted by number of movies in the genre.
  2. Iterate through a sorted version of each genre page to get the list of top 100 highest grossing films in the genre.
  3. Iterate through each film's page to retrieve data for that particular film.  

Data from each movie was stored in a dictionary, where the keys corresponded to eventual column names of the data frame. The dictionary of each movie was appended to a list with the dictionaries of all the movies. The biggest plight that I faced when running my script was caused by missing data leading to errors. I learned the value of setting up an error logger and using try/except clauses to identify and resolve any issues. Below is the simple error handling style I employed.

```python  
try:  
# Attempt to assign the domestic gross value.  
# The function money_to_int cleans up the string and converts it to an integer.  
    domestic_gross = money_to_int(soup.find('div', class_ = "mp_box_content").findAll('td', align = 'right')[0].text)  
    movie_data_dict['Domestic_Gross'] = domestic_gross # Put the domestic gross into the movie data dictionary.  
except:  
# If there's an issue retrieving the domestic gross, this will allow the script to keep running and create a record of the url that caused the issue.  
    with open('ErrorLog.txt','a') as efile:  
    efile.write('\nError domestic gross. Movie name: {}'.format(mov_url))  
```

The last issue to hurdle was getting timed-out by Box Office Mojo. With so many of my classmates also scraping their site, I had numerous scrape attempts get prematurely halted by HTTP request errors. My solution was to add a randomized delay in the python script, and to limit my scraping to no more than 1000 movies at a time. By the time the script was running smoothly I was already focused on getting the modelling finished, so I opted to cap my data collection at ~2200 movies from 29 different genres. The final piece of data, critical reception, was pulled from the API of the Open Movie Database. Once all of the data was collected and loaded into a Pandas dataframe, it was time to examine the relationship between features.  
  
To be continued...
