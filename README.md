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

<img width="630" height="470" alt="image" src="https://github.com/user-attachments/assets/76008ab5-0297-4fac-9425-61a8d8334cb8" />


<img width="630" height="470" alt="image" src="https://github.com/user-attachments/assets/b3054f8a-aa10-4635-bb59-5a7172c86a10" />

<img width="630" height="470" alt="image" src="https://github.com/user-attachments/assets/536abfbd-223b-45d3-a28d-818e13186880" />

<img width="630" height="470" alt="image" src="https://github.com/user-attachments/assets/8985a382-809b-49cf-be94-738564fac79d" />


|   k |   train_acc |   test_acc |
|----:|------------:|-----------:|
|   1 |    0.942857 |   0.666667 |
|   3 |    0.866667 |   0.666667 |
|   5 |    0.847619 |   0.8      |
|  10 |    0.809524 |   0.755556 |

## 🔹 Results & Analysis

### k = 1
- The decision boundary is very irregular and jagged.  
- Each training point strongly influences its local region.  
- This indicates **high variance** and a tendency to **overfit**.  
- The model is very sensitive to noise.

---

### k = 3
- The boundary is smoother compared to k=1.  
- Predictions are based on 3 neighbors, so local noise has less effect.  
- Some irregular shapes remain, but the model is **more stable**.  

---

### k = 5
- The boundaries are smoother and more generalized.  
- Noise influence is further reduced.  
- This achieves a **good balance between bias and variance**.  
- The model generalizes well compared to smaller k.

---

### k = 10
- The boundaries are the smoothest of all cases.  
- Predictions are very stable because the model considers a larger neighborhood.  
- However, some fine details are lost, leading to **higher bias**.  
- This may cause **underfitting** if k is set too high.

---

## 🔹 Overall Observation
- **Small k (1, 3):** High variance, low bias → prone to overfitting.  
- **Medium k (5):** Best trade-off between bias and variance → good generalization.  
- **Large k (10):** Low variance, high bias → may underfit.  

➡️ Based on the plots, **k=5** gives the most balanced and reliable decision boundaries for this dataset.

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

<img width="577" height="470" alt="image" src="https://github.com/user-attachments/assets/8cbefa99-b530-4960-9e57-3a12f674bda4" />

## 🔹 Confusion Matrix

| True Class   | Predicted Setosa | Predicted Versicolor | Predicted Virginica |
|--------------|------------------|-----------------------|----------------------|
| **Setosa**      | 15               | 0                     | 0                    |
| **Versicolor**  | 0                | 15                    | 0                    |
| **Virginica**   | 0                | 1                     | 14                   |

**Observations:**
- The model classified **Setosa** and **Versicolor** perfectly.  
- For **Virginica**, 1 sample was misclassified as Versicolor.  
- Overall, the misclassification rate is very low.

---

## 🔹 Classification Report

- **Setosa** → Precision: 1.00, Recall: 1.00, F1: 1.00  
- **Versicolor** → Precision: 0.94, Recall: 1.00, F1: 0.97  
- **Virginica** → Precision: 1.00, Recall: 0.93, F1: 0.97  

**Overall performance:**
- **Accuracy:** 97.8%  
- **Macro avg (across classes):** Precision = 0.979, Recall = 0.978, F1 = 0.978  
- The model performs consistently well across all three classes.
<img width="630" height="470" alt="image" src="https://github.com/user-attachments/assets/9c5c24a1-0d9a-4d4a-9fc1-a937f3d505c4" />

## 🔹 ROC Curve & AUC

- I plotted the **micro-average ROC curve** for the multiclass setting.  
- The **AUC (Area Under Curve) ≈ 0.997**, which indicates **excellent separability** between classes.  
- The curve lies close to the top-left corner, showing high true positive rate with very low false positives.

  ## 🔹 Conclusion
- The **kNN classifier with k=5** achieves **very high accuracy and strong generalization** on the Iris dataset.  
- Only a single misclassification occurred, showing that this choice of k is effective.  
- Based on the confusion matrix, precision, recall, and AUC, the model is reliable and balanced across all three Iris classes.
