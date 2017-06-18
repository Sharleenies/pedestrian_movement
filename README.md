# Analyzing Melbourne Pedestrian Data
Implemented as part of General Assembly's Data Science Immersive Capstone Project

For final notebooks and dataset, refer to *Part 4*, where each notebook is arranged in order of implementation.

Main data analyzed: Hourly Pedestrian count for each 42 location sensors obtained from data.melbourne.vic.gov.au

## Objective
Urban cities all over the world are aiming to make their cities more walkable and there are many reasons to do this, that is cultural, environmental, economic and so on. But what makes a city walkable? What patterns, if any, do pedestrians follow? What effect do major events in the city have on it?

 I've conducted my analysis across 4 different notebooks:
 
    * [One](../blob/master/Part4/1.Classification%20of%20Pedestrians%20(Flinders%20Street%20Most%20Popular).ipynb) Classification of Different Pedestrian Groups: Looking for any main patterns in pedestrian movement into the city area. Performed using: PCA and KNN

    * [Two](../blob/master/Part4/2.Classification%20of%20Pedestrians-Difference%20between%20sensors.ipynb) Classification of Different Areas: Looking for difference in pedestrian usage of different areas. Performed using: PCA 

    * [Three](../blob/master/Part4/3.%20Predicting%20Pedestrian%20Type%20by%20Businesses%20or%20Landmarks%20in%20the%20area.ipynb) Prediction and analysis of location features per Area Type found in Model 2. Performed using: LogisticRegression, LinearDiscriminantAnalysis, KNeighborsClassifier, DecisionTreeClassifier, GaussianNB, SVM, Ridge and Lasso Regularization, GridSearchCV.  Performed with surrounding landmarks and small businesses as my features.
    
    * [Four](../blob/master/Part4/4.Time%20Series%20(Monthly%20Sum).ipynb) Forecasting pedestrian trend in Melbourne and locating anomalies throughout the years. Performed using: Time Series and Count Vectorizer

## Summary
In order to determine whether or not pedestrians in Melbourne had any specific patterns, I chose to use unsurpervised clustering. This is generally performed when you are trying to find hidden patterns in your data and since I don't know what patterns or groups I have in my pedestrian data just yet, this was the perfect choice. 

With just pedestrian hourly count and the corresponding date time, each individual hour in time was used as my features. Using PCA, I was then able to find the most important hours in the day that described variances in my data the best.  Two PCs that explained 80% variance was found. After scatter plotting in PC space, two distinct groups emerged: Weekday and Weekend patterns. Weekday cluster followed an 8am and 5pm peak with a noon-time dip. Weekend cluster followed a steady rise towards noon-time lasting till about 4pm before gently falling. Any deviation from this trend corresponded to major events that disrupted the trend, commonly public holidays.

Knowing I have two specific pedestrian groups with different patterns, namely Commuters and Casual-walkers, I looked across all different areas to identify which were more Commuter-dominant.  Using PCA again, I was able to find these areas very well. In Melbourne, there were 10 locations out of the 42 that were Commuter-dominant. Note that commuter trends also show up in other areas but these 10 locations were the ones used by majority commuters.

The next question then was, if an area is commuter-dominant or casual-dominant, were there different characteristics of that area that drew different groups to it? Short answer: no. At least not with the features I used anyway, which were public facilities, cafes and restaurants, landmarks and transport stations in the area. My models all failed to give good results, even after GridSearch. One big reason is due to my small dataset in terms of the areas, I only had 42 areas to train my model on. Also, commuter path might be more determined by transport network than much else. (Something to look into in the next update)

Finally, since I wasn't able to find specific physical features of the area that drew pedetrians, I employed a time series model to find what events drew more crowds than usual. Drawing up a seasonal trend of peddestrian count throughout the years, I was able to pinpoint anomalies that diverged from this trend and match them to specific events happening during that period.

### Appreciation to and help from:
 * https://jakevdp.github.io/blog/2015/07/23/learning-seattles-work-habits-from-bicycle-counts/
 * https://www.analyticsvidhya.com/blog/2016/02/time-series-forecasting-codes-python/
 * https://www.kaggle.com/arthurtok/principal-component-analysis-with-kmeans-visuals
 
### Original links to all datasets:
Pedestrian data: https://data.melbourne.vic.gov.au/Transport-Movement/Pedestrian-volume-updated-monthly-/b2ak-trbp


Shops & Businesses: https://data.melbourne.vic.gov.au/Economy/Cafes-and-restaurants-with-seating-capacity/xt2y-tnn9


Landmarks: https://data.melbourne.vic.gov.au/Assets-Infrastructure/Landmarks-and-places-of-interest-including-schools/j5vt-ppat


Public Facilities: https://data.melbourne.vic.gov.au/Assets-Infrastructure/Street-furniture-including-bollards-bicycle-rails-/8fgn-5q6t/data


Employment Market: https://data.melbourne.vic.gov.au/Economy/Employment-by-block-by-industry/b36j-kiy4


Residential dwellings: https://data.melbourne.vic.gov.au/Property-Planning/Residential-dwellings/44kh-ty54


Crash Statistics: https://www.data.vic.gov.au/data/dataset/crash-stats-data-extract


Each site above has the related data dictionary and summary for reference.