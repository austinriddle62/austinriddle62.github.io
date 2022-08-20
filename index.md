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


markdown
Syntax highlighted code block

# Header 1
## Header 2
### Header 3

- Bulleted
- List

1. Numbered
2. List

**Bold** and _Italic_ and `Code` text

[Link](url) and ![Image](src)
```

For more details see [Basic writing and formatting syntax](https://docs.github.com/en/github/writing-on-github/getting-started-with-writing-and-formatting-on-github/basic-writing-and-formatting-syntax).

### Jekyll Themes

Your Pages site will use the layout and styles from the Jekyll theme you have selected in your [repository settings](https://github.com/austinriddle62/austinriddle62.github.io/settings/pages). The name of this theme is saved in the Jekyll `_config.yml` configuration file.

### Support or Contact

Having trouble with Pages? Check out our [documentation](https://docs.github.com/categories/github-pages-basics/) or [contact support](https://support.github.com/contact) and we’ll help you sort it out.
