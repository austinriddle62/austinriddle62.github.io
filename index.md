## Austin Riddle's Personal Website

Hello, my name is Austin Riddle and I am based in the Salt Lake Valley. This website will demonstrate my capabilities when it comes to data analysis and showcasing my skills. 

### Project One: Automotive Brands and Customer Satisfaction

For this project, I found a dataset off of Kaggle provided by [Ayaz Lakho](https://www.kaggle.com/datasets/ayazlakho/carsdataset). 
My goal of this project was to find automotive brands with the highest satisfaction rate among customers from cars under $150,000 and from 2016 or newer. 

#### Process
Firstly, I separated the columns in excel by using the left() and right() functions. This helped me separate the year and brand name (the year, brand, model, and trim were all formatted together in one cell, like "2021 Ferrari SF90 Stradale Base"). I also added another column to make the average ratings a single number (for example, 4.2 was rounded to 4 and 3.6 was rounded to 3). 

After organizing the data, I decided to upload the CSV file to BigQuery (SQL) to sort and organize the data. I created a nested query in which the first query was to filter the data to any vehicle from 2016-2022 and under $150,000.
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
Next, I took this sorted information and uploaded it to Tableau to visualize it. 
I placed the average ratings for brands in descending order.

![Average Brands](https://user-images.githubusercontent.com/111258181/185814727-a927bf25-a30d-4650-b11c-1bf70e5a2b4f.png)

Of the top 10 rated brands, I found the average price and displayed them in descending order.

![Average Price of Top 10 Brands](https://user-images.githubusercontent.com/111258181/185814755-cc475f11-d6eb-401b-b9d3-0776c265bb0c.png)
