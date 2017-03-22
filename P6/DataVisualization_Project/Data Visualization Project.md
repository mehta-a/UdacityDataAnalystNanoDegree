# Data Visualization Project
# Udacity Data Analyst Nanodegree
#### By Ankita Mehta

## Summary

I wish to demonstrate the growth of Facebook (in terms of active users) over the last decade and how it coincides their revenue, major feature launches and acquisitions. To do so, I collected a dataset for facebook with 'Year', 'FacebookActiveUsers', and 'Revenue' as the columns. I also highlighted some key feature launches and acquisitions.

## Design
Taking the last ten years data (2008-2017), I decided that it would be interesting to see Facebook's retention (in terms of number of active users) and their revenue growth. 

####Dataset collection
I realised that since this data was available over Facebook's wikipedia page; I created a csv dataset to store the information. In order to get the get the major feature launches and acquisition information, Facebook's website was my resort.

####Visualization design
Since this was a time series data, I opted for line and bar graph. I decided to use two y-axis to highlight the revenue, allowing me to simultaneously show revenue and retention (active users) growth in a single chart. Finally I decided to use dimple plot bubbles to show major events.

### Hand Sketch
The initial design was as follows:
![Hand Sketch](https://github.com/ankitameht/UdacityDataAnalystNanoDegree/blob/master/P6/DataVisualization_Project/data/initial.jpg)

This was my intial thought on the visualization. I would like to compare Number of active users as a bar graph and compare it with Number of Internet users worldwide (as line plot). My intention was to see if there are any unseen relevance between these. I felt I should include the data of last decade only and hence I planned not to include 2004 and 2005 Year's information.

### Coded Sketch - Take 1
My first sketch was to get any insights from Facebook's retention and Internet user's growth world wide.
![Take 1](https://github.com/ankitameht/UdacityDataAnalystNanoDegree/blob/master/P6/DataVisualization_Project/Take1.png)

This was my first attempt to make a plot using d3. I felt my inexperience with the language made the plot erroneous.

Anyhow, the attempt was to plot the bars represeting Facebook's Active users. I tried to plot a line to show the growth of internet users worldwide. 


(Details: https://bl.ocks.org/ankitameht/06563d6e65d34531afa78384b8ce4a4b)


### Coded Sketch - Take 2
After one self-reflection, I feel my visualization doesnt communicate much. I do have some insightful data to improvise this, which I felt I should be using. I made the following changes:

- Including the number of internet users worldwide distracts the users from the information I want to show. Hence, focussing only on Facebook's growth, I plot the revenue instead.
- Right y-axis scale is modified to represent Revenue instead of No of internet users.
- I use scatter plot and line plot combined in order to parallelly show both growth in terms of users and revenue.
- I decided to add few bubble highlights to point at major aqusitions and feature launches.
- I used interactive features of dimple and added colors to make it look appealing.
- I also include a facebook logo to add to user retention.

![Take 1](https://github.com/ankitameht/UdacityDataAnalystNanoDegree/blob/master/P6/DataVisualization_Project/Take2.png)

(Details: http://bl.ocks.org/ankitameht/0d1a77731efa88f4cc3ce731903830cb)

## Feedback

### Friend 1 Feedback

#### Friend 1 provided the following feedback after reviewing Take 1:
"Hi,
Your visualization looks great , but I think you should add some more description ( or rather a story) about the data that you are trying to present. Also can you provide some more info on the top most points in the x-axis? like what information is that axis representing, etc."

#### Friend 1 then provided the following feedback after reviewing Take 3:
I took this review seriously and added major changes in the plot as shown in take2.

### Friend 2 Feedback

#### Friend 2 provided the following feedback after reviewing Take 1:
"It looks pretty good and yeah it is easy to understand. Bars show the number of users. The line graph shows revenue. And the dots on top shows acquisition events"


### Udacity Forum Feedback
(Details: https://discussions.udacity.com/t/require-project-feedback/230618)

####Review 1
I posted my take 1 visualization on Udacity Forum and "vishy730" provided the following feedback:

"Hi @ankitamehta283,

The visualization looks great and nice selection of the graph. However, the objective of this project is to narrate a story.

You can add some description before the presentation to make it more interesting. Also you should highlight the trend present in the visualization to narrate the story."

####Critical Review
This was the critic by one of my technical friends - "The data is trying to correlate revenue, user base and key launches/acquisitions. However I feel that the three fields by themselves are not completely correlated. E.g.: total online population is not provided. Once Facebook reaches close to online global population, its growth is bound to flatline. Until recently Facebook did not had ads on its site. How was sales growing before that? Ideally for insights on Facebook's strategy, we should have assumed user base count as base and derived insights such as. Revenue per customer, Average like per user, Average photo upload per user, Average age of users, Average time spent per user."


I am glad that my friend was able to clearly understand correlations I am trying to portray in the visualization. Although, I agree to him to some extent, but I had some limitations in the visualizations which could not take care of the above points. Initially, I planned to add total no of internet users in the plot and per customer information, but I felt it was overwhelming for a reader. I wanted to keep the visualization simple and give a broad overview of facebook's growth. 
#####None-the-less, I will definitely work on a new visualization as my future work. 


## Resources
I referred multiple resources as listed below:

- https://newsroom.fb.com/news/
- https://newsroom.fb.com/company-info/
- https://en.wikipedia.org/wiki/List_of_Facebook_features
- https://www.statista.com/statistics/264810/number-of-monthly-active-facebook-users-worldwide/
- https://finance.yahoo.com/news/number-active-users-facebook--over-years-214600186--finance.html
- https://www.theguardian.com/news/datablog/2014/feb/04/facebook-in-numbers-statistics
- http://www.internetlivestats.com/internet-users/#definitions
- https://en.wikipedia.org/wiki/Facebook
- https://en.wikipedia.org/wiki/Timeline_of_social_media

Finally Udacity's course content on Data visualization helped me with technical knowledge.