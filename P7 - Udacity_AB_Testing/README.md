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

6. **Retention** (_Number of user-ids to remain enrolled past 14-day boundary (and thus make at least one payment) divided by the number of user-ids to complete checkout_): It is expected that fewer students enroll in the free trial in the experimental group, but possibly the number of paying students after 14 days to be unchanged or even increase. Thus this is a good evaluation metric rather than invariant metric.  However, I didn't choose  to use this as an evaluation metric for the test because it is redundant to Gross conversion and Net conversion; this value can be calculated using Retention and Net Conversion. 

	Also it is not feasibile to run the experiment for longer duration. Consider for 4,741,212 page views and  40,000 page views per day, retention would be  = 4,741,212 page views / 40,000 page views per day = 119 days. This is a really long duration to run the experiment. Hence retention should be dropped as an evaluation metric.

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
	+ For 3200 clicks & 40000 pageviews: SE = SQRT(0.1093125*(1-0.1093125)/3200) = 0.00551.
	+ For 50000 pageviews: SE = 0.00715 * SQRT(40000/5000) = 0.0156 
	
> For each of your evaluation metrics, indicate whether you think the analytic estimate would be comparable to the the empirical variability, or whether you expect them to be different (in which case it might be worth doing an empirical estimate if there is time). Briefly give your reasoning in each case.

Gross Conversion and Net Conversion use the number of cookies as their denominators. This is a unit of diversion and it is same as a unit of analysis; thus, analytical estimate is comparable to the empirical variability.

####Sizing
#####Number of Samples vs. Power
>Indicate whether you will use the Bonferroni correction during your analysis phase, and give the number of pageviews you will need to power you experiment appropriately. (These should be the answers from the "Calculating Number of Pageviews" quiz.)

I did not use Bonferroni Correction during my analysis phase. The metrics in the test have high correlation (covariant) and the Bonferroni correction will be too conservative to it.

I realised that the amount of pageview for retention as evaluation metrics would need almost half-a-year for testing even if we direct 50% of traffic to that experiment, which is completely not a economic feasible timeline for a A/B Testing result. Therefore, I have iterate my evaluation metrics and use Gross Conversion and Net Conversion as evaluation metrics. Using [Evan Miller](http://www.evanmiller.org/ab-testing/sample-size.html), the result can be referred below:

```
Probability of enrolling, given click:
20.625% base conversion rate, 1% min d.
Samples needed: 25,835

Probability of payment, given click:
10.93125% base conversion rate, 0.75% min d.
Samples needed: 27,413 (chosen)

Therefore, pageview/group = 27413/0.08 = 342662.5
Total pageview = 342662.5*2 = 685325
Note:
- only 0.08 pageview leads to click.
- double pageview because we need total pageview for both experiment & control group
```

#####Duration vs. Exposure
> Indicate what fraction of traffic you would divert to this experiment and, given this, how many days you would need to run the experiment. (These should be the answers from the "Choosing Duration and Exposure" quiz.)

With daily traffic of 40000, I'd direct 80% of my traffic (32000) to the experiment, which means it would take us approximately 22 days (685325/32000 = 22) for the experiment. 

>Give your reasoning for the fraction you chose to divert. How risky do you think this experiment would be for Udacity?

Only 80% will be affected and the change due to the experiment is small, so it won't cause toomuch trouble in the overall business. The overall experiment is not very risky since there are nosensitive information we use in this experiment. Although users have to provide their credit cardnumbers when they enroll the course, these information are not part of the experiment.

The experiment should not affect whole operation of existing paying customers as well as highly motivated students (I'd suspect comprised the majority of the net conversion) and also would not affect Udacity content. Therefore, the whole experiment would not be considered as highly risky. However, I'd not direct all (100%) traffic to experiment. This is beacause due to the experiment Udacity will actively attempt to discourage certain students from signing up for a free trial, which could ultimately impact the company’s revenues. 
So a reduced ratio of 0.8 (80% traffic) will lead to a duration of 22 days, that is less than a month (which is what the client wants). So it is good amount ofduration.

##Experiment Analysis ([data](https://docs.google.com/spreadsheets/d/1Mu5u9GrybDdska-ljPXyBjTpdZIUev_6i7t4LRDfXM8/edit#gid=0))
####Sanity Checks
> For each of your invariant metrics, give the 95% confidence interval for the value you expect to observe, the actual observed value, and whether the metric passes your sanity check. (These should be the answers from the "Sanity Checks" quiz.)

+ Number of cookies:

 ```
PageViews (Control Group): 345543
PageViews (Experiment Group): 344660 
Total PageViews : 690203
Probability of Cookie in control or experiment group: 0.5
SE = SQRT(0.5*(1-0.5)*(1/345543+1/344660) = 0.0006018
Margin of error (m) = SE * 1.96 = 0.0011796
Confidence Interval = [0.5-m,0.5+m] = [0.4988,0.5012]
Observed value  = 344660/690203 = 0.5006
```

+ Number of clicks: 

 ```
PageViews (Control Group): 28378
PageViews (Experiment Group): 28325
Total PageViews : 56703
Probability of Cookie in control or experiment group: 0.5
SE = SQRT(0.5*(1-0.5)*(1/28378+1/28325) = 0.0021
Margin of error (m) = SE * 1.96 = 0.0041
Confidence Interval = [0.5-m,0.5+m] = [0.4959,0.5041]
Observed value  = 28378/56703 = 0.50046
```

+ Click Through Probability

	```
PageViews (Control Group): 28378
PageViews (Experiment Group): 28325
Total PageViews : 56703Pooled Probability = 0.0821540908979SE = 0.000661060815639Margin of error (m) = 0.00129567919865Difference = 5.66270915869e-05Confidential interval CI = (-0.0012956791986518956, 0.0012956791986518956) = [-0.0013, 0.0013]
Observed value = 0.0001
```

+ Results:

 ```
Number of cookies: [0.4988,0.5012]; observed .5006; PASS Sanity Check
Number of clicks : [0.4959,0.5041]; observed .50046; PASS Sanity Check
Clicks-through-probability : [-0.0013, 0.0013]; observed 0.0001; PASS Sanity Check
```

> For any sanity check that did not pass, explain your best guess as to what went wrong based on the day-by-day data. Do not proceed to the rest of the analysis unless all sanity checks pass.

	All Sanity checks passed.
	
####Result Analysis
#####Effect Size Tests
>For each of your evaluation metrics, give a 95% confidence interval around the difference between the experiment and control groups. Indicate whether each metric is statistically and practically significant. (These should be the answers from the "Effect Size Tests" quiz.)

Gross Conversion:

|               | Control Group | Experiment |
| ------------- | ------------- | ---------- |
| Clicks        | 17293         | 17260      |
| Enrolment     | 3785          | 3423       |
| Gross Conversion| 0.2188746892 | 0.1983198146 |
```
SE = 0.004371675385
m = SE * 1.96 = 0.00856848375
Pooled Probability = 0.2086
D hat = -0.02055
Confidence Interval = [-0.0291,-0.0120]

```
Result:

```
Gross conversion CI: [-.0291, -.0120]
- statistically significant (CI doesn't contain zero)
- practically significant (CI doesn't contain d_min value)
```

|               | Control Group | Experiment |
| ------------- | ------------- | ---------- |
| Clicks        | 17293 		  | 17260      |
| Enrolment     | 2033  		  | 1945       |
| Net Conversion| 0.1175620193  | 0.1126882966 |

```
SE = 0.003434133513
m = SE * 1.96 = 0.0067
Pooled Probability = 0.2086
D hat = -0.0049
Confidence Interval = [-0.0116, 0.0019]
```
Result:

```
Net conversion CI: (-0.0116, 0.0019)
- NOT statistically significant (CI contains zero)
- NOT practically significant (CI contain d_min = +/- 0.0075)
```

#####Sign Tests
> For each of your evaluation metrics, do a sign test using the day-by-day data, and report the p-value of the sign test and whether the result is statistically significant. (These should be the answers from the "Sign Tests" quiz.)

Gross Conversion:

```
Number of success: 4
Number of trials: 23
Probability: 0.5
Two-tailed p-value : 0.0026
```

+ p-value = 0.0026 < alpha level = 0.025. 
+ Therefore, we agree with the initial hypothesis, that the data is statistically significant.


Net Conversion:

```
Number of success: 10
Number of trials: 23
Probability: 0.5
Two-tailed p-value : 0.6776
```
+ p-value = 0.6776 > alpha level = 0.025. 
+ Therefore, we agree with the initial hypothesis, that the net conversion CI is both statistically insignificant.

#####Summary
> State whether you used the Bonferroni correction, and explain why or why not. If there are any discrepancies between the effect size hypothesis tests and the sign tests, describe the discrepancy and why you think it arose.

Bonferroni correction was not used because the metrics in the test has high correlation (high variance) and the Bonferroni correction will be too conservative to it. I completely comprehend the importance to correct if a test is launched and the metrics shows a significant difference, because it's more liely that one of multiple metrics will be falsely positive as the number of metrics increases. However, we would only launch if all evaluation metrics must show a significant change. In that case, there would be no need to use Bonferroni correction. In other words, correction is applied if we are using OR on all metrics, but not if we are testing for AND of all metrics.

##Recommendation
> Make a recommendation and briefly describe your reasoning.

I would recommend not to launch the experiment. The result of Gross Conversion showed statistically and practically significant changes after the pop-up message. This means that only those who are likely to commit more than 5 hours per week enroll the classes and they are more likely to make the first payments; this will reduce the costs of having those who are only taking free courses without making any payment. However, Net Conversion don't show statistically or practiclly significant changes after the test. This means that showing pop-up message to users before they enroll the classes don't affect the number of users who make their first payments after the free trial. Furthermore, the confidence interval of the net conversion includes the negative of the practical significance boundary which suggests the risk of hurting the Udacity's businiess.

##Follow-Up Experiment
> Give a high-level description of the follow up experiment you would run, what your hypothesis would be, what metrics you would want to measure, what your unit of diversion would be, and your reasoning for these choices.

I believe that one of the main reasons why students choose not to opt for course or cancel early in the course is due to the uncertainty of getting jobs after attaining the degree. Only if they have some guarantees of getting jobs, they would definitely continue enrolling the courses. 

Unfortunately the statistics of students of getting jobs after the course is difficult to measure because there isn't enough amount of data and it takes too long to gather such data. However, Udacity can give students some inspirations by showing some clips of students who enjoy taking the Nanodegree. 

For example, when a user checks the course structure of Data Analyst Nanodegree (say), they will see some clips of students who enjoy taking Data Analyst course. Clips can show students who don't have any experience in computer science or students who are just trying to learn more about the certain area of studies. In current Data Anayst Nanodegree, there is no such thing specific to data analyst nanodegree in the course structure page. I believe that showing the clips can motivate and inspire those who are considering to start the courses and it might increase the chance of reducing the number of students who cancel early in the course.

**Note**: This experiment could be first tested on a single nanodegree.

**Null Hypothesis**: Showing a clip of enrolled students (or Udacity alumni) at the course structure page will not increase the net conversion siginificantly.

**Alternate Hypothesis**: Showing a clip of enrolled students (or Udacity alumni) at the course structure page will increase the net conversion by a practically siginificant amount.

Clips will be assigned to users randomly by dividing users into two groups: control and experiment groups. In control group, everything stays the same and no clip will be shown in the course overview page. In experiment group, users will see clips when they visit the course overview page.

-**Unit of diversion** is unique number of cookies who watch the newly put clips. We are interested in the number of users who view full course structure, watch the clips and then click on "start free trial" button to enroll themselves. Thus those unique users who enroll after the browsing the course structure would be a good unit of divergence.

- **Invariant Metric**: The number of unique cookies, click (or watch clips) and click-through probability would be good invariant metric(s) because the value won't be affected by the test because users see the clips at the time they view the course structure.

- **Evaluation Metric**: Retention will be a good evaluation metric because this value tells us the ratio of the number of users who make first payments to the number of users who view full course structure and then click on "start free trial" button. We want to see statistically siginificant increases in experiment group.
