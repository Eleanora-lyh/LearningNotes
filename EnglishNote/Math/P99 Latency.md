## 1. Introduction

In this tutorial, we’ll study percentiles and their application to [network latency](https://www.baeldung.com/cs/graphs-network-diameter) and application response time.

## 2. Percentiles

**A percentile of a distribution or a sample is a value greater than the given [percentage](https://www.baeldung.com/cs/runtime-percentage-improvement) of observations in the same group**.

For example, if we say that Sam’s GRE score lies in the ![95^{th}](https://www.baeldung.com/wp-content/ql-cache/quicklatex.com-7e29aa9692b967e1047038585fbd2df6_l3.svg "Rendered by QuickLaTeX.com") percentile, then we want to say that Sam has performed better than ![95\%](https://www.baeldung.com/wp-content/ql-cache/quicklatex.com-9779796b1f3b96e67133dbdcbdb63339_l3.svg "Rendered by QuickLaTeX.com")of all GRE test givers.

So, we use percentiles to express how a given value compares to others in the same set. The following figure illustrates ![95^{th}](https://www.baeldung.com/wp-content/ql-cache/quicklatex.com-7e29aa9692b967e1047038585fbd2df6_l3.svg "Rendered by QuickLaTeX.com")  and ![99^{th}](https://www.baeldung.com/wp-content/ql-cache/quicklatex.com-280bf65da28558df05ad6fb1e928fdba_l3.svg "Rendered by QuickLaTeX.com") percentile for a normal distribution of a test score with mean value ![\mu =720](https://www.baeldung.com/wp-content/ql-cache/quicklatex.com-a42114167962799993a07621ca1aa02a_l3.svg "Rendered by QuickLaTeX.com") and  standard deviation ![\sigma = 30](https://www.baeldung.com/wp-content/ql-cache/quicklatex.com-829824974c5a466ff62e30ca26b843ef_l3.svg "Rendered by QuickLaTeX.com"):

![](C:\Users\v-liuyuhang\myprojects\LearningNotes\EnglishNote\imgs\2025-05-29-14-08-12-image.png)

As evident in the figure, the ![95^{th}](https://www.baeldung.com/wp-content/ql-cache/quicklatex.com-7e29aa9692b967e1047038585fbd2df6_l3.svg "Rendered by QuickLaTeX.com") percentile value is 769.3, and the ![99^{th}](https://www.baeldung.com/wp-content/ql-cache/quicklatex.com-280bf65da28558df05ad6fb1e928fdba_l3.svg "Rendered by QuickLaTeX.com") percentile value is 789.8.

**More formally, the** ![\mathbf{k^{th}}](https://www.baeldung.com/wp-content/ql-cache/quicklatex.com-cf8022523ee7c58e4ec642be40846946_l3.svg "Rendered by QuickLaTeX.com") **percentile of a distribution (**![\mathbf{k=1,2,\ldots,100}](https://www.baeldung.com/wp-content/ql-cache/quicklatex.com-f31deaac618226258060660bd165eb0a_l3.svg "Rendered by QuickLaTeX.com")**) is greater than or equal to** ![\mathbf{100}](https://www.baeldung.com/wp-content/ql-cache/quicklatex.com-a4dcadd45624c87539400a416ae5ffca_l3.svg "Rendered by QuickLaTeX.com") **% of values in the same distribution.**  We can calculate the percentile of a finite sample, in which case we’re talking about the sample estimates, not distributional percentiles.

### 2.1. Percentile vs. Percentage

Percentile is not the same as percentage.The key difference is that a percentage is a part of a unit, whereas a percentile is a value that a specific percentage of other values from the same group is smaller from.

- 比如你在第 90 百分位，意思是：在这组数据中，有 90% 的值比你小（或等于你）。
- 它不是比例，而是一个**数据点**，这个数据点把数据集分成了“前 90%”和“后 10%”。

## 3. Latency Percentiles

**We define latency as the total time it takes for a data packet to travel from its origin to its destination.** We usually refer to latency in the context of a network. Network latency is one of the key values we use to define the quality of service that a provider offers to a customer. We usually measure latency in milliseconds.

The lower the latency, the better the user experience.

### 3.1. P99 Latency

We usually describe latency with its 99th percentile or P99.

**So, if we say that our [HTTP-based web application](https://www.baeldung.com/cs/rest-vs-http) has a P99 latency of less than or equal to 2 milliseconds, then we mean that** ![\mathbf{99}](https://www.baeldung.com/wp-content/ql-cache/quicklatex.com-466ce34ea75500be67cf5e8371403366_l3.svg "Rendered by QuickLaTeX.com") **% of web calls are serviced with a response under 2 milliseconds.** Conversely, only ![1\%](https://www.baeldung.com/wp-content/ql-cache/quicklatex.com-88e1f5bcc16908e58a5a4ad948617c4a_l3.svg "Rendered by QuickLaTeX.com") of calls get a [delayed response](https://www.baeldung.com/cs/propagation-vs-transmission-delay) of over 2 milliseconds.

### 3.2. Why P99 Latency?

People often use basic statistical measures such as the minimum, mean, median, or maximum value to describe a data set. The problem with these statistics is that they may be bad at describing data. **The mean and median often mask outliers, whereas minimum or maximum may give us an outlier.**

**Network administrators aim to optimize the** ![\mathbf{99^{th}}](https://www.baeldung.com/wp-content/ql-cache/quicklatex.com-4eabeff0445b73e862f899f96a060c10_l3.svg "Rendered by QuickLaTeX.com") **percentile of network latency to improve the overall response time with peak load.** They also use percentile-based alerts for monitoring as these don’t have high false-positive rates. Also, such alerts are a lot less volatile and thus depict important performance degradation events.

So, the P99 latency is greater than almost all latencies, so optimizing it is like maximizing the performance in the worst case. However, since P99 isn’t the maximal value, we expect it not to be influenced by outliers.

## 4. Percentile Calculation

Let’s say we have a dataset ![d](https://www.baeldung.com/wp-content/ql-cache/quicklatex.com-b7950117119e0530b9b4632250a915c5_l3.svg "Rendered by QuickLaTeX.com") of ![n](https://www.baeldung.com/wp-content/ql-cache/quicklatex.com-ec4217f4fa5fcd92a9edceba0e708cf7_l3.svg "Rendered by QuickLaTeX.com") latency records.

To calculate the P99 latency, we first sort the dataset non-decreasingly. Let the rank of a latency value be by its index in the sorted array. The rank of the ![p^th](https://www.baeldung.com/wp-content/ql-cache/quicklatex.com-9d10e109239c6868bf96593ce7167ff3_l3.svg "Rendered by QuickLaTeX.com") percentile is then:

<img src="https://www.baeldung.com/wp-content/ql-cache/quicklatex.com-453c527132dcf1f8df06321bb95d7ab1_l3.svg" title="Rendered by QuickLaTeX.com" alt="\[Rank_{p} \; = \; ceil(\frac{p}{100} * n)\]" data-align="center">

Now, we get the ![p^{th}](https://www.baeldung.com/wp-content/ql-cache/quicklatex.com-9d10e109239c6868bf96593ce7167ff3_l3.svg "Rendered by QuickLaTeX.com") percentile as:

<img src="https://www.baeldung.com/wp-content/ql-cache/quicklatex.com-018cb6025242d5bde29692974f65c191_l3.svg" title="" alt="\[Percentile_{p} \; = \; d[Rank_{p}]\]" data-align="center">

### 4.1. Example

Let’s apply these formulae. Let’s say we have the quiz marks of 15 students in a class:

89    92    34    45    67    75    37    55    66    44    98    99    77    72    39

To compute their ![90^{th}](https://www.baeldung.com/wp-content/ql-cache/quicklatex.com-ce2f1c23b57e82ec15b18e6366257059_l3.svg "Rendered by QuickLaTeX.com") percentile, we first sort them:

34    37    39    44    45    55    66    67    72    75    77    89    92    98    99

Next, we find the percentile rank of P90:

<img src="https://www.baeldung.com/wp-content/ql-cache/quicklatex.com-e686c6257bc72726498d6aa429ba0627_l3.svg" title="" alt="\[Rank_{90} \; = \; ceil(\frac{90}{100} * 15) \; = \; ceil(13.5) \; = 14\]" data-align="center">

Finally, we get the ![90^{th}](https://www.baeldung.com/wp-content/ql-cache/quicklatex.com-ce2f1c23b57e82ec15b18e6366257059_l3.svg "Rendered by QuickLaTeX.com") percentile:

<img src="https://www.baeldung.com/wp-content/ql-cache/quicklatex.com-57425e24ec8bb7ac4230b76199de8fac_l3.svg" title="" alt="\[Percentile_{90} \; = \; d[Rank_{90}] \; = \; d[14] \;=\; 98\]" data-align="center">

So, for this dataset, we can say that ![90\%](https://www.baeldung.com/wp-content/ql-cache/quicklatex.com-702ee7d4809a367d93c3a93c9a75442b_l3.svg "Rendered by QuickLaTeX.com") of students got marks less than or equal to 98.

## 5. Percentiles and Confidence Intervals

If we take a sample of ![n](https://www.baeldung.com/wp-content/ql-cache/quicklatex.com-ec4217f4fa5fcd92a9edceba0e708cf7_l3.svg "Rendered by QuickLaTeX.com") elements from a dataset having ![N](https://www.baeldung.com/wp-content/ql-cache/quicklatex.com-7354bae77b50b7d1faed3e8ea7a3511a_l3.svg "Rendered by QuickLaTeX.com") (![N](https://www.baeldung.com/wp-content/ql-cache/quicklatex.com-7354bae77b50b7d1faed3e8ea7a3511a_l3.svg "Rendered by QuickLaTeX.com") is much larger than ![n](https://www.baeldung.com/wp-content/ql-cache/quicklatex.com-ec4217f4fa5fcd92a9edceba0e708cf7_l3.svg "Rendered by QuickLaTeX.com")), the sample’s ![99^{th}](https://www.baeldung.com/wp-content/ql-cache/quicklatex.com-280bf65da28558df05ad6fb1e928fdba_l3.svg "Rendered by QuickLaTeX.com") percentile may differ from that of the entire dataset. Here, the larger the sample, the more precise our estimate will be.

This is similar to the case with latency. When dealing with it, we record latencies and assume they follow the same but unknown distribution. Then, we treat the records as a sample. To account for possible fluctuations of the sample estimate around the actual P99 when generalizing the results to all future latencies, we can construct confidence intervals (CI).

**A CI of P99 is the range of values that contain the distributional P99 with predefined confidence.** For instance, if ![[a, b]](https://www.baeldung.com/wp-content/ql-cache/quicklatex.com-1697b646881a88b3a6029defcd0dd8f6_l3.svg "Rendered by QuickLaTeX.com") is the CI with the confidence of 80%, that means that 80% of the CIs we construct in the same way as ![[a, b]](https://www.baeldung.com/wp-content/ql-cache/quicklatex.com-1697b646881a88b3a6029defcd0dd8f6_l3.svg "Rendered by QuickLaTeX.com") (but by using other samples) will contain the distributional P99.

We can use order [statistics](http://baeldung.com/cs/ai-ml-statistics-data-mining) to construct a CI for P99. In order statistics, we arrange all the sample values in ascending order and then do our analysis. We employ order statistics in applications such as process simulation, network modeling, actuarial products, and optimizing production processes.

## 6. Conclusion

In this article, we have gone through percentiles, latency, and their relationship. Percentiles give us a more realistic and intuitive understanding of the actual performance characteristics of our network or application.

**We use the** ![\mathbf{99^{th}}](https://www.baeldung.com/wp-content/ql-cache/quicklatex.com-4eabeff0445b73e862f899f96a060c10_l3.svg "Rendered by QuickLaTeX.com") **percentile to monitor and improve the overall network latency or our application response time**. Percentiles help us distinguish between outliers and real effects.
