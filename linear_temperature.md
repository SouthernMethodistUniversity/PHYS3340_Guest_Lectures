---
jupyter:
  jupytext:
    formats: ipynb,md
    text_representation:
      extension: .md
      format_name: markdown
      format_version: '1.3'
      jupytext_version: 1.12.0
  kernelspec:
    display_name: Python 3 (ipykernel)
    language: python
    name: python3
---

# Linear Regression and Temperature


In this notebook, we'll look at using linear regression to study changes in temperature.


## Setup

```python
import pandas as pd
import numpy as np
import matplotlib
import matplotlib.pyplot as plt
import warnings
warnings.simplefilter(action='ignore', category=FutureWarning)

%config InlineBackend.figure_format ='retina'
```

## Getting our data


We'll be getting data from [North America Land Data Assimilation System (NLDAS)](https://wonder.cdc.gov/NASA-NLDAS.html), which provides the daily average temperature from 1979-2011 for the United States.


For the next step, you will need to choose some settings in the data request form. These are:

- GroupBy: Month Day, Year
- Your State
- Export Results (check box)
- Show Zero Values (check box)


>1) Download the data for your home state (or state of your choosing) and upload it to M2 in your work directory.


# Loading our data

```python
df = pd.read_csv('North America Land Data Assimilation System (NLDAS) Daily Air Temperatures and Heat Index (1979-2011).txt',delimiter='\t',skipfooter=14,engine='python')
```

```python
df
```

### Clean the data


>2) Drop any rows that have the value "Total" in the Notes column, then drop the Notes column

```python

```

>3) Make a column called Date that is in the pandas datetime format

```python

```

>4) Make columns for 'Year', 'Month', and 'Day' by splitting the column 'Month Day, Year'

```python

```

```python
df['DateInt'] = df['Date'].astype(int)/10e10 # This will be used later
```

## Generating a scatter plot


> 4) Use df.plot.scatter to plot 'Date' vs 'Avg Daily Max Air Temperature (F)'. You might want to add figsize=(50,5) as an argument to make it more clear what is happening.

```python

```

>5) Describe your plot.


### Adding colors for our graph

```python
# No need to edit this unless you want to try different colors or a pattern other than colors by month

cmap = matplotlib.cm.get_cmap("nipy_spectral", len(df['Month'].unique())) # Builds a discrete color mapping using a built in matplotlib color map

c = []
for i in range(cmap.N): # Converts our discrete map into Hex Values
    rgba = cmap(i)
    c.append(matplotlib.colors.rgb2hex(rgba))

df['color']=[c[int(i-1)] for i in df['Month'].astype(int)] # Adds a column to our dataframe with the color we want for each row
```

>6) Make the same plot as 4) but add color by adding the argument c=df\['color'\] to our plotting command.

```python

```

## Pick a subset of the data


>7) Select a 6 month period from the data. # Hint use logic and pd.datetime(YYYY, MM, DD)

```python

```

>8) Plot the subset using the the same code you used in 6). You can change the figsize if needed.

```python

```

## Linear Regression


We are going to use a very [simple linear regression model](https://en.wikipedia.org/wiki/Simple_linear_regression). You may implement a more complex model if you wish.

The method described here is called the least squares method and is defined as:

$m = \frac{\sum_{i=1}^{n}(x_i-\bar{x})(y_i-\bar{y}))}{\sum_{i=1}^{n}(x_i-\bar{x})^2}$

$b = \bar{y} - m\bar{x}$

Where $\bar{x}$ and $\bar{y}$ are the average value of $x$ and $y$ respectively.


First we need to define our X and Y values.

```python
X=subset['DateInt'].values
Y=subset['Avg Daily Max Air Temperature (F)'].values
```

```python
def lin_reg(x,y):
    # Calculate the average x and y
    x_avg = np.mean(x)
    y_avg = np.mean(y)

    num = 0
    den = 0
    for i in range(len(x)): # This represents our sums
        num = num + (x[i] - x_avg)*(y[i] - y_avg) # Our numerator
        den = den + (x[i] - x_avg)**2 # Our denominator
    # Calculate slope
    m = num / den
    # Calculate intercept
    b = y_avg - m*x_avg

    print (m, b)
    
    # Calculate our predicted y values
    y_pred = m*x + b
    
    return y_pred
```

```python
Y_pred = lin_reg(X,Y)
```

```python
subset.plot.scatter(x='Date', y='Avg Daily Max Air Temperature (F)',c=subset['color'])
plt.plot([min(subset['Date'].values), max(subset['Date'].values)], [min(Y_pred), max(Y_pred)], color='red') # best fit line
plt.show()
```

>9) What are the slope and intercept of your best fit line?

```python

```

>10) What are the minimum and maximum Y values of your best fit line? Is your slope positive or negative?

```python

```

## Putting it all together


>11) Generate a best fit line for the full data set and plot the line over top of the data.

```python

```

```python

```

>12) Is the slope positive or negative? What do you think that means?

```python

```
