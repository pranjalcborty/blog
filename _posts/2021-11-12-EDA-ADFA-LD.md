---
layout: post
title: "[EDA] ADFA-LD (in progress)"
tags: EDA ADFA-LD
published: false
author: "Pranjal Chakraborty"
---

```python
import os
import seaborn as sns
sns.set(rc={'figure.figsize':(11.7,8.27)})
```


```python
sum([len(files) for r, d, files in os.walk("ADFA-LD/Attack_Data_Master")])
```




    746




```python
attack_types = ["UAD-Adduser", "UAD-Hydra-FTP", "UAD-Hydra-SSH", "UAD-Java-Meterpreter", "UAD-Meterpreter", "UAD-WS"]
```


```python
from collections import defaultdict
data_count_dict = defaultdict(lambda: 0)
```


```python
for r, d, files in os.walk("ADFA-LD/Attack_Data_Master"):
    for attack_type in attack_types:
        count = len([file_name for file_name in files if file_name.startswith(attack_type)])
        data_count_dict[attack_type] += count
```


```python
data_count_dict
```




    defaultdict(<function __main__.<lambda>()>,
                {'UAD-Adduser': 91,
                 'UAD-Hydra-FTP': 162,
                 'UAD-Hydra-SSH': 176,
                 'UAD-Java-Meterpreter': 124,
                 'UAD-Meterpreter': 75,
                 'UAD-WS': 118})




```python
keys = list(data_count_dict.keys())
sns.barplot(
    x = keys,
    y = [data_count_dict[k] for k in keys]
)
```




    <AxesSubplot:>




    
![image](/blog/assets/images/1.png)
    



```python
sum([len(files) for r, d, files in os.walk("ADFA-LD/Training_Data_Master")])
```




    833



### Creating the pandas datatable


```python
df_dict = { 'data': list(), 'attack': list()}

for r, d, files in os.walk("ADFA-LD/Attack_Data_Master"):
    for file in files:
        with open(os.path.join(r, file), 'r') as f:
            df_dict['data'].append(f.read())
            df_dict['attack'].append(1)
```


```python
for r, d, files in os.walk("ADFA-LD/Training_Data_Master"):
    for file in files:
        with open(os.path.join(r, file), 'r') as f:
            df_dict['data'].append(f.read())
            df_dict['attack'].append(0)
```


```python
import pandas as pd

df = pd.DataFrame.from_dict(df_dict)
```


```python
df.head()
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
      <th>data</th>
      <th>attack</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>265 168 168 265 168 168 168 265 168 265 168 16...</td>
      <td>1</td>
    </tr>
    <tr>
      <th>1</th>
      <td>3 104 91 265 142 142 104 3 175 3 142 142 146 1...</td>
      <td>1</td>
    </tr>
    <tr>
      <th>2</th>
      <td>265 43 3 265 43 168 265 168 168 168 3 43 168 3...</td>
      <td>1</td>
    </tr>
    <tr>
      <th>3</th>
      <td>309 54 309 309 54 309 54 54 54 3 54 54 3 54 54...</td>
      <td>1</td>
    </tr>
    <tr>
      <th>4</th>
      <td>168 3 168 168 168 265 265 265 168 168 265 168 ...</td>
      <td>1</td>
    </tr>
  </tbody>
</table>
</div>




```python
df['list_data'] = df['data'].apply(lambda x: [int(strNum) for strNum in x.split()])
```


```python
from tensorflow.keras.preprocessing.sequence import pad_sequences
df['list_data'] = pad_sequences(df['list_data']).tolist()
```


```python
from sklearn.model_selection import train_test_split
```


```python
train_df, test_df = train_test_split(df, test_size = 0.2)
```


```python
print(train_df.shape)
print(test_df.shape)
print(df.shape)
```

    (1263, 3)
    (316, 3)
    (1579, 3)
    


```python
train_df.head()
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
      <th>data</th>
      <th>attack</th>
      <th>list_data</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>400</th>
      <td>162 162 162 162 114 162 114 162 114 162 114 11...</td>
      <td>1</td>
      <td>[0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, ...</td>
    </tr>
    <tr>
      <th>156</th>
      <td>91 5 140 197 192 140 142 91 91 91 91 78 3 3 3 ...</td>
      <td>1</td>
      <td>[0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, ...</td>
    </tr>
    <tr>
      <th>923</th>
      <td>6 174 174 174 11 45 33 192 33 5 197 192 6 33 5...</td>
      <td>0</td>
      <td>[0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, ...</td>
    </tr>
    <tr>
      <th>1048</th>
      <td>104 104 104 174 174 174 174 174 174 174 174 17...</td>
      <td>0</td>
      <td>[0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, ...</td>
    </tr>
    <tr>
      <th>1363</th>
      <td>6 11 192 6 192 125 125 6 45 45 197 174 45 5 45...</td>
      <td>0</td>
      <td>[0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, ...</td>
    </tr>
  </tbody>
</table>
</div>




```python
train_x = train_df['list_data']
test_x = test_df['list_data']
```


```python
train_y = train_df['attack']
test_y = test_df['attack']
```


```python
train_x = pd.DataFrame(train_x.to_list())
test_x = pd.DataFrame(test_x.to_list())
```


```python
import numpy as np

train_x = np.asarray(train_x).astype('float32')
train_y = np.asarray(train_y).astype('float32')
```


```python
from sklearn.linear_model import LogisticRegression

model = LogisticRegression(max_iter=100000, verbose=1)
```


```python
model.fit(train_x, train_y)
```

    [Parallel(n_jobs=1)]: Using backend SequentialBackend with 1 concurrent workers.
    [Parallel(n_jobs=1)]: Done   1 out of   1 | elapsed:   33.1s finished
    




    LogisticRegression(max_iter=100000, verbose=1)




```python
model.score(test_x, test_y)
```




    0.5284810126582279




```python
from sklearn import svm
```


```python
model = svm.SVC(kernel='linear', verbose=1)
```


```python
model.fit(train_x, train_y)
```

    [LibSVM]


```python
from sklearn import metrics
pred_y = model.predict(test_x)
print(metrics.accuracy_score(test_y, pred_y))
```




    0.617965402975497



