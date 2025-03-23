# XGBoost Part 1: Regression

## Video Source

## Overview

### Introduction to XGBoost
- XGBoost stands for **Extreme Gradient Boosting**.
- It's a sophisticated machine learning algorithm with various components.
- The tutorial assumes familiarity with basic **gradient boosting** and **regularization** concepts.

### Unique Regression Trees
This part focuses on XGBoost's unique approach to building regression trees. There are three parts in total:
1. **Part 1**: Intuition about XGBoost regression trees.
2. **Part 2**: XGBoost classification trees.
3. **Part 3**: Mathematical details and relationships between regression and classification.

## Initial Predictions
- Initial prediction can be **arbitrary**; by default, it is set to **0.5**.
- The **residuals** (differences between observed and predicted values) indicate how well the initial prediction performs.

## Building XGBoost Trees

### Start with a Single Leaf
- All residuals are grouped in the initial leaf.

### Calculate Similarity Score
Formula:

![image](https://github.com/user-attachments/assets/85a49767-9dd0-408f-8f48-ea9fd1a694e2)


![image](https://github.com/user-attachments/assets/dec81d7f-3f8b-41e3-8c59-89c8efd395b0)


- Set **λ (lambda) to 0** temporarily for calculations.

### Clustering Similar Residuals
- Assess if splitting the residuals into two groups improves the **similarity score**.
- **Example**: Split observations based on dosage.

### Splitting Residuals
For a split:
1. **Calculate** the similarity score for each resulting leaf.
2. **Determine** if clustering improves residual similarity compared to the root leaf.

### Calculating Gain
Gain measures how much better the split is at clustering similar residuals.

Formula:

![image](https://github.com/user-attachments/assets/50f33d04-8dbd-4b92-8a82-b0646fed14fd)


### Pruning the Tree
#### Define Gamma (γ) for Pruning:
- Set a threshold for **gain**, if \( \text{gain} - \gamma < 0 \), **prune** the branch.
- **Example Scenario**:
  - With a chosen **γ** (e.g., **130**):
  - Evaluate **gain** differences and decide whether to keep branches.
  - ![image](https://github.com/user-attachments/assets/6682b21a-c94d-4fad-8679-c99fc0bd238c)


## Output Values
Formula:

```markdown
\[
\text{Output Value} = \frac{\sum \text{residuals}}{\text{number of residuals} + \lambda}
\]
```

- When **λ = 0**, the output is the **average of the residuals**.
- Increasing **λ** reduces **individual observation contribution**. The pruning becomes easier when **λ > 1**
- ![image](https://github.com/user-attachments/assets/898a1a18-a070-41bf-a9a1-739401ea632f)

-![image](https://github.com/user-attachments/assets/b08ff438-352e-4902-8ddc-12f8a69840d8)


## Predictions
- New predictions combine the **initial prediction** with the output of trees, **scaled by learning rate (η)**.

### Learning Rate (η):
- Default value: **0.3**.
- Updated predictions depend on previous residuals and aim to **minimize them over iterations**.

## Summary of Tree Building Process
1. **Calculate similarity scores**.
2. **Determine gain** to assess data splitting.
3. **Prune based on differences** between gain and the defined parameter **γ**.
4. **Achieve output values** for the final leaves.
5. **Understand the role of λ** in controlling overfitting by adjusting similarity scores.

## Conclusion
This video provides foundational insights into building and refining **regression trees** in **XGBoost**, preparing the ground for more complex features and applications in later parts.

