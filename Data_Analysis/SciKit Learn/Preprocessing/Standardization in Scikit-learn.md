More info here: [scikit docs](https://scikit-learn.org/stable/modules/preprocessing.html#preprocessing-data)
Standardization formula: $\dfrac{x-mean(x)}{\sqrt{var}}$
# Purpose
Standardization rescales the data so that it has a mean of 0 and standard deviation of 1. This is useful for machine learning algorithms, because they are sensitive to the scale of input data.

# Components of the equation
The standard formula: $\frac{x-mean(x)}{\sqrt{var}}$ has following features:
* `x` - The raw feature value
* `mean(x)` - The mean of all values in the feature, subtracting it centers the data at 0
* `var` - The variance of the feature. Taking the square root gives standard deviation. Dividing by this value ensures that the feature is scaled to have a standard deviation 
## Trivialized explanation of what is going on
When we standardize dataset, we take the middle of the group (mean of x) and shift it to 0. That is the upper term in the equation.  Then we squish or stretch it according to the standard deviation , which is the square root of variance.

Lets consider example of measuring heights. The mean is average height of the group. And standard deviation is like saying "How far are most people from this typical height?". In the first term we shift everything so the average is at zero $x-mean(x)$. Now we are measuring how much taller or shorter someone is compared to the group.

For example if one person is 5.5 feet tall and average height is 5 they are 0.5 from the average.

Then we squish or stretch the values so that the scatter (the standard deviation) is the same for everyone.
# How it helps computers
When computer looks at data, some numbers might be small while others large. Standardization makes them all comparable so the computer does not think one is more important than other set of values.