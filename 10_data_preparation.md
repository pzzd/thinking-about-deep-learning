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

## Reuse the transformation

Normalizing and standardizing routines use parameters to define how to do their type of transformation. The parameters can be produced by libraries from the training data and they are saved for running the transformations later. This is important because when you test your system or use it after deployement this data must be transformed using the parameters from training. It is ok that the new data is not itself normalized or standardized.

## How to apply a transformation

Decide on univariate or multivariate transformation. Univariate is a good option when features are independent. Multivariate is the option for when features have a dependency between them. These features should be scaled together (e.g., temperature and time of day).

Decide on slice processing method: by sample, feature, or element.

- Samplewise processing is appropriate if all the features are the same kind of data (e.g., an audio file with features of amplitude at a certain time). You would scale all the features in a single sample to the same scale. All samples are independent of other samples.

- Featurewise processing is appropriate when features represent different things. It wouldn't make sense to scale all features to the same scale because the ranges and measurement units differ. You can analyze and modify a single feature across all the samples. In this method, each column of feature values is called a fibre.

- Elementwise processing is appropriate for data that is the same type of data with the same scale and measurement unit; for example, if all data is in inches and you want to convert to centimenters. You apply the same transformation to every value of every feature of every sample. This is common when working with image data: each pixel is an element.

## Inverse Transformations

Every transformation object comes with a routine to undo a transformation. This is required when the system reports back data. Here is the scenario: You normalize your original data and train a system. Now the deployed system takes input from a user, which is normalized before being used. The return result is normalized, but the value doesn't make sense for a user, so the data is inverse-transformed to put it into the scale and unit the user expects.

If user-supplied sample is very out of range from the original data, the system may still give a reasonable output, or it may return something that doesn't make sense.

## Cross validation
When you do cross-validation of your system, you set aside one fold of data for testing, and use the rest for training. The transformer must be built from the training data only: be sure to leave out the validation data when making the transformer. Not doing so leads to information leakage: the validation data is leaked bc it affects the transformer.

The transformation, built only on the training data, is used on the validation data just like it would be used on data coming into a deployed system.

Cross validation is done on a loop, with a different fold removed each time for validation data. In each iteration, compute a new transformation for that iteration's training set.

Most libraries take care of this issue for you in their cross-validation routines.
