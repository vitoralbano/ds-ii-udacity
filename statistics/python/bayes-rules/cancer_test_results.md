
# Cancer Test Results


```python
import pandas as pd
```


```python
# load dataset
df = pd.read_csv('cancer_test_data.csv')

df.head(10)
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>patient_id</th>
      <th>test_result</th>
      <th>has_cancer</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>79452</td>
      <td>Negative</td>
      <td>False</td>
    </tr>
    <tr>
      <th>1</th>
      <td>81667</td>
      <td>Positive</td>
      <td>True</td>
    </tr>
    <tr>
      <th>2</th>
      <td>76297</td>
      <td>Negative</td>
      <td>False</td>
    </tr>
    <tr>
      <th>3</th>
      <td>36593</td>
      <td>Negative</td>
      <td>False</td>
    </tr>
    <tr>
      <th>4</th>
      <td>53717</td>
      <td>Negative</td>
      <td>False</td>
    </tr>
    <tr>
      <th>5</th>
      <td>67134</td>
      <td>Negative</td>
      <td>False</td>
    </tr>
    <tr>
      <th>6</th>
      <td>40436</td>
      <td>Negative</td>
      <td>False</td>
    </tr>
    <tr>
      <th>7</th>
      <td>77872</td>
      <td>Positive</td>
      <td>True</td>
    </tr>
    <tr>
      <th>8</th>
      <td>78761</td>
      <td>Positive</td>
      <td>True</td>
    </tr>
    <tr>
      <th>9</th>
      <td>71212</td>
      <td>Negative</td>
      <td>False</td>
    </tr>
  </tbody>
</table>
</div>




```python
# number of patients
df.patient_id.nunique()

```




    2914




```python
# number of patients with cancer
df.loc[df.has_cancer == True].shape[0]
```




    306




```python
# number of patients without cancer
df.loc[df.has_cancer == False].shape[0]
```




    2608




```python
# proportion of patients with cancer
p_a = (df.has_cancer == True).mean()
p_a
```




    0.10501029512697323




```python
# proportion of patients without cancer
p_b = (df.has_cancer == False).mean()
p_b
```




    0.8949897048730268




```python
# proportion of patients with cancer who test positive
df_has_cancer = df.loc[df.has_cancer == True]

p_pos_a = (df_has_cancer.test_result == 'Positive').mean()
p_pos_a
```




    0.9052287581699346




```python
# proportion of patients with cancer who test negative
p_neg_a = (df_has_cancer.test_result == 'Negative').mean()
p_neg_a
```




    0.09477124183006536




```python
# proportion of patients without cancer who test positive
df_no_cancer = df.loc[df.has_cancer == False]

p_pos_b = (df_no_cancer.test_result == 'Positive').mean()
p_pos_b
```




    0.2036042944785276




```python
# proportion of patients without cancer who test negative
p_neg_b = (df_no_cancer.test_result == 'Negative').mean()
p_neg_b
```




    0.7963957055214724




```python
# proportion of positive tests
p_pos = (df.test_result == 'Positive').mean()
p_pos
```




    0.2772820864790666




```python
# proportion of negative tests
p_neg = (df.test_result == 'Negative').mean()
p_neg
```




    0.7227179135209334



# Conditional Probability & Bayes Rule Quiz (without scikit)


```python
# Load dataset
```


```python
# What proportion of patients who tested positive has cancer?
p_a_pos = (p_pos_a * p_a) / p_pos
p_a_pos
```




    0.3428217821782178




```python
# What proportion of patients who tested positive doesn't have cancer?
p_b_pos = (p_pos_b * p_b) / p_pos
p_b_pos
```




    0.6571782178217821




```python
# What proportion of patients who tested negative has cancer?
p_a_neg = (p_neg_a * p_a) / p_neg
p_a_neg
```




    0.013770180436847102




```python
# What proportion of patients who tested negative doesn't have cancer?
p_b_neg = (p_neg_b * p_b) / p_neg
p_b_neg
```




    0.9862298195631529


