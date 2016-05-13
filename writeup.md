I have used random seed 0 which is also pasted in my script.
My script can run either from PayalGala-mock-final repo or from src folder.
I separated data into high risk and low risk groups.
I have removed the admission date from the features.

I have tried plotting various features of data as scatter plots and histograms.
    I plotted histograms to understand the distribution of data in high risk and low risk patients groups.
        This shows generally similar spread of features in high risk as well as low risk patients.
        Histograms can plot single features.
    I plotted scatter plots to understand the difference of data in both the groups.
        I found that features are similar in high as well as low risk patients.
        Scatter plots can plot two feature together.

I tried feature selection using RFE and doing logistic regression as one of the classification method
    I tried using 1 to 6 as number of features to be selected for RFE and I found that
        When number of features to be selected is 1 - diastolic blood pressure was the feature that was ranked 1.
        When number of features to be selected is 2 - diastolic blood pressure and heart rate were selected with ranking 1.
        When number of features to be selected is 3 - heart rate, systolic and diastolic blood pressure were selected with ranking 1.
        When number of features to be selected is 4 - all features except age and respiratory rate received ranking 1.
        When number of features to be selected is 5 - all features except age were selected with ranking 1.

However, logistic regression doesn't seem to be the appropriate method for this data classification as performance metrics obtained with various number of features were similar and were not very good.
    Sensitivity was around 0.3.
    Accuracy was around 0.58.
    AUC was around 0.5
Logistic regression is a regression model where the dependent variable (DV) is categorical.
The binary logistic model is used to estimate the probability of a binary response based on one or more predictor (or independent) variables (features)

I tried performing PCA, as the values of features are continuous, they seem to be interdependent
PCA explained variance showed that variance in all the components was more or less same. It can be said that all the features are important.
PCA are the underlying structure in the data. They are the directions where there is the most variance, the directions where the data is most spread out.
Since, PCA resulted in similar variance of all the components, I continued grid search with all the parameters.
    I performed grid search for support vector machine for
        kernels - linear, RBF and Poly
        C - 0.01, 0.1, 1, 10, 100
        Gamma - 0.001,0.01,0.1, 1.0, 10
        Degree - 2

I found that Polynomial kernel with C = 100, gamma = 10 and degree = 2 were the best estimators.
    The accuracy is 0.52
    sensitivity is 0.42
    precision is 0.49

Since, Polynomial kernel was found to be the best estimator, I decreased sample size to 0.4 to also try degree-3.
Polynomial kernel is resource intensive when I am trying to run degrees 3 and hence, I have decided to run it with degree 2.

In machine learning, kernel methods are a class of algorithms for pattern analysis, whose best known member is the support vector machine (SVM).
Support Vector Machines algorithm is used for pattern recognition.
Basic idea of SVM is to establish optimal hyperplane for linearly separable patterns and also, extend to patterns that are not linearly separable by transformations of original data to map into new space by Kernel function.
C is the cost of constraints violation (default: 1).

I performed kmeans clustering on the data
K-means is one of the simplest unsupervised learning algorithm.
The procedure follows a simple and easy way to classify a given data set through a certain number of clusters (assume k clusters) fixed a priori.
The main idea is to define k centroids, one for each cluster.
The next step is to take each point belonging to a given data set and associate it to the nearest centroid.
When no point is pending, the first step is completed and an early groupage is done.
At this point we need to re-calculate k new centroids as barycenters of the clusters resulting from the previous step.
After we have these k new centroids, a new binding has to be done between the same data set points and the nearest new centroid. A loop has been generated.
As a result of this loop we may notice that the k centroids change their location step by step until no more changes are done.
In other words centroids do not move any more.

Since, there are two clusters possible - high risk and low risk, I selected number of clusters to be 2.
I calculated Silhouette
Silhouette refers to a method of interpretation and validation of consistency within clusters of data.
The silhouette value is a measure of how similar an object is to its own cluster (cohesion) compared to other clusters (separation).
Here, silhouette score is 0.37 and heart rate and respiratory rate clustered well in two separate clusters
Systolic and diastolic pressure clusters and age and score clusters did not separate well.
 This can also be seen earlier in scatter plots. Hence, the Silhouette score is low.
It is also seen in histograms that data is not separable and it is overlapping.
scatter plot also shows that data is similarly distributed in high risk as well as low risk patients.

It is seen on scatter plot, histogram that spread of all the features in high risk and low risk patients is more or less.

I have tested various performance metrics like accuracy, sensitivity, specificty, precision, area under curve and ROC curve.
    Sensitivity is the true positive rate.
    Specificity is the true negative rate.
    Precision is measure of positive predicted value.
    Accuracy is the measure of correctly classified observations.
    A receiver operating characteristics (ROC) graph is a technique for visualizing, organizing and selecting classifiers based on their performance.
    ROC graphs are commonly used in machine learning algorithms as one of the performance metrics.
    ROC curve is a plot of as true positive rate vs false positive rate. The closer the curve follows the left-hand border and then the top border of the ROC space, the more accurate the test. The closer the curve comes to the 45-degree diagonal of the ROC space, the less accurate the test.
    The accuracy of the test depends on how well the test separates the group being tested into those with and without the disease in question. This is measured by the Area Under the ROC Curve (AUC). An area of 1 represents a perfect test; an area of .5 represents a worthless test.

    ### Histograms
    ![Histograms of all the features]

     (https://github.com/PayalGala/Practice/blob/dev/Plots/Histograms%20of%20variables.png)