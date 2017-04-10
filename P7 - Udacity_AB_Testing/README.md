## Design and Analysis of A/B Testing Questions

by [Ankita Mehta](https://profiles.udacity.com/p/3853148787), as part of Udacity's [Data Analyst Nanodegree](https://www.udacity.com/course/nd002)

##Introduction
Udacity is considering the change at the Udacity home page regarding the options available for students as: “start free trial” and “access coursematerials”. For this purpose a specific A/B test was performed. 

The goal of this project is to do the following:

1. Make design decisions for the A/B test, including which metrics to measure and how long the test should be run,
2. Analyze the results of the A/B test that was run by Udacity, and
3. Recommend whether or not to launch the change.

##Experiment Design
####Metric Choice
> List which metrics you will use as invariant metrics and evaluation metrics here. (These should be the same metrics you chose in the "Choosing Invariant Metrics" and "Choosing Evaluation Metrics" quizzes.)

+ Invariant metrics: Number of Cookies, Number of Clicks, Click-through-Probability
+ Evaluation metrics: Gross Conversion, Net conversion

> For each metric, explain both why you did or did not use it as an invariant metric and why you did or did not use it as an evaluation metric. Also, state what results you will look for in your evaluation metrics in order to launch the experiment.

1. **Number of cookies** (_Number of unique users to visit the course overview page_): I would use it as an invariant metric as it will consistent throught the experiment. The visit to the course overview page happen before the users see the experiment (“start free trial” option). Thus, it should an invariant metric and rather than a evaluation metric.

2. **Number of user-ids** (_Number of unique users who enroll in the free trail_): I would not use it for both evaluation & invariant metric. The number of users, who do not enroll in the free trial, will not be tracked, and thus should not be used as an invariant metric. This should not be used as an evaluation metric as this value does not have a denominator so it can't be normalized. If it could normalize like net conversion and retention, then it would have been a good evaluation metric.

3. **Number of Clicks** (_Number of unique cookies to click "start free trail" button (which happens before the free trial screen is trigger)_): This value is independent from the experiment just like the Number of cookies and thus I choose to use it as an invariant metric.

4. **Click-through-probability** (_Number of unique cookies to click "start free trail" button divided by the number of unique users who visited the course overview page_): Since both numerator and the denominator is consistent during the experiment, it makes sense that their division will also be consistent. Thus this is an invartiant metric instead of an evaluation metric.

5. **Gross Conversion** (_Number of user-ids to complete checkout and enrol in the free trial divided by number of unique cookies to click "start free trail" button_): This is a good evaluation metrics (and so it cannot be a good invariant metric) since this is directly dependent on the effect of the experiment. Expected is that the value will be lower in the experiment group because some people who are not able to commit more than 5 hours per week won't enroll the classes. where as, in the control group, users won't see any pop-up message so they will enroll without any consideration of the number of hours they can commit per week.

6. **Retention** (_Number of user-ids to remain enrolled past 14-day boundary (and thus make at least one payment) divided by the number of user-ids to complete checkout_): It is expected that fewer students enroll in the free trial in the experimental group, but possibly the number of paying students after 14 days to be unchanged or even increase. Thus this is a good evaluation metric rather than invariant metric.  However, I didn't choose  to use this as an evaluation metric for the test because it is redundant to Gross conversion and Net conversion.

7. **Net Conversion** (_Number of user-ids to remain enrolled past 14-day boundary (and thus make at least one payment) divided by the number of unique cookies to click on the "start free trial" button_): This is a good evaluation metric. It would be great if this value increases after the test; however, due to the expected decrease in number of students enrolling the free trial, it is possible that net conversion might decrease after the test. However, since the majority of the experiment group are those who can commit 5 hours per week and they are more likely to make the first payments for the course. So we want this value not to decrease after the test.

####Measuring Standard Deviation
> List the standard deviation of each of your evaluation metrics. (These should be the answers from the "Calculating standard deviation" quiz.)

Following is the standard deviation for the following:

+ **Gross Conversion**: 
	+ For 40000 page views: SE = SQRT(0.20625*(1-0.20625)/3200) (3200 clicks)= 0.00715
	+ For 5000 page views: SE = 0.00715*SQRT(40000/5000) = 0.02023
+ **Retention**:
	+ (Similar to above) SE = SQRT((0.53*(1-0.53)/660) * SQRT(40000/5000))) = 0.5494
+ **Net Conversion**:
	+  

> For each of your evaluation metrics, indicate whether you think the analytic estimate would be comparable to the the empirical variability, or whether you expect them to be different (in which case it might be worth doing an empirical estimate if there is time). Briefly give your reasoning in each case.

####Sizing
#####Number of Samples vs. Power
Indicate whether you will use the Bonferroni correction during your analysis phase, and give the number of pageviews you will need to power you experiment appropriately. (These should be the answers from the "Calculating Number of Pageviews" quiz.)

#####Duration vs. Exposure
Indicate what fraction of traffic you would divert to this experiment and, given this, how many days you would need to run the experiment. (These should be the answers from the "Choosing Duration and Exposure" quiz.)

Give your reasoning for the fraction you chose to divert. How risky do you think this experiment would be for Udacity?

##Experiment Analysis
####Sanity Checks
For each of your invariant metrics, give the 95% confidence interval for the value you expect to observe, the actual observed value, and whether the metric passes your sanity check. (These should be the answers from the "Sanity Checks" quiz.)

For any sanity check that did not pass, explain your best guess as to what went wrong based on the day-by-day data. Do not proceed to the rest of the analysis unless all sanity checks pass.

####Result Analysis
#####Effect Size Tests
For each of your evaluation metrics, give a 95% confidence interval around the difference between the experiment and control groups. Indicate whether each metric is statistically and practically significant. (These should be the answers from the "Effect Size Tests" quiz.)

#####Sign Tests
For each of your evaluation metrics, do a sign test using the day-by-day data, and report the p-value of the sign test and whether the result is statistically significant. (These should be the answers from the "Sign Tests" quiz.)

#####Summary
State whether you used the Bonferroni correction, and explain why or why not. If there are any discrepancies between the effect size hypothesis tests and the sign tests, describe the discrepancy and why you think it arose.

##Recommendation
Make a recommendation and briefly describe your reasoning.

##Follow-Up Experiment
Give a high-level description of the follow up experiment you would run, what your hypothesis would be, what metrics you would want to measure, what your unit of diversion would be, and your reasoning for these choices.
