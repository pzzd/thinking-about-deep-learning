Chapter 3: Measurig Performance

- TP = True positive
- TN = True negative
- FP = False positive
- FN = False negative 
---

Accuracy is the measure of samples assigned to the right category: 

(TP count + TN count)/all

Accuracy of 1.0 means all samples were predicted correctly.
---

Precision is the percentage of correct positive predictions:

TP / (TP + FP)

Precision is also known as positive predictive value.

Precision of 1.0 means every sample that is positive was correctly predicted as positive.

Precision doesn't tell if all the positive events were found. It ignores all samples except those labeled as positive.
---

Recall is the percentage of positive samples that were predicted correctly:

TP / (TP + FN)

Recall is also known as sensitivity, hit rate, true positive rate.

Recall of 1.0 means every positive event as predicted correctly. Less than 1.0 means missed some positive events (those all the FNs).
