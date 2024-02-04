# Data Preparation

Goal is to adjust data for the most efficient and effective learning process without changing the meaning of the data.

## Definitions
Feature is a value attributed to a sample. A sample can have many features. Each feature can be numerical or categorical.

Numerical data is a number (floating point or integer). AKA quantitative data.

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
