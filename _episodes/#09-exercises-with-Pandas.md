---
title: Exercises with Pandas
teaching: 0
exercises: 1 hour 45
objectives:
    - Importing necessary libraries to manipulate data
    - Use Pandas to read data from excel
    - Manipulate the Pandas DataFrames to retrieve the necessary information
---

## Exercise 1: Import libraries and retrieve dynamic information

```python
import datetime as dt
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
```

```python
today = dt.date.today()
```

## Exercise 2: Load the earnings and benefits datasets using Pandas

```python
earnings = pd.read_excel('earnings.xlsx')
benefits = pd.read_excel('benefits.xlsx')
```

## Exercise 3: Check for duplicated IDs in both datasets

```python
any(earnings['ID'].duplicated())
```

```python
any(benefits['ID'].duplicated())
```

## Exercise 4: Are there any missing IDs from either of the datasets?

```python
# All the IDs in earnings are present in benefits!
len(set(earnings['ID']).difference(benefits['ID']))>0
```

```python
# Not all the IDs in benefits are present in earnings!
len(set(benefits['ID']).difference(earnings['ID']))>0
```

## Exercise 5: Join the two datasets on the ID column

```python
df = pd.merge(benefits, earnings, on='ID')
print(df)
```

## Exercise 6: Count of individuals above a certain age threshold.

```python
ans = ((today.year - df['YOB']) > 23).sum()
print(ans)
```

```python
ans = ((today.year - df['YOB']) > 95).sum()
print(ans)
```

## Exercise 7: Do we have people above or below a certain age / income threshold in the sample (also given some other features like given that they receive disability benefits)?

```python
# People above or below a certain age
ans = ((today.year - df['YOB']) > 23).sum() > 0.
print(ans)
```

```python
ans = ((today.year - df['YOB']) < 95).sum() > 0.
print(ans)
```

```python
# People above or below a certain income threshold
income_threshold = 1000
ans = (df["SSTE2003"]<income_threshold).sum() > 0.
print(ans)
```

```python
# People above or below a certain age and disability benefits
ans = (((today.year - df['YOB']) > 23) & (df['OTOB']=="b'A'")).sum() > 0.
print(ans)
```

## Exercise 8: Is your income zero or your retirement capital zero?

```python
income_threshold = 0
ans = (df["SSTE2003"]==income_threshold).sum() > 0.
print(ans)
```

## Exercise 9: Calculate the sum of retirement capital given certain conditions


```python
age_threshold = 99.
ans = df[((today.year - df['YOB']) > age_threshold)]["MBC"].sum()
print(ans)
```