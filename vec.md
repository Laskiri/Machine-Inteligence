# Vectorizing Linear Regression with Multiple Variables

Vectorizing linear regression with multiple variables refers to implementing the linear regression algorithm using matrix operations, which allows for efficient computation. This approach leverages the power of linear algebra to perform operations on entire datasets at once, rather than iterating through individual data points.

## Steps Involved

1. **Representation of Data:**
   - Let \( X \) be the matrix of input features, where each row represents a data point and each column represents a feature.
   - Let \( y \) be the vector of target values.
   - Let \( \theta \) be the vector of parameters (weights) that we want to learn.

2. **Hypothesis Function:**
   - The hypothesis function for linear regression can be written as:
     \[
     h(X) = X \theta
     \]
   - Here, \( X \theta \) is a matrix multiplication of the feature matrix \( X \) and the parameter vector \( \theta \).

3. **Cost Function:**
   - The cost function (Mean Squared Error) for linear regression is:
     \[
     J(\theta) = \frac{1}{2m} \sum_{i=1}^{m} (h(X_i) - y_i)^2
     \]
   - In vectorized form, this can be written as:
     \[
     J(\theta) = \frac{1}{2m} (X \theta - y)^T (X \theta - y)
     \]

4. **Gradient Descent:**
   - The gradient descent update rule in vectorized form is:
     \[
     \theta := \theta - \alpha \frac{1}{m} X^T (X \theta - y)
     \]
   - Here, \( \alpha \) is the learning rate, and \( X^T \) is the transpose of the feature matrix \( X \).

By using matrix operations, we can efficiently compute the hypothesis, cost function, and parameter updates for all data points simultaneously. This is much faster than using loops, especially for large datasets.

## Example in Python

Here is an example of vectorized linear regression in Python using NumPy:

```python
import numpy as np

# Load data
data = np.loadtxt("https://drive.google.com/uc?id=1IM7fSyvchd6MPlV_5b8wuakO09aFcw4s", delimiter=',', skiprows=1)
X = data[:, :4]
y = data[:, 4]

# Add a column of ones to X for the intercept term
X = np.hstack((np.ones((X.shape[0], 1)), X))

# Initialize theta
theta = np.zeros(X.shape[1])

# Set learning rate and number of iterations
alpha = 0.01
iterations = 1000

# Gradient descent
m = len(y)
for _ in range(iterations):
    gradient = (1/m) * X.T @ (X @ theta - y)
    theta -= alpha * gradient

print("Learned parameters:", theta)