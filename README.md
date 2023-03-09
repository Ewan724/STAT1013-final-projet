---
jupyter:
  colab:
  kernelspec:
    display_name: Python 3
    name: python3
  language_info:
    name: python
  nbformat: 4
  nbformat_minor: 0
---

<div class="cell markdown" id="9xZnRXM7x0Cv">

# CUHK-STAT1013: Practical Assignment Part 1: Sharing Your Idea and Data

</div>

<div class="cell markdown" id="9Fy05KAkyJI0">

## Titanic dataset background

**Description**:

Dataset describe the global monthly mean temperature using the data from
GISS Surface Temperature (GISTEMP) analysis and the global component of
Climate at a Glance (GCAG). The dataset includes the mean temperature in
Celsius from 1880 to December 2016. In order to avoid any inconsistency
due to mixing data from different sources, we only consider the data
from GCAG.

**Github**:
<https://github.com/datasets/global-temp/blob/master/data/monthly.csv>

**Sample size**: 1,644

**Feature documentation**:

| Column | Count | Dtype  |
|--------|-------|--------|
| Source | 1644  | object |
| Date   | 1644  | object |
| Mean   | 1644  | floa64 |

</div>

<div class="cell markdown" id="k85zO7zxys4H">

## Hypothesis

-   Tell us what your idea is and why you have chosen to pursue this
    idea.
    -   As global warming seems to be on everyone's lips, everybody know
        the temperature nowaday are significantly higher then that in
        before. So, I would like to ask a question, "*Do the temperature
        in recent years really higher than that in before?*"
-   What two groups you are comparing:
    -   **G1**: the average global mean temperature from 1987 to 2016;
        **G2**: the average global mean temperature from 1880 to 1909
-   What you will be measuring (i.e., what your response variable will
    be)
    -   `Mean`
-   Is your response variable quantitative rather than categorical?
    -   `Mean` is numerical data, showing data in temperature form,
        which can be regarded as a quantitative variable.
-   Make a prediction about what kind of difference you expect to see
    between your samples and WHY.
    -   We'd expect that **G1** \> **G2** since [the existence of global
        warming is well proved by numerous scientific
        research](https://climate.nasa.gov/scientific-consensus/).
-   Talk about how you will gather your data
    -   From Github link:
        <https://github.com/datasets/global-temp/blob/master/data/monthly.csv>
-   If you had unlimited resources (time, money, staff, etc.) how would
    you collect your data?
    -   \(i\) Attempt to get more detailed data, such as daily mean
        temperature or city specific data
    -   \(ii\) investigate if the provided dataset is reliable source to
        get the temperature related information.

</div>

<div class="cell markdown" id="3GOdPWT03PQB">

## Prepare your dataset

</div>

<div class="cell code" execution_count="44"
colab="{&quot;base_uri&quot;:&quot;https://localhost:8080/&quot;,&quot;height&quot;:206}"
id="mUxJb4hxvpHQ" outputId="a3fb4f77-e46b-41b3-95b1-918f657f70a8">

``` python
## load dataset from github

import pandas as pd

df = pd.read_csv('https://raw.githubusercontent.com/datasets/global-temp/master/data/monthly.csv')
df = df[df['Source'] == 'GCAG']
df.head(5)
```

<div class="output execute_result" execution_count="44">

      Source     Date    Mean
    0   GCAG  2016-12  0.7895
    2   GCAG  2016-11  0.7504
    4   GCAG  2016-10  0.7292
    6   GCAG  2016-09  0.8767
    8   GCAG  2016-08  0.8998

</div>

</div>

<div class="cell code" execution_count="45"
colab="{&quot;base_uri&quot;:&quot;https://localhost:8080/&quot;}"
id="FjGowdT9OkOf" outputId="f6da0fff-c9ff-4ff9-acc0-bd9352c3afd4">

``` python
df.info()
```

<div class="output stream stdout">

    <class 'pandas.core.frame.DataFrame'>
    Int64Index: 1644 entries, 0 to 3286
    Data columns (total 3 columns):
     #   Column  Non-Null Count  Dtype  
    ---  ------  --------------  -----  
     0   Source  1644 non-null   object 
     1   Date    1644 non-null   object 
     2   Mean    1644 non-null   float64
    dtypes: float64(1), object(2)
    memory usage: 51.4+ KB

</div>

</div>

<div class="cell markdown" id="55xAIxVa3hpQ">

-   Tell us what groups you want to compare in the dataset
    -   **G1** (Mean \| Date:1987/01-2016/12) vs. **G2** (Mean \|
        Date:1880/01-1909/12)

</div>

<div class="cell markdown" id="13PdL3ht3902">

-   Print first 5 records of each group, respectively.

</div>

<div class="cell code" execution_count="46"
colab="{&quot;base_uri&quot;:&quot;https://localhost:8080/&quot;}"
id="UNL0WXav3hLj" outputId="afd106db-cc8d-4ba7-a2bd-57d16cebd369">

``` python
## First 5 records of G1 (1987/01-2016/12)
G1 = df[(df['Date'] <= '2016-12') & (df['Date'] >= '1987-01')]
(G1['Mean']).head(5)
```

<div class="output execute_result" execution_count="46">

    0    0.7895
    2    0.7504
    4    0.7292
    6    0.8767
    8    0.8998
    Name: Mean, dtype: float64

</div>

</div>

<div class="cell code" execution_count="47"
colab="{&quot;base_uri&quot;:&quot;https://localhost:8080/&quot;}"
id="dhe52HVB4T1O" outputId="5d041ae8-d165-4f02-ec70-3e961a3d98de">

``` python
## First 5 records of G2 (1880/01-1909/12)
G2 = df[(df['Date'] <= '1909-12') & (df['Date'] >= '1880-01')]
(G2['Mean']).head(5)
```

<div class="output execute_result" execution_count="47">

    2568   -0.4071
    2570   -0.2733
    2572   -0.3935
    2574   -0.3611
    2576   -0.3052
    Name: Mean, dtype: float64

</div>

</div>

<div class="cell code" execution_count="48"
colab="{&quot;base_uri&quot;:&quot;https://localhost:8080/&quot;,&quot;height&quot;:534}"
id="zEgfWXaKGvNC" outputId="33433777-cdbf-41d0-aa80-ee6321ff6447">

``` python
## Any other data description and visualization you want to add.

## Open question, be flexible and no example can be provided.

## plot the line graph for G1 and G2 in the same diagram
import seaborn as sns
## add column 'Month' for indexing
month = range(360, 0, -1)
G1.loc[:, 'Month'] = month
G2.loc[:, 'Month'] = month

## concatenate G1 and G2, and assign tag 'G1' and 'G2' to both dataset
concatenated = pd.concat([G1.assign(dataset='G1'), G2.assign(dataset='G2')])
concatenated
```

<div class="output stream stderr">

    /usr/local/lib/python3.8/dist-packages/pandas/core/indexing.py:1667: SettingWithCopyWarning: 
    A value is trying to be set on a copy of a slice from a DataFrame.
    Try using .loc[row_indexer,col_indexer] = value instead

    See the caveats in the documentation: https://pandas.pydata.org/pandas-docs/stable/user_guide/indexing.html#returning-a-view-versus-a-copy
      self.obj[key] = value

</div>

<div class="output execute_result" execution_count="48">

         Source     Date    Mean  Month dataset
    0      GCAG  2016-12  0.7895    360      G1
    2      GCAG  2016-11  0.7504    359      G1
    4      GCAG  2016-10  0.7292    358      G1
    6      GCAG  2016-09  0.8767    357      G1
    8      GCAG  2016-08  0.8998    356      G1
    ...     ...      ...     ...    ...     ...
    3278   GCAG  1880-05 -0.0738      5      G2
    3280   GCAG  1880-04 -0.0499      4      G2
    3282   GCAG  1880-03 -0.1357      3      G2
    3284   GCAG  1880-02 -0.1229      2      G2
    3286   GCAG  1880-01  0.0009      1      G2

    [720 rows x 5 columns]

</div>

</div>

<div class="cell code" execution_count="50"
colab="{&quot;base_uri&quot;:&quot;https://localhost:8080/&quot;,&quot;height&quot;:297}"
id="RFR_8TQNlvQr" outputId="0773fbc7-18e3-4ff9-8ea3-d1ffec7137eb">

``` python
##plotting the line graph
sns.lineplot(data = concatenated, x = 'Month', y = 'Mean', hue = 'dataset')
```

<div class="output execute_result" execution_count="50">

    <AxesSubplot:xlabel='Month', ylabel='Mean'>

</div>

<div class="output display_data">

![](5b0410f8f51ce4aace64f762eb5f3521586d060e.png)

</div>

</div>
