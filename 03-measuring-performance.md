Chapter 3: Measurig Performance

- TP = True positive
- TN = True negative
- FP = False positive
- FN = False negative

"Identified" means "assigned to the right category" by a model.

"Event" and "sample" are synonyms.

---
**Accuracy** is the measure of correctly identified samples: 

(TP count + TN count)/all

Accuracy of 1.0 means all samples were predicted correctly.

Precision and recall are used to measure the mistakes.

---
**Precision** is the measure of correctly identified positives out of all identified positives:

TP / (TP + FP)

Precision is also known as positive predictive value.

Precision of 1.0 means every sample that is identified as positive was correctly identified.

Precision doesn't tell if all the positive events were found. It ignores all samples except those labeled as positive.

Precision does not tell you any information about false negatives.

---
**Recall** is the measure of correctly identified positives out of all actual positives:

TP / (TP + FN)

Recall is also known as sensitivity, hit rate, true positive rate.

Recall of 1.0 means every actually positive event was predicted correctly. Less than 1.0 means some positive events (those all the FNs) were missed by the model.

Recall does not tell you any information about false positives.

---
Reducing the number of false positives (which increase precision) increases the number of false negatives (which reduces recall) and vice versa.

_Why is that necessarily so? Maybe it is so when you are tuning a finished, trained model. Seems like a better model would reduce both false negatives and false positives._

In machine learning precision and recall are useful for characterizing  the performance of the classifier and comparing it to other classifiers. Accuracy, precision, and recall should be considered together, and ideally they are all as close to 1 as possible. It's not possible for both perfect precision and perfect recall.

---
**f1 score **is a combination of precision and recall; also called harmonic mean. f1 is low when either precision or recall is low, and approaches 1 as both precision and recall approach 1.
