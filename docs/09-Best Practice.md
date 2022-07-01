# ⭐Best practice and other insights

## 1. Is Anomaly Detection the Right Approach?

Not all of the problems you’ll find are solvable with anomaly detection. This implies three important things:

- You need a clear and unambiguous definition of the problem you’re trying to detect. It is also best if there are direct ways to measure it happening.
- The best indicators of problems are usually directly related to one or more business goals or desired outcomes. KPIs (key performance indicators) that relate to actual impact, in other words.
- To detect a more complicated problem, you might need to relate the system behavior to a known model, such as physical laws or queueing theory or the like. If you have no model that describes how the system should behave, how do you know that your definition of a problem is correct?

If you can get close to that, you might have a pretty good shot at using anomaly detection to solve your problem.



## 2. Start small, iterate quickly

- Start small: instead of taking the full data set, you're looking at a subsample. It's more valuable if you have a size of a data set which allows you to work very quickly, try out different ideas. And then only over time, when you think you can know this is the right thing, and you have to make more fine-grain decisions, then you can move up to the thing. Because one of the main points about data-driven projects is that all the truth in the data and, often, you don't really know-- you cannot know beforehand what it actually is that will work. So figuring out, actually, what it is that works, that's the most important thing. And don't fall into this trap of either trying too complicated things or building too much too early. 



## 3. Choose a Metric

It’s important to be sure that the problem you’re trying to detect has a reliable signal. It’s not a good idea to use anomaly detection to alert on metrics that looked weird during that one outage that one time. One of the things we’ve learned by doing this ourselves is that metrics are weird constantly during normal system operation. You need to find metrics (or combinations of metrics) that are always normal during healthy system behavior, and always abnormal when systems are in trouble. Here “normal” and “abnormal” are in comparison with the local behavior of the metric, because if there were a reliable global good/bad you could just use a threshold.

When it comes to real-world problems or business-related problems, is that you really need to know what it is, what you want to achieve. So **what is the metric?** What kind of performance is the performance level you actually need? you should, beforehand, know what is the expected level of performance that would be OK for the application so that you can also know, do I need more data, is this already good enough, and so on, and also how to measure it. And especially in some cases, in some cases, it might also be very clear like what the prediction, what the accuracy is you're looking for. 

Example metrics you could check include:

- Error rate
- Throughput
- Latency (response time), although this is tricky because latency almost always has a complex multi-modal distribution
- Concurrency, service demand, backlog, queue length, utilization, and similar metrics of load or saturation of capacity; all also usually have characteristics that are difficult to analyze with standard statistical tools unless you find an appropriate model



## 4. Evaluate properly

The labels and the evaluation metrics will help assess just how good the unsupervised models are at catching known patterns. Unsupervised learning systems are much harder to evaluate than supervised learning systems. Often, unsupervised learning systems are judged by their ability to catch known patterns. It’s important to be mindful of this limitation as we proceed in evaluating the results. With time series data where you have highly interdependent data, you really have to make sure that you're testing on the right thing.  You have to be really careful there to make sure that the estimate of the performance that you get from data analysis is the thing that you will also then see in the reality. 

## 5. Close the loop

In the company, data science is just one part. And eventually you want to bring data analysis to production. On the upper right hand side, we have the data science part, and on the lower side is the engineering part.  it's not a one-way road where you start with the data, you create your model, you bring it to production. But actually, then, the next round will be that how can we improve the model? So you should definitely, from the very beginning, already think of this whole like bigger iteration workflow between production and data science. 



## 6. Alarm Selectively

Anomaly detection methods and models don’t have enough context themselves to know if a system is actually anomalous or not. It’s your task to utilize them for that purpose. On the flip side, you also need to know when to *not* rely on your anomaly detection framework. When a system or process is highly unstable, it becomes extremely difficult for models to work well. We highly recommend implementing filters to reduce the number of false positives. Some of the filters we’ve used include:

- Instead of sending an alert when an anomaly is detected, send an alert when N anomalies are detected within an interval of time.
- Suppress anomalies when systems appear to be too unstable to determine any kind of normal behavior. 
- If a system violates a threshold and you trigger an anomaly or send an alert, don’t allow another one to be sent unless the system resets back to normal first. This can be implemented by having a reset threshold, below which the metrics of interest must dip before they can trigger above the upper threshold again.

Filters don’t have to be complicated. Sometimes it’s much simpler and more efficient to just simply ignore metrics that are likely to cause alerting nuisances.

# Conclusions

Although it’s easy to get excited about success stories in anomaly detection, most of the time someone else’s techniques will not translate directly to your systems and your data. That’s why you have to learn for yourself what works, what’s appropriate to use in some situations and not in others, and the like.

Our suggestion, store the results, but don’t alert on them in most cases. And keep in mind that the map is not the territory: the metric isn’t the system, an anomaly isn’t a crisis, three sigmas isn’t unlikely, and so on.
