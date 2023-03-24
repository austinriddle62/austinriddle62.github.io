# Austin Riddle's Website and Portfolio 
Hello, my name is Austin Riddle and I am based in the Salt Lake Valley. This website demonstrates my capabilities when it comes to data analysis and showcasing my skills. 

## Project One: Point System
January 2023

My friend came to me with a business problem. They needed a way to keep track of points as a reward system for her employees. The goal of this point reward system was to give a set amount of points for weekly tasks and the team with the highest amount of points at the end of the week or month got a prize. 

### Excel Process

I started out in Excel creating a spreadsheet that listed all the tasks and the point amounts assigned to each one. I then made it so that they could input any amount of times the tasks were completed and it would automatically update the weekly and monthly point system. I used the SUM function to get the weekly points and the SUM IF function to get the monthly points. I broke up each team in to colors so I could use this function (=SUMIF(C10:R10,"Purple",C41:R41)) to get the monthly points. 

![Point_System_AE](https://user-images.githubusercontent.com/111258181/227423367-0e25e624-9171-4025-bc12-4bec715c8d06.png)

### Conclusion

Although this wasn't a lengthy or in depth project, it was a great experience coming up with a solution to solve a business problem with my excel skills. My friend benefited a lot from this point system and her employer and coworkers thoroughly enjoyed it. 

## Project Two: Automotive Brands and Customer Satisfaction
October 2022

For this project, I found a dataset off of Kaggle provided by [Ayaz Lakho](https://www.kaggle.com/datasets/ayazlakho/carsdataset). 
The goal of this project was to find automotive brands with the highest satisfaction rate among customers from vehicles under $150,000 and from 2016 or newer. 

### Excel Process

Firstly, I separated the columns by using the left() and right() functions. This helped me separate the year and brand name (the year, brand, model, and trim were all formatted together in one cell, like "2021 Ferrari SF90 Stradale Base"). I also added another column to make the average ratings a single number (for example, 4.2 was rounded to 4 and 3.6 was rounded to 3). 

### SQL Process

After organizing the data, I decided to upload the CSV file to BigQuery to sort and organize the data. I created a nested query in which the first query was to filter the data to any vehicle from 2016-2022 and under $150,000.

``` 
WITH target_data AS 
(SELECT year, brand, ratings_grouped, price
FROM `capstone-358715.New_Used_Cars.Organized_New_Used`
WHERE price <= 150000
  AND year >= 2016
)
SELECT brand, AVG(ratings_grouped) AS average_ratings_brand
FROM target_data
GROUP BY brand
ORDER BY average_ratings_brand DESC
LIMIT 10
```
### Tableau Process

Next, I took this sorted information and uploaded it to Tableau to visualize it. 
I placed the average ratings for brands in descending order.

![Average Brands](https://user-images.githubusercontent.com/111258181/185814727-a927bf25-a30d-4650-b11c-1bf70e5a2b4f.png)

Of the top 10 rated brands, I found the average price and displayed them in descending order.

![Average Price of Top 10 Brands](https://user-images.githubusercontent.com/111258181/185814755-cc475f11-d6eb-401b-b9d3-0776c265bb0c.png)

### Conclusion

Based off the results from this case study, I discovered that Land Rover had the highest rated satisfaction upon customers. I also came to the conslusion that if you want to buy a new vehicle from 2016 or newer, want something that is highly rated upon customers, but want to spend as least as possible, a Fiat will most likely fulfill your wants and needs. 

# Project Three: Superbowl Winning Teams and Draft Class Correlation
October 2023

For this project, I used two datasets off Kaggle provided by [CVIAXMIWNPTR](https://www.kaggle.com/datasets/cviaxmiwnptr/nfl-draft-19702021) and [Timo Bozsolik](https://www.kaggle.com/datasets/timoboz/superbowl-history-1967-2020). The goal of this project was to see if there was a correlation between a team in the NFL winning the Superbowl and that seasons draft class. 

### Excel Process

First I took the two datasets and formatted the years so I would be looking at the 1970-2020 draft class and Superbowl winners. I created a season column as well, since the draft year and year the Superbowl took place didn't align (for example the for the 2013 season, the Draft took place on 4/25/2013 and the Superbowl took place on 2/2/14). I then filtered the data to show the draft class of that years Superbowl champion and copied and pasted it into another dataset. 

### R Process

In RStudio, I decided to do more analysis and visualization. For the first part of my analysis, I wanted to see how many people were drafted on offense, defense, and special teams. 

``` 
# install packages
install.packages('tidyverse')
install.packages('dplyr')
install.packages('ggplot2')
# loading the data
unit <- read.csv('draft_superbowl.csv')
# changing the unit dataset
unit[unit == "C" | unit == "FB" | unit == "G" | unit == "OL" | unit == "QB" |
       unit == "RB" | unit == "T" | unit == "TE" | unit == "WR"] <- "Offense"
unit[unit == "CB" | unit == "DB" | unit == "DE" | unit == "DT" |
       unit == "ILB" | unit == "LB" | unit == "NT" | unit == "OLB" |
       unit == "S"] <- "Defense"
unit[unit == "K" | unit == "P"] <- "Special Teams"
# visualizing the unit data
ggplot(unit, aes(x=YEAR, fill=POSITION)) + geom_bar() +
  labs(title="Superbowl Winners and Their Draft Class",
       caption="Draft picks vary based on trade agreements among teams.",
       x="Year of Draft/Season", y="Count of Draftees") +
  annotate("text",x=1983,y=18,label="Only 26 Teams until 1976",
           color="black",size=2.5)
```

This code returned this visualization. 

![dft_sb_unit_graph](https://user-images.githubusercontent.com/111258181/187313006-6a112f3e-dc1e-4c7d-b29e-d27a581d16c6.png)

For the next part of the analysis, I wanted to see how many specific positions were drafted from 1970-2020. 

```
# install packages
install.packages('tidyverse')
install.packages('dplyr')
install.packages('ggplot2')
# loading the data
pos <- read.csv('draft_superbowl.csv')
# visualizing the position data
ggplot(pos, aes(x=POSITION)) + 
  geom_bar()+ 
  labs(title="Positions Drafted by Superbowl Winners 1970-2020",
       x="Position", y="Count of Draftees") + 
  geom_text(stat='count', aes(label= ..count..), vjust= -0.5)
```

This code returned this visualization. 

![dft_sb_pos_graph](https://user-images.githubusercontent.com/111258181/187094934-6d22d158-179d-46fe-96d9-56ec88276692.png)

### Conclusion 

From this project, I discovered that defensive backs are the most common to draft in the NFL, especially among Superbowl winnning teams. According to Dictionary.com, a defensive back (also known as a DB) is "a defender positioned off the line of scrimmage for the purpose of covering pass receivers and tackling runners who elude linemen and linebackers." Defensive backs include safties (S) and cornerbacks (CB) as well. Although defensive backs are able to play the corner back and safety position, some athletes specialize in one or the other. Although this may seem like it is skewing the results of the analysis since a defensive back is made up of two other positions, they are doing the same job, just in different areas of the field. In most cases, a defensive back can go from playing corner back to safety with ease. 
