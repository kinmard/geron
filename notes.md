
# Supervised Learning

## Batch Learning

In batch learning, the system is incapable of learning incrementally: it must be trained using all the available data. This will generally take a lot of time and computing resources, so it is typically done offline. First the system is trained, and then it is launched into production and runs without learning anymore; it just applies what it has learned. This is called offline learning.

If you want a batch learning system to know about new data (such as a new type of spam), you need to train a new version of the system from scratch on the full dataset (not just the new data, but also the old data), then stop the old system and replace it with the new one.

However, training on the full dataset many be costly or impossible (if the data is very large). 
This is where online learning comes into play.

## Online Learning

In online learning, training happens incrementally as new data instances are fed sequentially or in mini-batches. Once the system has learned the data, it can discard. So, it uses less resources and does not need to be trained from scratch on all data unlike a Batch Learning system.

It can also be used for 'out of core' learning where data does not fit in the memory. It is broken down into smaller batches for learning until all such batches are processed.

# Chapter 3 - Classification 

Evaluating a classifier is often significantly trickier than evaluating a regressor. 

WHY IS THIS THE CASE ?

Accuracy is generally not a preferred performance measure for classifiers, especially when you are dealing with skewed datasets (i.e. when some classes are much more frequent than others).
This is because accuracy is a simple yes/no question but the reality is a bit more nuanced. E.g. in practice, we care about false positives and true positives (type 1 and type 2 errors)

Alternate way to measure a classifier performance is using Confusion Matrix.

## Confusion Matrix

In a confusion matrix, True Positive Rate (TPR) gives the accuracy of the positive predictions. This is called the precision of the classifier and is given by 

precision = TP / (TP + FP) i.e. ratio of how many ACTUAL positives (TP) vs how many the model predicted to be positive (TP + FP)

On the other hand, Recall gives us the ratio of positive instances that are correctly detected by the classifier.

recall = TP / (TP + FN) i.e. ratio of how many ACTUAL positives vs how many total positive instances are there in the actual data i.e. ACTUAL positives + those positives that were falsely classified as negative (FN)

f1 score is a harmonic mean of precision and recall. Harmonic mean gives more weight to low values. So, F1 score is high only if both precision and recall are high. 

F1  = 2 / (1/precision + 1/recall) 

Usually, we care more about precision or recall. So, F1 may not be that good a measure. 

## But how is the threshold set so that anything above it is positive and below it is negative ?

scikit-learn does not expose the threshold but it gives access to the deciion scores that it uses to make predictions. Instead of calling predict() function, we can call the decision_function() to get the score for each instance and then compare it with any threshold to make predictions.

## What is the impact of increasing the threshold on recall ?
As threshold goes up, recall goes down. This is because the number of FN goes up.

## Precision-Recall Curve
We can also precision vs recall to find the best threshold where our desired benchmark for both are met. 

## ROC Curve
ROC or Receiver Operating Characteristic curve plots TPR vs the FPR rate. FPR rate = 1 - TNR 

TPR = TP/ (TP+FP) , TNR = TN/(TN + FN)
so FPR = 1 - TN/(TN+FN) = FN/(TN+FN)


Bigger the area under the ROC curve, the better it is.


## When to use Precision-Recall curve vs ROC curve ?
PR curve should be used where the positive class is rare or when you care more about false-positives than false negatives. 
ROC curve should be used in other cases. 