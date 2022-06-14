# DS-Producao

![63b806b1494a7fbd9cb05271667b9c61](https://user-images.githubusercontent.com/55566708/173489469-0c468c00-291f-4bf5-8af2-a8676f0bd3a4.png)

## This project aims to create a model for the Rossmann store franchise where the focus is to project the total profit of each store for 6 weeks from now.


#### This project was made by Felipe S. Pedrosa.

# 1. Business Problem.
Rossmann's is a big European drugstore. Some store managers call me to help them to predict sales for the next six weeks.
The root cause is a demand from the CFO, discussed at their weekly meeting: he needed to plan store renovations, and for that, the budget needs to be aligned with each store's sales.
Therefore, the principal stakeholder is the CFO, but from which all store managers will benefit.

# 2. Business Assumptions.

All data was taken from the company's internal sales base of the last 30 months. Any data coming from before this period would be seriously affected by external events (biased).
Several details were provided, such as type of store, variety of products offered and the competition proximity. Other variable info such as customers per day and sales per day, holidays, marketing promotions were available too.
However, it was necessary to assume some things. As you can see down below.


- Conmpetition proximity: Was expressed in meters but, sometimes it was zero. So, 'Zero Competition Distance' was the same as 'No Competition Proximity'. But, for ML Algorithms this input is a bias. In this case, I assumed a fixed value (100,000 m) higher than the highest value in the dataset.

- Assortment: I assumed there is a hierarchy between types. So, stores with Assortment Type C must offer Types A and B too.

- Store Open: I removed all the lines that indicate Store Closed, as we also had Zero sales on the same day. For ML purposes, this will be reviewed in future CRISP cycle.

- Sales Prediction: In agreement with the CFO, I presumed they would provide the total sales for eatch store at the end of the sixth week.

# 3. Solution Strategy

My strategy to solve this challenge was:

**Step 01. Data Description:**
- My goal is to use statistics metrics to identify data outside the scope of business.

**Step 02. Feature Engineering:**
- Filter rows and select columns that do not contain information for modeling or that do not match the scope of the business.

**Step 03. Data Filtering:**
- Derive new attributes based on the original variables to better describe the phenomenon that will be modeled.

**Step 04. Exploratory Data Analysis:**
- Explore the data to find insights and better understand the impact of variables on model learning.

**Step 05. Data Preparation:**
- Prepare the data so that the Machine Learning models can learn the specific behavior.

**Step 06. Feature Selection:**
- Selection of the most significant attributes for training the model.

**Step 07. Machine Learning Modelling:**
- Machine Learning model training

**Step 08. Hyperparameter Fine Tunning:**
- Choose the best values for each of the parameters of the model selected from the previous step.

**Step 09. Convert Model Performance to Business Values:**
- Convert the performance of the Machine Learning model into a business result.

**Step 10. Deploy Modelo to Production:**
- Publish the model to a cloud environment so other people or services can use the results to improve the business decision. In this particular case, the model can be accessible from a Telegram Bot.

# 4. Top 3 Data Insights

**Hypothesis 01:**

**True/False.**

**Hypothesis 02:**

**True/False.**

**Hypothesis 03:**

**True/False.**

# 5. Machine Learning Model Applied

# 6. Machine Learning Modelo Performance

# 7. Business Results

# 8. Conclusions

# 9. Lessons Learned

# 10. Next Steps to Improve
- Build a pipeline to retrain model.
- Docker.
- More tests in ML algoritms.

# LICENSE

# All Rights Reserved - Comunidade DS 2021
