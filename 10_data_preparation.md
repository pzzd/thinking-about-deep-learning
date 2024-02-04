# Data Preparation

Goal is to adjust data for the most efficient and effective learning process without changing the meaning of the data.

## Definitions
Feature is a value attributed to a sample. A sample can have many features. Each feature can be numerical or categorical.

Numerical data is a number (floating point or integer). AKA quantitative data. Because of the numerical nature of algorithms in a learning system, large numbers may influence a learning program more than smaller ones.

Categorical data is anything else, usually string data.

Ordinal data is categorical data with a known sort order (rainbow order of color names, days of the week). Can be sorted by a custom routine.

Nominal data is categorical data without a natural ordering. Can be turned into ordinal data by defining how to sort it.

## Data cleaning

We should address blanks, incorrect entries, or other errors.

- no typos, misspellings, unprintable characters, corrupted text
- remove accidental duplicates: they will skew data
- no typos with numbers like comma vs period, double negatives sign, NaN, weird choice to indicate empty numerical field
- standardized scientific notation
- features that are mostly empty
- decide on what to do with outliers

Garbage in, garbage out!

## Transformations

You apply transformations to numbers in data without changing relationships among them in order to prepare them for learning. Important principle: any time we modify our training data in some way, we must also modify all future data in the same way. That means a transformer that is used to prepare data for learning must also be used on data before the system is tested and used on data before it is analyzed by a deployed system.

### Convert strings to numbers
Machine learning algorithms require numbers as input so all string data must be turned into numerical data. Many libraries have functions that assign a unique number to each string value of a feature for you.

One-Hot Encoding means turning a single feature value into a list, one value of which is true or "hot". The output of a classifier system is a list, and using one-hot encoding makes the input a list too. Now the classifier can compare lists.

### Normalization

This is scaling numerical data to a specific range (e.g. -1 to 1 or 0 to 1). Data is skewed as a result of this transformations when data of different dimensions originally started with different ranges.

### Standardization

This is two-step process: 

1. Mean normalization or mean subtraction: Add or subtract a fixed value to each data point so that the mean value of every feature is 0.

2. Variance normalization: Scale it so that it has a standard deviation of 1. 68% percent of values in a feature lie in the range -1 to 1.
