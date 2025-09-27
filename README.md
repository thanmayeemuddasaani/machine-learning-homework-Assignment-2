# machine-learning-homework-Assignment-2
**Student Name:** *M. Thanmayee*  
**Student ID:** *700776997*  
**Course:** CS5710 Machine Learning  

This README summarizes the outcomes for **Q7–Q9** using the Iris dataset. We report training/test metrics, visualize decision boundaries for kNN (2 features), and evaluate a kNN model (k=5) with confusion matrix and ROC/AUC.

## Q7. Decision Trees (max_depth = 1, 2, 3)

Split: 70/30 stratified train/test, random_state=42. All 4 features used.

|   max_depth |   train_acc |   test_acc |
|------------:|------------:|-----------:|
|           1 |    0.666667 |   0.666667 |
|           2 |    0.971429 |   0.888889 |
|           3 |    0.980952 |   0.977778 |

**Discussion:**
- Depth=1 shows lower capacity and may underfit (training accuracy below 1.0).
- As depth increases to 3, training accuracy rises and test accuracy improves up to a point.
- There is **no severe overfitting** observed up to depth=3 on this split, but the usual trade-off applies.

## Q8. kNN (2 features: sepal length & sepal width)

We trained kNN with k ∈ {1,3,5,10} on the two-feature subset. Decision-boundary visualizations on the train split:

![decision_boundary_k1.png](./decision_boundary_k1.png)

![decision_boundary_k3.png](./decision_boundary_k3.png)

![decision_boundary_k5.png](./decision_boundary_k5.png)

![decision_boundary_k10.png](./decision_boundary_k10.png)

|   k |   train_acc |   test_acc |
|----:|------------:|-----------:|
|   1 |    0.942857 |   0.666667 |
|   3 |    0.866667 |   0.666667 |
|   5 |    0.847619 |   0.8      |
|  10 |    0.809524 |   0.755556 |

**Boundary Evolution:**
- **k=1**: very wiggly, highly local boundaries (risk of overfitting).
- **k=3–5**: smoother boundaries, better generalization.
- **k=10**: boundaries become smoother but can underfit class edges.

## Q9. Performance Evaluation for kNN (k=5, 4 features)

Confusion Matrix (counts):

|            |   setosa |   versicolor |   virginica |
|:-----------|---------:|-------------:|------------:|
| setosa     |       15 |            0 |           0 |
| versicolor |        0 |           15 |           0 |
| virginica  |        0 |            1 |          14 |

Classification Report:

```
              precision    recall  f1-score   support

      setosa     1.0000    1.0000    1.0000        15
  versicolor     0.9375    1.0000    0.9677        15
   virginica     1.0000    0.9333    0.9655        15

    accuracy                         0.9778        45
   macro avg     0.9792    0.9778    0.9778        45
weighted avg     0.9792    0.9778    0.9778        45
```

**Micro-average ROC AUC:** `0.9968`

![Confusion Matrix](./knn_k5_confusion_matrix.png)

![ROC Curve](./knn_k5_roc.png)

