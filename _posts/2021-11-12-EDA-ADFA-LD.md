---
layout: post
title: "[EDA] ADFA-LD"
tags: EDA ADFA-LD
author: "Pranjal Chakraborty"
---

```python
import os
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
import seaborn as sns
sns.set(rc={'figure.figsize':(11.7,8.27)})
```


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

```
