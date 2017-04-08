## Udacity Data Analyst Sample Interview Questions

by [Ankita Mehta](https://profiles.udacity.com/p/3853148787), as part of Udacity's [Data Analyst Nanodegree](https://www.udacity.com/course/nd002)

##### 1. Data Project Experience
> Describe a data project you worked on recently.

Ans: Recently I worked on project to use a data-set collected from homes in suburbs of Boston, Massachusetts (originated from [UCI Machine Learning Repository](https://archive.ics.uci.edu/ml/datasets/Housing)) and build a model which could be used to make the predictions of monetory values of houses. This project could be used by real estate agents who would require such information on a daily basis. The dataset had 506 enteries (data points) and 14 features such as average number of rooms in the neighbourhood, percentage of house owners, etc.

I used python's `sklearn` library and `sklearn.tree.DecisionTreeRegressor` model, also various machine learning techniques to perform this task. Intitally to build the model and perform evaluation on the data-set, it was divided into 80% training and 20% testing using `train_test_split ` from `sklearn.cross_validation`. 

Before building the actual model, I visualized the data using `visuals. ModelLearning` function in order to check the learning and testing performances on various subsets of training data. This was very interesting as I observed that the training and test score were very high, which made me learn that may the model suffers from high variance (or overfitting). I later performed grid search (with k-fold cross validation) technique to optimise the hyperparameters of learning algorithm. Finally after choosing the optimal `max_depth` of the tree, the model was built and predictions were performed. 

The overall model had a R^2 value as 0.77, i.e. the model had 77% accuracy.

##### 2. Probability
> Q2: You are given a ten piece box of chocolate truffles. You know based on the label that six of the pieces have an orange cream filling and four of the pieces have a coconut filling. If you were to eat four pieces in a row, what is the probability that the first two pieces you eat have an orange cream filling and the last two have a coconut filling?

> Follow-up question: If you were given an identical box of chocolates and again eat four pieces in a row, what is the probability that exactly two contain coconut filling?

Ans: The solution are provided as I would perform on a white-board:

![Solution for Q2 part 1](https://github.com/ankitameht/UdacityDataAnalystNanoDegree/blob/master/P8%20-%20Data_Analyst_Interview/Q2_1.jpg)

P(case 1) = 0.0714

Solution to the follow up answers:

![Solution for Q2 part 2](https://github.com/ankitameht/UdacityDataAnalystNanoDegree/blob/master/P8%20-%20Data_Analyst_Interview/Q2_2.jpg)

P(case 2) = 0.4285


##### 3. SQL Programming
> Q3: Given the table users:

>      Table "users"

| Column      | Type      |
|-------------|-----------|
| id          | integer   |
| username    | character |
| email       | character |
| city        | character |
| state       | character |
| zip         | integer   |
| active      | boolean   |

> construct a query to find the top 5 states with the highest number of active users. Include the number for each state in the query result. Example result:

| state      | num_active_users |
|------------|------------------|
| New Mexico | 502              |
| Alabama    | 495              |
| California | 300              |
| Maine      | 201              |
| Texas      | 189              |

Ans:

```
SELECT state, COUNT(active) as "num_active_users"
FROM users
GROUP BY state
HAVING active = TRUE
ORDER BY COUNT(active) DESC
LIMIT 5
```

##### 4. Data Structures and Algorithms Programming

> Q4: Define a function first_unique that takes a string as input and returns the first non-repeated (unique) character in the input string. If there are no unique characters return None. Note: Your code should be in Python.

Ans:

```
def first_unique(string):
	 string = string.lower()
	 unique_char = {}
	 for c in string:
	 	if c not in unique_char.keys():
	 		unique_char[c] = 1
	 	else:
	 		unique_char[c] += 1
	 l = list(unique_char.values())
	 if 1 not in l:
	 	return "None"
	 for c in string:
	 	if(unique_char[c]==1):
	 		return c
	 return "None"

> first_unique('aabbcdd123')
c

> first_unique('a')
a

> first_unique('112233')
None
```


##### 5. Data Analysis

> Q5: What are underfitting and overfitting in the context of Machine Learning? How might you balance them?

Ans: Overfitting is when a model is built that describes random error or noise instead of the underlying relationship. It performs extereemly well on a train data, however, it fails to generalise the relationship between features and target value. 

Underfitting occurs when the model that we are using is not able to capture the underlying trend of the data. For example, when fitting a linear model to non-linear data. 

Both overfitting and underfitting lead to poor predictions on new (test) data sets.

##### 6. Future Plan
> Q6: If you were to start your data analyst position today, what would be your goals a year from now?

Ans: 
I would like to apply to [Data Analyst Position at Microsoft](https://www.linkedin.com/jobs/view/258854419/)

Within one year, my goal are:

1. Understand nuts and bolts of every single relevant business tools related to big data and also Outlook services, especially for the ones implemented and used at WA, US.

2. Code fluently in Python to build new innovative ideas and make informed decisions for Microsoft. 

3. Develop new big data (large repo of mails and other documents) management product specifically for Outlook users. E.g an automate tool to calculate A/B testing result & experiement for a new features in Outlook.
