# K-Means

### Information about K-Means

K-means clustering is a very popular unsupervised learning algorithm. In this article I want to provide a bit of background about it, and show how we could use it in an anecdotal real-life situation.

K-Means Clustering is an algorithm that, given a dataset, will identify which data points belong to each one of the k clusters. It takes your data and learns how it can be grouped.

K-Means Clustering is part of a group of learning algorithms called unsupervised learning. In this type of learning model, there is no explicit identification of a label/class/category for each data point.

Each data point in your dataset is a vector of attributes, i.e., features without a specific label that could assign it to a specific cluster or class. The algorithm will then learn on its own how to group data points that have similar features and cluster them together.

One important detail about K-Means Clustering is that, even though it identifies which data point should part of which cluster, you'll have to specify the parameter K, representing the total number of clusters that you want to use to "distribute" your data.

Your preferred workout is jogging and, since you're extremely data-inclined, you make sure to keep track of your performance. So you end up compiling a dataset similar to this

### Overall

1. To begin, we first select a number of classes/groups to use and randomly initialize their respective center points. To figure out the number of classes to use, it’s good to take a quick look at the data and try to identify any distinct groupings. The center points are vectors of the same length as each data point vector and are the “X’s” in the graphic above.

2. Each data point is classified by computing the distance between that point and each group center, and then classifying the point to be in the group whose center is closest to it.

3. Based on these classified points, we recompute the group center by taking the mean of all the vectors in the group.

4. Repeat these steps for a set number of iterations or until the group centers don’t change much between iterations. You can also opt to randomly initialize the group centers a few times, and then select the run that looks like it provided the best results. 

K-Means has the advantage that it’s pretty fast, as all we’re really doing is computing the distances between points and group centers; very few computations! It thus has a linear complexity O(n).

On the other hand, K-Means has a couple of disadvantages. Firstly, you have to select how many groups/classes there are. This isn’t always trivial and ideally with a clustering algorithm we’d want it to figure those out for us because the point of it is to gain some insight from the data. K-means also starts with a random choice of cluster centers and therefore it may yield different clustering results on different runs of the algorithm. Thus, the results may not be repeatable and lack consistency. Other cluster methods are more consistent.

K-Medians is another clustering algorithm related to K-Means, except instead of recomputing the group center points using the mean we use the median vector of the group. This method is less sensitive to outliers (because of using the Median) but is much slower for larger datasets as sorting is required on each iteration when computing the Median vector.


![1 krczk0xygta4qfrvr0fo2w](https://user-images.githubusercontent.com/17385297/50397095-c7a68a00-074c-11e9-9d64-c86bf941c8cd.gif)


[Source](https://www.kdnuggets.com/2018/06/5-clustering-algorithms-data-scientists-need-know.html/).


### Application

By identifying events that are similar to each other you can have a better understanding of your overall performance and get new ideas on how to improve.

A clustering algorithm like K-Means Clustering can help you group the data into distinct groups, guaranteeing that the data points in each group are similar to each other.

A good practice in Data Science & Analytics is to first have good understanding of your dataset before doing any analysis.

Taking an exploratory view of your dataset, you start by plotting a pair-plot, in order to get a better idea about the correlation between different features.

###PairPlot

...Python
X = A[['Unidad_Negocio_num', 'MERCH_AMT_BSE','week']]
X1 = X.fillna(0)
sns.set(style="ticks", color_codes=True)
g = sns.pairplot(X1)
...

![pairplot](https://user-images.githubusercontent.com/17385297/50396627-dfc8da00-0749-11e9-9e97-2fd6559442c7.PNG)

The plots on the diagonal correspond to the distribution of each feature, while the others are scatterplots of each pair of features.

### K means 2

Now that you have a good idea of how your dataset looks like, it's time to use K-Means and see how the individual sessions are grouped. You can start off by splitting your dataset into two distinct groups.

![k means 2](https://user-images.githubusercontent.com/17385297/50396679-37ffdc00-074a-11e9-87a1-dde5f96a959e.PNG)


In this plot, like in the pair plot, we see the relationship between distance and workout duration, but now each data point has the colour of its cluster.

Taking a quick look at this scatter plot we can see that, for instance, all workouts under 25 minutes are in one cluster.

### Correct K value

Depending on the dataset and the problem you're solving, you may have an idea of how you want to cluster your data. Maybe you want to see the data clustered in 3 groups, 5 groups, 10 groups…

If that's not the case, how do we figure out which K value to use?

    Like any parameter in an algorithm, it requires some experimentation, i.e., tuning.

In order to experiment with different values of K, you also need to have a deciding factor or metric, which you're going to be using to make a decision on which value of K provides the best results.


![elbow method](https://user-images.githubusercontent.com/17385297/50396801-f6236580-074a-11e9-858e-c151ce20cdd3.PNG)


The plot above is the result of running K-Means Clustering on the workout dataset with values of K between 2 and 43, which corresponds to the size of the dataset. Each value of K is against the respective distortion value.

Distortion, on the y-axis, corresponds to our cost function: the sum of squared difference between each data point and the centroid, i.e., the cluster centre.

As K increases the corresponding distortion value will tend to zero, because you end up having just one data point per cluster. With only one data point in per cluster, the centroid is the data point itself, so the distortion will be equal to zero.

For this dataset, the the elbow of the curve is around K= 5. For values of K greater than 5, the distortion value starts decaying steadily.


### K means 5

Going back to the original dataset and re-running K-Means with the new found K, you can cluster the data into 5 different groups!


![k means 5](https://user-images.githubusercontent.com/17385297/50396762-ac3a7f80-074a-11e9-8670-7ea1f58ad397.PNG)


[Source](https://www.kdnuggets.com/2018/08/k-means-real-life-clustering-workout-sessions.html/).

