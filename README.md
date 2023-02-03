# DS-Produção

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


- **Conmpetition proximity:** Was expressed in meters but, sometimes it was zero. So, 'Zero Competition Distance' was the same as 'No Competition Proximity'. But, for ML Algorithms this input is a bias. In this case, I assumed a fixed value (100,000 m) higher than the highest value in the dataset.

- **Assortment:** I assumed there is a hierarchy between types. So, stores with Assortment Type C must offer Types A and B too.

- **Store Open:** I removed all the lines that indicate Store Closed, as we also had Zero sales on the same day. For ML purposes, this will be reviewed in future CRISP cycle.

- **Sales Prediction:** In agreement with the CFO, I presumed they would provide the total sales for eatch store at the end of the sixth week.

# 3. Solution Strategy

![img02-mod01-vid04-1](https://user-images.githubusercontent.com/55566708/186332188-267ab6c9-b3bb-4956-869b-cd89339d1cc1.png)


The project was developed based on the CRISP-DM methodology, that is, in a cyclical way we carry out the progress of each end-to-end stage of the project.


![img01-mod01-vid04-1](https://user-images.githubusercontent.com/55566708/186331887-fdbbc526-324b-4a64-b1f7-d0b873d87942.png)


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


# 4. Machine Learning Model Applied

My final choice of model was XGBoost.

ML step may be the most interesting step. There is were the 'magic' happens. Well, I tested four (4) Machine Learning Algoritms: Linear Regression, Lasso Regression, Random Forest Regressor and a XGBoost Regressor. The metrics applied to measure the performance of the algorithms were MAE, MAPE and RMSE.

So, the results from these metrics can be seen in the table below:

|      Model Name          |             MAE CV            |           MAPE CV       |           RMSE CV       |  
| -------------------------| ------------------------------|-------------------------|-------------------------|
|  Linear Regression       |       2082.46 +/- 295.78      |      30.26 +/- 1.66     |    2950.11 +/- 468.88   |
|  Lasso Regression        |       2116.65 +/- 341.58      |      29.2  +/- 1.18     |    3056.56 +/- 504.44   |
|  Random Forest Regressor |       837.7   +/- 219.23      |      11.61 +/- 2.32     |    1256.59 +/- 320.26   |
|  XGBoost Regressor       |       2889.54 +/- 343.25      |      34.54 +/- 1.39     |    3714.69 +/- 456.1    |


# 5. Machine Learning Modelo Performance


What !?!? Why did I choose XGBoost over Random Forest ? See the RMSE above !


Well, I did it because the company's policy is to do not go over the budget ($0.00).


All ML projects have to be lined with budget. Can the final model be sustained by the business infrastructure?


Do the results (direct or indirect) affect, or are affected, by any internal company policy?


In this case, the model will be hosted on a free cloud (Heroku), where we have a space limitation. If I choose random forest, the final model would be 1GB. Meanwhile, with XGBoost, the model became much smaller.


The metric problems can be solved in "Hyperparameter fine tuning" step.


Look the metrics after a better choice of parameters to train the model:

|      Model Name     |         MAE         |       MAPE%      |      RMSE      |  
| ------------------- | ------------------- |------------------|----------------|
|  XGBoost Regressor  |       764.9756      |      11.4861     |    1,100.7251  |


# 6. Business Results
It all appears to be good, beautiful ... but without converting these metrics in Business Words ... all the work can be ruined !
Business People don't understand RMSE. Maybe they understand MAE and MAPE, but 'cold' numbers they, certainly, understand. Graphics also help.


For example, the table below show the TOTAL of predictions. Considering the best and worst cenarios.

|      Scenario       |         Values      |  
| ------------------- | ------------------- |
|     predictions     |   R$283,256,128.00  | 
|    worst_scenario   |   R$282,266,876.81  |
|    best_scenario    |   R$283,945,369.96  |



Below we have a Scatter Plot with all the predictions. Notice that most are centered around a line parallel to the X axis (MAPE 11% in Y axis). However, there are points quite far apart. This is because there are stores for which the forecasts are not so accurate, while others are very assertive.

<img width="947" alt="scatter_plot" src="https://user-images.githubusercontent.com/55566708/186501125-077d531d-9d52-4ac6-8ba0-0c78f730b253.png">

Ok, but what does this deviation really represent?
Check the table below for the 5 best cases.

|         Store       |        predictions       |      worst_scenario      |      best_scenario      |         MAE          |        MAPE         |
| ------------------- | ------------------------ |--------------------------|-------------------------|----------------------|---------------------|
|         1089        |        373,394.1875      |        372,825.1184      |      373,963.2566       |       569.0691       |        5.3232       |
|         667         |        315,185.8438      |        314,693.4028      |      315,678.2847       |       492.4410       |        5.5487       |
|         323         |        282,916.4688      |        282,488.0610      |      283,344.8765       |       428.4077       |        5.6277       |
|         742         |        301,657.5312      |        301,199.1451      |      302,115.9174       |       458.3861       |        5.6393       |
|         1097        |        450,342.1562      |        449,703.2118      |      450,981.1007       |       638.9445       |        5.7761       |

And the table below with 5 worst cases.

|         Store       |        predictions       |      worst_scenario      |      best_scenario      |         MAE          |        MAPE         |
| ------------------- | ------------------------ |--------------------------|-------------------------|----------------------|---------------------|
|         292         |       108,359.7891       |        104,977.6086      |       111,741.9695      |      3,382.1804      |        60.2768      |
|         909         |       220,300.0781       |        212,395.1411      |       228,205.0152      |      7,904.9371      |        51.8675      |
|         876         |       194,060.8125       |        189,924.5347      |       198,197.0903      |      4,136.2778      |        33.7730      |
|         170         |       201,541.6875       |        200,194.4216      |       202,888.9534      |      1,347.2659      |        33.2923      |
|         749        |        206,800.9531       |        205,789.1920      |       207,812.7142      |      1,011.7611      |        28.3049      |



**Gráfico do real x predito**


![graph](https://user-images.githubusercontent.com/55566708/186514964-209511fc-ca54-4ff0-81a6-e91a69ed9003.png)


## Bot telegram with Results

https://user-images.githubusercontent.com/55566708/186500665-cd689c5b-67f5-44aa-9c6a-2101042b11ef.mp4



# 7. Conclusions

We finished the first cycle of CRISP, and this is the deliverable. There is still a world of possibilities to do and to be investigated, but this can be done in the next cycles.

# 8. Lessons Learned

- Metrics are important, but they are not everything;
- Make more graphics, make better graphics;
- Keep your code clean;
- Plan... and re-plan your work;
- Git is your friend.

# 9. Next Steps to Improve

- Build a pipeline to retrain model.
- Docker.
- More tests in ML algoritms.

# LICENSE

# All Rights Reserved - Comunidade DS 2021
