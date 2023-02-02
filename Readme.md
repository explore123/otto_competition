# OTTO competition 

[Otto on Kaggle](https://www.kaggle.com/competitions/otto-recommender-system/overview/description) 

Notebook for model training and creating submission can be run on [kaggle website](https://www.kaggle.com/code/explore12345/xgb-ranker-using-weights-from-covisitation-mat/notebook)

### Description in short:
  * "The goal of this competition is to predict e-commerce clicks, cart additions, and orders."
  * During one user session on website, user activities are logged
  * User behaviour is logged by logging: user clicks on items, user adding item to cart, user ordering item.
  * Test set is created by supplying only first part of user session, and the goal is to predict the second part of session. 
### Data in short:
  * Data consist of [session, aid, timestamp, type] columns (which coresponds to [user_id, item_id, user_action_type, timestamp]).
  * type value can be one of click, cart, order
  * session and aid are integer unique numbers.
  * timestamp is ordinary integer timestamp
  * train set consists of whole sessions, while test set sessions are stopped at some point and only first part is supplied
  * train set is rougly between 31.7.2022 and 28.8.2022., test set is between 28.8.2022. and 4.9.2022. (no overlapping)

  * Dataset consists of:
    * 12,899,779 sessions
    * 1,855,603 items
    * 216,716,096 events
    * 194,720,954 clicks
    * 16,896,191 carts
    * 5,098,951 orders

## What is done:
  * Cudf is used for data manipulation on GPU
  * XGBoost is used for training ranker models on GPU 

  1. For each session, 40 candidate items (more is better) are generated using handcrafted rules and covisitation matrices  
  2. For generated candidates various features are added and train, val, test sets are prepared
  3. XGBoost ranker models are created for each of event types to rank candidates (5 folds are used)
  4. Score is calculated for validation sets and final sumbission is created

## Thanks
* Thanks to <a href='https://www.kaggle.com/cdeotte'>Chris</a>, <a href='https://www.kaggle.com/radek1'>Radek</a>, and others that supplied knowledge, code, comments...