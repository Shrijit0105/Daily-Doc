# Understanding Sigmoid: Numerical Calculations and the Value of e^x

## 1. Introduction

While learning Machine Learning, I came across the Sigmoid function. It is commonly used in logistic regression and other machine learning applications.

The formula looks simple, but understanding how to calculate its value manually requires some knowledge of exponential functions.

The sigmoid function is:

\[
\sigma(x)=\frac{1}{1+e^{-x}}
\]

Here:

- \(x\) is the input value.
- \(e\) is Euler's number, approximately 2.71828.
- \(e^{-x}\) is the exponential term.
- The final output always lies between 0 and 1.

The objective of this document is to understand how to calculate this function using numerical examples instead of relying entirely on a calculator or Python.

## 2. First, What Is Euler's Number (e)?

Euler's number is a mathematical constant, just like pi (π).

Its approximate value is:

\[
e=2.718281828459...
\]

It is an irrational number, which means its decimal representation continues infinitely without repeating in a fixed pattern.

The number e appears in many mathematical concepts, including:

- Exponential growth and decay
- Compound interest
- Calculus
- Probability and statistics
- Machine Learning

For now, the important thing is understanding how powers of e work.

## 3. What Does e^x Actually Mean?

The expression \(e^x\) means that we are raising Euler's number to the power of x.

For example:

\[
e^2=2.71828^2
\]

\[
e^2\approx7.389
\]

Similarly:

\[
e^1=2.71828
\]

\[
e^0=1
\]

And:

\[
e^{-1}=\frac{1}{e^1}
\]

\[
e^{-1}\approx0.3679
\]

Notice something interesting: a negative exponent does not make the result negative. Instead, it gives us the reciprocal of the corresponding positive exponent.

### Some useful values

| Expression | Approximate value |
|---|---:|
| \(e^{-3}\) | 0.0498 |
| \(e^{-2}\) | 0.1353 |
| \(e^{-1}\) | 0.3679 |
| \(e^0\) | 1 |
| \(e^1\) | 2.7183 |
| \(e^2\) | 7.3891 |
| \(e^3\) | 20.0855 |

These values are useful when solving sigmoid problems manually.

## 4. How Do We Calculate e^x?

There are different ways to calculate an exponential value.

### Method 1: Using a Scientific Calculator

Most scientific calculators have an `e^x` button.

For example, to calculate:

\[
e^2
\]

We enter:

1. Press the `e^x` function.
2. Enter 2.
3. Press equals.

The result will be approximately:

\[
7.389056
\]

The exact button sequence depends on the calculator model.

### Method 2: Using the Taylor Series Expansion

This method helps us understand how exponential values can be calculated mathematically.

The exponential function can be represented using an infinite series:

\[
e^x=1+x+\frac{x^2}{2!}+\frac{x^3}{3!}+\frac{x^4}{4!}+\cdots
\]

Here, `!` represents factorial.

For example:

\[
3!=3\times2\times1=6
\]

Let's calculate \(e^1\).

Substituting x = 1:

\[
e^1=1+1+\frac{1}{2!}+\frac{1}{3!}+\frac{1}{4!}+\cdots
\]

Taking the first few terms:

\[
e^1\approx1+1+\frac12+\frac16+\frac1{24}+\frac1{120}
\]

\[
e^1\approx2.71667
\]

The actual value is approximately 2.71828.

The difference occurs because we have used only a limited number of terms. Adding more terms improves the approximation.

**Important:** We normally don't calculate exponential values manually this way in everyday programming. Scientific calculators and mathematical libraries handle these calculations efficiently.

## 5. Understanding the Sigmoid Function

Now let's return to sigmoid.

\[
\sigma(x)=\frac{1}{1+e^{-x}}
\]

The function takes any real number as input and converts it into a value between 0 and 1.

This is particularly useful in binary classification, where we may interpret the output as a probability estimate.

Let's solve some examples.

## 6. Numerical Example 1: When x = 0

Given:

\[
\sigma(x)=\frac{1}{1+e^{-x}}
\]

Substitute x = 0:

\[
\sigma(0)=\frac{1}{1+e^{-0}}
\]

Since:

\[
e^0=1
\]

Therefore:

\[
\sigma(0)=\frac{1}{1+1}
\]

\[
\boxed{\sigma(0)=0.5}
\]

So, when the input is zero, sigmoid returns 0.5.

## 7. Numerical Example 2: When x = 1

Substitute x = 1:

\[
\sigma(1)=\frac{1}{1+e^{-1}}
\]

We know:

\[
e^{-1}\approx0.3679
\]

Substitute the value:

\[
\sigma(1)=\frac{1}{1+0.3679}
\]

\[
=\frac{1}{1.3679}
\]

\[
\boxed{\sigma(1)\approx0.7311}
\]

The output is approximately 0.7311.

## 8. Numerical Example 3: When x = -1

Substitute x = -1:

\[
\sigma(-1)=\frac{1}{1+e^{-(-1)}}
\]

The two negative signs cancel:

\[
=\frac{1}{1+e^1}
\]

We know:

\[
e^1\approx2.7183
\]

Therefore:

\[
\sigma(-1)=\frac{1}{1+2.7183}
\]

\[
=\frac{1}{3.7183}
\]

\[
\boxed{\sigma(-1)\approx0.2689}
\]

Notice that the output is below 0.5 because the input is negative.

## 9. Numerical Example 4: When x = 2

Substitute x = 2:

\[
\sigma(2)=\frac{1}{1+e^{-2}}
\]

We know:

\[
e^{-2}\approx0.1353
\]

Therefore:

\[
\sigma(2)=\frac{1}{1+0.1353}
\]

\[
=\frac{1}{1.1353}
\]

\[
\boxed{\sigma(2)\approx0.8808}
\]

As the positive input increases, the sigmoid output moves closer to 1.

## 10. Numerical Example 5: When x = -2

Substitute x = -2:

\[
\sigma(-2)=\frac{1}{1+e^{-(-2)}}
\]

\[
=\frac{1}{1+e^2}
\]

We know:

\[
e^2\approx7.3891
\]

Therefore:

\[
\sigma(-2)=\frac{1}{1+7.3891}
\]

\[
=\frac{1}{8.3891}
\]

\[
\boxed{\sigma(-2)\approx0.1192}
\]

## 11. Summary of Numerical Results

| Input (x) | e^(-x) | Sigmoid output |
|---:|---:|---:|
| -2 | 7.3891 | 0.1192 |
| -1 | 2.7183 | 0.2689 |
| 0 | 1.0000 | 0.5000 |
| 1 | 0.3679 | 0.7311 |
| 2 | 0.1353 | 0.8808 |

From these examples, we can observe:

- Negative inputs produce outputs below 0.5.
- An input of zero produces exactly 0.5.
- Positive inputs produce outputs above 0.5.
- As the input increases, the output approaches 1.
- As the input decreases, the output approaches 0.

## 12. Why Does Sigmoid Use e?

The exponential function gives sigmoid a smooth, continuous S-shaped curve.

It also ensures that the output stays between 0 and 1.

This makes sigmoid useful for converting a numerical score into a probability-like value.

For example, in binary classification:

- 0.90 could indicate a high estimated probability of belonging to class 1.
- 0.20 could indicate a low estimated probability of belonging to class 1.
- 0.50 represents the midpoint.

A classification threshold, often 0.5, can then be used to make a class prediction.

However, a sigmoid output is not automatically a well-calibrated probability. That depends on the model and data.

## 13. Implementing the Calculation in Python

Python's `math` module provides an exponential function.

```python
import math

x = 1

exp_value = math.exp(-x)

sigmoid = 1 / (1 + exp_value)

print("Exponential value:", exp_value)
print("Sigmoid output:", sigmoid)
```

Output:

```text
Exponential value: 0.36787944117144233
Sigmoid output: 0.7310585786300049
```

Here, `math.exp(-x)` calculates \(e^{-x}\).

We can also implement the same calculation using NumPy:

```python
import numpy as np

x = np.array([-2, -1, 0, 1, 2])

sigmoid = 1 / (1 + np.exp(-x))

print(sigmoid)
```

Output:

```text
[0.11920292 0.26894142 0.5 0.73105858 0.88079708]
```

NumPy's `np.exp()` performs the exponential operation on each element of the array.

## 14. Practice Problems

Try solving these manually before checking the results with Python.

**Problem 1:** Calculate sigmoid when x = 3.

**Problem 2:** Calculate sigmoid when x = -3.

**Problem 3:** What is the value of \(e^0\), and why?

**Problem 4:** Why does \(e^{-2}\) have a positive value even though its exponent is negative?

**Problem 5:** If the sigmoid output is 0.5, what is the input value?

**Problem 6:** What is the difference between `math.exp()` and `np.exp()`?

### Answers for self-checking

1. Approximately 0.9526
2. Approximately 0.0474
3. 1, because any non-zero number raised to the power zero equals 1.
4. A negative exponent represents the reciprocal of the corresponding positive exponent.
5. x = 0
6. `math.exp()` is designed for individual numerical values, while `np.exp()` supports element-wise calculations on NumPy arrays and other supported inputs.

## 15. What I Learned

The main thing I understood from this exercise is that sigmoid is not a mysterious formula that Python simply calculates for us.

It is built from basic mathematical operations, and the exponential term is an important part of it.

I also learned that \(e^x\) is not a collection of random pre-written values. It is a mathematical function that can be evaluated for different inputs. Libraries such as Python's `math` and NumPy provide efficient implementations of that function.

Understanding this makes it easier to connect the mathematical definition of sigmoid with its actual implementation in Python and its use in Machine Learning.

**Next learning target:** Understand the derivative of sigmoid and why it is useful during gradient-based learning.
