# MEX
Model EXplorer

## General idea
you have some data organized in key-values (think of a dataframe)
and this provides the possibility to 
- create all the possible models
- sort them by any result criteria
- filter unwanted model according to a given predicate


## Example
``` python
# DATA is a pandas dataframe
cols = DATA.columns.to_list()

y = "sepal_length"
xs = [c for c in cols if c != y]

from statistics import linear_regression, LinearRegression

# adjust the function that estimate the model
# x and y are series, and the order is different
def modelf(y, x):
    return linear_regression(x.values, y.values)

# estimate only models with a single regressor
def filterxs(cols):
    return len(cols) == 1

# some model acceptance criteria
def filtermodels(m: LinearRegression):
    return m.slope < 0.5

for m in estimate_models(y, xs, DATA, modelf, filterxs, filtermodels):
    print(m)

```

### Motivation
it's a repetitive part of my job that I wish to abstract away
