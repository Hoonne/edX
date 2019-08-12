
# Add data with newest dataset ( WDI 2019 ) 

`now_data` is given data by edX  
`new_data` is newest data from worldbank

However, Format of the dataset's table is differnt.  
so It was difficult to join two table simply.  
Let's check how differnt two tables.


```python
import numpy as np
import pandas as pd

path = '../Week-5-Visualization/world-development-indicators/Indicators.csv'
now_data = pd.read_csv(path)

path2 = './WDI_csv/WDIData.csv'
new_data = pd.read_csv(path2)
```


```python
now_data.head()
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
      <th>CountryName</th>
      <th>CountryCode</th>
      <th>IndicatorName</th>
      <th>IndicatorCode</th>
      <th>Year</th>
      <th>Value</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Arab World</td>
      <td>ARB</td>
      <td>Adolescent fertility rate (births per 1,000 wo...</td>
      <td>SP.ADO.TFRT</td>
      <td>1960</td>
      <td>1.335609e+02</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Arab World</td>
      <td>ARB</td>
      <td>Age dependency ratio (% of working-age populat...</td>
      <td>SP.POP.DPND</td>
      <td>1960</td>
      <td>8.779760e+01</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Arab World</td>
      <td>ARB</td>
      <td>Age dependency ratio, old (% of working-age po...</td>
      <td>SP.POP.DPND.OL</td>
      <td>1960</td>
      <td>6.634579e+00</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Arab World</td>
      <td>ARB</td>
      <td>Age dependency ratio, young (% of working-age ...</td>
      <td>SP.POP.DPND.YG</td>
      <td>1960</td>
      <td>8.102333e+01</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Arab World</td>
      <td>ARB</td>
      <td>Arms exports (SIPRI trend indicator values)</td>
      <td>MS.MIL.XPRT.KD</td>
      <td>1960</td>
      <td>3.000000e+06</td>
    </tr>
  </tbody>
</table>
</div>



As you can see now_data looks like above.  
Otherwise, new_data does not have Year field, but it has many fields by each years like below.


```python
new_data.head()
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
      <th>Country Name</th>
      <th>Country Code</th>
      <th>Indicator Name</th>
      <th>Indicator Code</th>
      <th>1960</th>
      <th>1961</th>
      <th>1962</th>
      <th>1963</th>
      <th>1964</th>
      <th>1965</th>
      <th>...</th>
      <th>2010</th>
      <th>2011</th>
      <th>2012</th>
      <th>2013</th>
      <th>2014</th>
      <th>2015</th>
      <th>2016</th>
      <th>2017</th>
      <th>2018</th>
      <th>Unnamed: 63</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Arab World</td>
      <td>ARB</td>
      <td>2005 PPP conversion factor, GDP (LCU per inter...</td>
      <td>PA.NUS.PPP.05</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>...</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Arab World</td>
      <td>ARB</td>
      <td>2005 PPP conversion factor, private consumptio...</td>
      <td>PA.NUS.PRVT.PP.05</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>...</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Arab World</td>
      <td>ARB</td>
      <td>Access to clean fuels and technologies for coo...</td>
      <td>EG.CFT.ACCS.ZS</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>...</td>
      <td>82.368101</td>
      <td>82.783289</td>
      <td>83.120303</td>
      <td>83.533457</td>
      <td>83.897596</td>
      <td>84.171599</td>
      <td>84.510171</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Arab World</td>
      <td>ARB</td>
      <td>Access to electricity (% of population)</td>
      <td>EG.ELC.ACCS.ZS</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>...</td>
      <td>86.007620</td>
      <td>86.428272</td>
      <td>87.070576</td>
      <td>88.176836</td>
      <td>87.342739</td>
      <td>89.130121</td>
      <td>89.678685</td>
      <td>90.273687</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Arab World</td>
      <td>ARB</td>
      <td>Access to electricity, rural (% of rural popul...</td>
      <td>EG.ELC.ACCS.RU.ZS</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>...</td>
      <td>73.466653</td>
      <td>73.942103</td>
      <td>75.244104</td>
      <td>77.162305</td>
      <td>75.538976</td>
      <td>78.741152</td>
      <td>79.665635</td>
      <td>80.749293</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
  </tbody>
</table>
<p>5 rows × 64 columns</p>
</div>



This is how i add new datas.   


```python
def add_data(now_data,new_data):
    dict_list =[]
    for i in picked_indicators_code :
        nowdata = now_data[now_data['IndicatorCode'] == i]
        add_year = nowdata['Year'].max() + 1
        last = len(now_data)
        while add_year < 2019 :
            filter1 = new_data['Indicator Code'] == i
            filter2 = new_data['Country Name'].isin(now_data['CountryName'])
            target = new_data[filter1 & filter2]
            theyear = int(add_year)
            try:
                added_data ={
                    'CountryName' : target['Country Name'].values[0],
                    'CountryCode': target['Country Code'].values[0],
                    'IndicatorName':target['Indicator Name'].values[0],
                    'IndicatorCode': target['Indicator Code'].values[0],
                    'Year':theyear,
                    'Value':target[str(add_year)].values[0]
                }
            except:
                added_data ={
                    'CountryName' : None,
                    'CountryCode': None,
                    'IndicatorName':None,
                    'IndicatorCode': None,
                    'Year':None,
                    'Value':None
                }
            dict_list.append(added_data)
            add_year = add_year + 1
    now_data = now_data.append(dict_list,ignore_index=True)
    return now_data
```
