```python
'''
env
Python 3.10.3
scikit-learn==1.0.2
scipy==1.8.0
'''

'''
load data from localized tools and calculate correlated score
'''
import re
import os
import pandas as pd

out_dir = "./output"
os.makedirs(out_dir,exist_ok=True)

localized_data = pd.read_csv("./raw-data/raw-quantitative - localized tool.csv",encoding="utf_8_sig")
localized_data = localized_data\
    .rename(columns={x:re.search(r'.\d+',x).group(0) for x in localized_data.columns[4:]})
l=localized_data.copy()

l["B-2"]=l["L11"]/5*4
l["B-3"]=l["L11"]/5*4
l["B-4"]=(l["L3"]/2*3+l["L4"]/2*3+l["L5"])/7*4
l["B-5"]= l["L1"]*3+1
l["B-6"]= 1
l.loc[l["L2"].str.contains("A",na=False),"B-6"]=l["B-6"]+1.5
l.loc[l["L2"].str.contains("B",na=False),"B-6"]=l["B-6"]+1.5
l["B-9"]= (l["L6"]+l["L7"]/2*3+l["L8"])/8*4

localized_data=l.copy()
localized_data.to_csv(f"{out_dir}/calculated_localized_data.csv",encoding="utf_8_sig")

localized_data



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
      <th>time period</th>
      <th>learner</th>
      <th>assessor</th>
      <th>double-assessment</th>
      <th>L1</th>
      <th>L2</th>
      <th>L3</th>
      <th>L4</th>
      <th>L5</th>
      <th>L6</th>
      <th>...</th>
      <th>L8</th>
      <th>L9</th>
      <th>L10</th>
      <th>L11</th>
      <th>B-2</th>
      <th>B-3</th>
      <th>B-4</th>
      <th>B-5</th>
      <th>B-6</th>
      <th>B-9</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>L-A</td>
      <td>A-S</td>
      <td>NaN</td>
      <td>1</td>
      <td>A</td>
      <td>2</td>
      <td>1</td>
      <td>1</td>
      <td>2</td>
      <td>...</td>
      <td>1</td>
      <td>NaN</td>
      <td>blood sampling,establish peripheral vascular a...</td>
      <td>3</td>
      <td>2.4</td>
      <td>2.4</td>
      <td>3.142857</td>
      <td>4</td>
      <td>2.5</td>
      <td>2.25</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1</td>
      <td>L-T</td>
      <td>A-S</td>
      <td>NaN</td>
      <td>1</td>
      <td>A</td>
      <td>1</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>...</td>
      <td>1</td>
      <td>NaN</td>
      <td>establish peripheral vascular access, make adm...</td>
      <td>2</td>
      <td>1.6</td>
      <td>1.6</td>
      <td>1.714286</td>
      <td>4</td>
      <td>2.5</td>
      <td>1.25</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2</td>
      <td>L-M</td>
      <td>A-S</td>
      <td>NaN</td>
      <td>0</td>
      <td>NaN</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>2</td>
      <td>...</td>
      <td>3</td>
      <td>NaN</td>
      <td>establish peripheral vascular access, transfer...</td>
      <td>3</td>
      <td>2.4</td>
      <td>2.4</td>
      <td>2.285714</td>
      <td>1</td>
      <td>1.0</td>
      <td>4.00</td>
    </tr>
    <tr>
      <th>3</th>
      <td>2</td>
      <td>L-A</td>
      <td>A-S</td>
      <td>NaN</td>
      <td>1</td>
      <td>A</td>
      <td>2</td>
      <td>1</td>
      <td>3</td>
      <td>2</td>
      <td>...</td>
      <td>3</td>
      <td>NaN</td>
      <td>establish peripheral vascular access, make adm...</td>
      <td>4</td>
      <td>3.2</td>
      <td>3.2</td>
      <td>4.285714</td>
      <td>4</td>
      <td>2.5</td>
      <td>4.00</td>
    </tr>
    <tr>
      <th>4</th>
      <td>2</td>
      <td>L-T</td>
      <td>A-S</td>
      <td>NaN</td>
      <td>1</td>
      <td>A</td>
      <td>2</td>
      <td>1</td>
      <td>1</td>
      <td>2</td>
      <td>...</td>
      <td>3</td>
      <td>NaN</td>
      <td>establish peripheral vascular access, make adm...</td>
      <td>3</td>
      <td>2.4</td>
      <td>2.4</td>
      <td>3.142857</td>
      <td>4</td>
      <td>2.5</td>
      <td>4.00</td>
    </tr>
    <tr>
      <th>5</th>
      <td>3</td>
      <td>L-H</td>
      <td>A-K</td>
      <td>NaN</td>
      <td>1</td>
      <td>A</td>
      <td>2</td>
      <td>1</td>
      <td>2</td>
      <td>3</td>
      <td>...</td>
      <td>3</td>
      <td>NaN</td>
      <td>establish peripheral vascular access, make adm...</td>
      <td>4</td>
      <td>3.2</td>
      <td>3.2</td>
      <td>3.714286</td>
      <td>4</td>
      <td>2.5</td>
      <td>4.50</td>
    </tr>
    <tr>
      <th>6</th>
      <td>3</td>
      <td>L-T</td>
      <td>A-K</td>
      <td>1.0</td>
      <td>1</td>
      <td>A</td>
      <td>2</td>
      <td>2</td>
      <td>2</td>
      <td>2</td>
      <td>...</td>
      <td>3</td>
      <td>NaN</td>
      <td>make initial assessment on admission</td>
      <td>4</td>
      <td>3.2</td>
      <td>3.2</td>
      <td>4.571429</td>
      <td>4</td>
      <td>2.5</td>
      <td>4.00</td>
    </tr>
    <tr>
      <th>7</th>
      <td>3</td>
      <td>L-T</td>
      <td>A-O</td>
      <td>1.0</td>
      <td>1</td>
      <td>A</td>
      <td>2</td>
      <td>1</td>
      <td>2</td>
      <td>3</td>
      <td>...</td>
      <td>3</td>
      <td>NaN</td>
      <td>make a document related to admission</td>
      <td>4</td>
      <td>3.2</td>
      <td>3.2</td>
      <td>3.714286</td>
      <td>4</td>
      <td>2.5</td>
      <td>4.50</td>
    </tr>
    <tr>
      <th>8</th>
      <td>5</td>
      <td>L-H</td>
      <td>A-O</td>
      <td>NaN</td>
      <td>1</td>
      <td>A</td>
      <td>2</td>
      <td>1</td>
      <td>2</td>
      <td>2</td>
      <td>...</td>
      <td>3</td>
      <td>NaN</td>
      <td>make a document related to admission</td>
      <td>4</td>
      <td>3.2</td>
      <td>3.2</td>
      <td>3.714286</td>
      <td>4</td>
      <td>2.5</td>
      <td>3.25</td>
    </tr>
    <tr>
      <th>9</th>
      <td>6</td>
      <td>L-H</td>
      <td>A-O</td>
      <td>NaN</td>
      <td>1</td>
      <td>A</td>
      <td>2</td>
      <td>1</td>
      <td>2</td>
      <td>2</td>
      <td>...</td>
      <td>3</td>
      <td>NaN</td>
      <td>make a document related to admission</td>
      <td>4</td>
      <td>3.2</td>
      <td>3.2</td>
      <td>3.714286</td>
      <td>4</td>
      <td>2.5</td>
      <td>4.00</td>
    </tr>
    <tr>
      <th>10</th>
      <td>6</td>
      <td>L-K</td>
      <td>A-O</td>
      <td>NaN</td>
      <td>1</td>
      <td>NaN</td>
      <td>2</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>...</td>
      <td>2</td>
      <td>NaN</td>
      <td>make a document related to admission</td>
      <td>3</td>
      <td>2.4</td>
      <td>2.4</td>
      <td>3.142857</td>
      <td>4</td>
      <td>1.0</td>
      <td>2.25</td>
    </tr>
    <tr>
      <th>11</th>
      <td>7</td>
      <td>L-K</td>
      <td>A-S</td>
      <td>NaN</td>
      <td>1</td>
      <td>A</td>
      <td>1</td>
      <td>2</td>
      <td>1</td>
      <td>1</td>
      <td>...</td>
      <td>1</td>
      <td>NaN</td>
      <td>establish peripheral vascular access,</td>
      <td>2</td>
      <td>1.6</td>
      <td>1.6</td>
      <td>3.142857</td>
      <td>4</td>
      <td>2.5</td>
      <td>1.75</td>
    </tr>
    <tr>
      <th>12</th>
      <td>7</td>
      <td>L-H</td>
      <td>A-S</td>
      <td>NaN</td>
      <td>1</td>
      <td>A</td>
      <td>1</td>
      <td>2</td>
      <td>2</td>
      <td>2</td>
      <td>...</td>
      <td>3</td>
      <td>NaN</td>
      <td>establish peripheral vascular access,communica...</td>
      <td>4</td>
      <td>3.2</td>
      <td>3.2</td>
      <td>3.714286</td>
      <td>4</td>
      <td>2.5</td>
      <td>4.00</td>
    </tr>
    <tr>
      <th>13</th>
      <td>8</td>
      <td>L-K</td>
      <td>A-K</td>
      <td>NaN</td>
      <td>1</td>
      <td>A</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>2</td>
      <td>...</td>
      <td>3</td>
      <td>NaN</td>
      <td>history taking, physical examincation, make in...</td>
      <td>3</td>
      <td>2.4</td>
      <td>2.4</td>
      <td>2.285714</td>
      <td>4</td>
      <td>2.5</td>
      <td>3.25</td>
    </tr>
    <tr>
      <th>14</th>
      <td>8</td>
      <td>L-Y</td>
      <td>A-K</td>
      <td>NaN</td>
      <td>1</td>
      <td>A</td>
      <td>1</td>
      <td>1</td>
      <td>2</td>
      <td>3</td>
      <td>...</td>
      <td>3</td>
      <td>NaN</td>
      <td>establish peripheral vascular access,make a pl...</td>
      <td>4</td>
      <td>3.2</td>
      <td>3.2</td>
      <td>2.857143</td>
      <td>4</td>
      <td>2.5</td>
      <td>4.50</td>
    </tr>
    <tr>
      <th>15</th>
      <td>9</td>
      <td>L-KR</td>
      <td>A-S</td>
      <td>NaN</td>
      <td>1</td>
      <td>A</td>
      <td>2</td>
      <td>1</td>
      <td>1</td>
      <td>2</td>
      <td>...</td>
      <td>2</td>
      <td>NaN</td>
      <td>establish peripheral root, order blood test, c...</td>
      <td>4</td>
      <td>3.2</td>
      <td>3.2</td>
      <td>3.142857</td>
      <td>4</td>
      <td>2.5</td>
      <td>3.50</td>
    </tr>
    <tr>
      <th>16</th>
      <td>10</td>
      <td>L-KA</td>
      <td>A-O</td>
      <td>NaN</td>
      <td>1</td>
      <td>NaN</td>
      <td>2</td>
      <td>2</td>
      <td>3</td>
      <td>3</td>
      <td>...</td>
      <td>3</td>
      <td>NaN</td>
      <td>make a document related to admission</td>
      <td>4</td>
      <td>3.2</td>
      <td>3.2</td>
      <td>5.142857</td>
      <td>4</td>
      <td>1.0</td>
      <td>3.75</td>
    </tr>
    <tr>
      <th>17</th>
      <td>10</td>
      <td>L-W</td>
      <td>A-O</td>
      <td>NaN</td>
      <td>1</td>
      <td>NaN</td>
      <td>2</td>
      <td>1</td>
      <td>1</td>
      <td>3</td>
      <td>...</td>
      <td>1</td>
      <td>NaN</td>
      <td>make a document related to admission</td>
      <td>3</td>
      <td>2.4</td>
      <td>2.4</td>
      <td>3.142857</td>
      <td>4</td>
      <td>1.0</td>
      <td>2.75</td>
    </tr>
    <tr>
      <th>18</th>
      <td>11</td>
      <td>L-I</td>
      <td>A-S</td>
      <td>NaN</td>
      <td>1</td>
      <td>A</td>
      <td>2</td>
      <td>1</td>
      <td>2</td>
      <td>2</td>
      <td>...</td>
      <td>2</td>
      <td>NaN</td>
      <td>establish peripheral vascular access,communica...</td>
      <td>3</td>
      <td>2.4</td>
      <td>2.4</td>
      <td>3.714286</td>
      <td>4</td>
      <td>2.5</td>
      <td>3.50</td>
    </tr>
    <tr>
      <th>19</th>
      <td>11</td>
      <td>L-T</td>
      <td>A-S</td>
      <td>NaN</td>
      <td>1</td>
      <td>A</td>
      <td>2</td>
      <td>1</td>
      <td>1</td>
      <td>2</td>
      <td>...</td>
      <td>1</td>
      <td>NaN</td>
      <td>establish peripheral vascular access, make ini...</td>
      <td>3</td>
      <td>2.4</td>
      <td>2.4</td>
      <td>3.142857</td>
      <td>4</td>
      <td>2.5</td>
      <td>2.25</td>
    </tr>
  </tbody>
</table>
<p>20 rows × 21 columns</p>
</div>




```python
'''
load data from generic ruburic
'''

import pandas as pd
import re

generic_data = pd.read_csv("./raw-data/raw-quantitative - generic rubric.csv",encoding="utf_8_sig")
generic_data
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
      <th>time period</th>
      <th>learner</th>
      <th>assessor</th>
      <th>double-assessment</th>
      <th>B-1</th>
      <th>B-2</th>
      <th>B-3</th>
      <th>B-4</th>
      <th>B-5</th>
      <th>B-6</th>
      <th>B-7</th>
      <th>B-8</th>
      <th>B-9</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>L-A</td>
      <td>A-S</td>
      <td>NaN</td>
      <td>2.0</td>
      <td>2.0</td>
      <td>2.0</td>
      <td>2.5</td>
      <td>2.5</td>
      <td>2.0</td>
      <td>NaN</td>
      <td>2.0</td>
      <td>2.0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1</td>
      <td>L-T</td>
      <td>A-S</td>
      <td>NaN</td>
      <td>2.0</td>
      <td>1.5</td>
      <td>1.5</td>
      <td>1.5</td>
      <td>1.5</td>
      <td>2.0</td>
      <td>NaN</td>
      <td>1.5</td>
      <td>1.5</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2</td>
      <td>L-M</td>
      <td>A-S</td>
      <td>NaN</td>
      <td>2.0</td>
      <td>2.0</td>
      <td>2.5</td>
      <td>2.5</td>
      <td>2.5</td>
      <td>2.5</td>
      <td>2.0</td>
      <td>2.5</td>
      <td>2.0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>2</td>
      <td>L-A</td>
      <td>A-S</td>
      <td>NaN</td>
      <td>3.0</td>
      <td>3.0</td>
      <td>3.0</td>
      <td>3.0</td>
      <td>3.0</td>
      <td>3.0</td>
      <td>2.5</td>
      <td>3.0</td>
      <td>3.0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>2</td>
      <td>L-T</td>
      <td>A-S</td>
      <td>NaN</td>
      <td>2.0</td>
      <td>2.0</td>
      <td>2.5</td>
      <td>3.0</td>
      <td>2.0</td>
      <td>2.5</td>
      <td>2.0</td>
      <td>2.0</td>
      <td>2.0</td>
    </tr>
    <tr>
      <th>5</th>
      <td>3</td>
      <td>L-H</td>
      <td>A-K</td>
      <td>NaN</td>
      <td>3.0</td>
      <td>2.5</td>
      <td>3.0</td>
      <td>3.5</td>
      <td>3.5</td>
      <td>3.0</td>
      <td>NaN</td>
      <td>3.0</td>
      <td>3.5</td>
    </tr>
    <tr>
      <th>6</th>
      <td>3</td>
      <td>L-T</td>
      <td>A-K</td>
      <td>1.0</td>
      <td>3.0</td>
      <td>3.5</td>
      <td>2.5</td>
      <td>3.0</td>
      <td>3.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>3.5</td>
      <td>3.5</td>
    </tr>
    <tr>
      <th>7</th>
      <td>3</td>
      <td>L-T</td>
      <td>A-O</td>
      <td>1.0</td>
      <td>3.0</td>
      <td>3.0</td>
      <td>3.0</td>
      <td>3.5</td>
      <td>3.0</td>
      <td>3.5</td>
      <td>NaN</td>
      <td>3.0</td>
      <td>3.0</td>
    </tr>
    <tr>
      <th>8</th>
      <td>5</td>
      <td>L-H</td>
      <td>A-O</td>
      <td>NaN</td>
      <td>3.0</td>
      <td>3.0</td>
      <td>3.0</td>
      <td>3.0</td>
      <td>3.0</td>
      <td>3.5</td>
      <td>NaN</td>
      <td>3.0</td>
      <td>3.0</td>
    </tr>
    <tr>
      <th>9</th>
      <td>6</td>
      <td>L-H</td>
      <td>A-O</td>
      <td>NaN</td>
      <td>3.5</td>
      <td>3.0</td>
      <td>3.0</td>
      <td>3.0</td>
      <td>3.0</td>
      <td>3.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>3.0</td>
    </tr>
    <tr>
      <th>10</th>
      <td>6</td>
      <td>L-K</td>
      <td>A-O</td>
      <td>NaN</td>
      <td>3.0</td>
      <td>3.0</td>
      <td>3.0</td>
      <td>3.0</td>
      <td>3.0</td>
      <td>3.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>3.0</td>
    </tr>
    <tr>
      <th>11</th>
      <td>7</td>
      <td>L-K</td>
      <td>A-S</td>
      <td>NaN</td>
      <td>2.0</td>
      <td>1.5</td>
      <td>1.0</td>
      <td>1.5</td>
      <td>1.5</td>
      <td>2.0</td>
      <td>1.5</td>
      <td>1.5</td>
      <td>1.5</td>
    </tr>
    <tr>
      <th>12</th>
      <td>7</td>
      <td>L-H</td>
      <td>A-S</td>
      <td>NaN</td>
      <td>3.0</td>
      <td>3.0</td>
      <td>3.0</td>
      <td>3.5</td>
      <td>3.0</td>
      <td>3.0</td>
      <td>2.5</td>
      <td>3.0</td>
      <td>3.0</td>
    </tr>
    <tr>
      <th>13</th>
      <td>8</td>
      <td>L-K</td>
      <td>A-K</td>
      <td>NaN</td>
      <td>3.0</td>
      <td>3.0</td>
      <td>3.0</td>
      <td>3.0</td>
      <td>3.0</td>
      <td>3.5</td>
      <td>3.0</td>
      <td>3.0</td>
      <td>3.0</td>
    </tr>
    <tr>
      <th>14</th>
      <td>8</td>
      <td>L-Y</td>
      <td>A-K</td>
      <td>NaN</td>
      <td>3.0</td>
      <td>3.5</td>
      <td>3.0</td>
      <td>3.0</td>
      <td>3.5</td>
      <td>3.0</td>
      <td>3.0</td>
      <td>3.5</td>
      <td>3.0</td>
    </tr>
    <tr>
      <th>15</th>
      <td>9</td>
      <td>L-KR</td>
      <td>A-S</td>
      <td>NaN</td>
      <td>3.0</td>
      <td>2.0</td>
      <td>2.0</td>
      <td>3.0</td>
      <td>2.5</td>
      <td>2.5</td>
      <td>2.0</td>
      <td>2.0</td>
      <td>2.0</td>
    </tr>
    <tr>
      <th>16</th>
      <td>10</td>
      <td>L-KA</td>
      <td>A-O</td>
      <td>NaN</td>
      <td>3.0</td>
      <td>3.0</td>
      <td>3.0</td>
      <td>3.0</td>
      <td>3.0</td>
      <td>3.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>3.0</td>
    </tr>
    <tr>
      <th>17</th>
      <td>10</td>
      <td>L-W</td>
      <td>A-O</td>
      <td>NaN</td>
      <td>3.0</td>
      <td>2.5</td>
      <td>2.5</td>
      <td>2.5</td>
      <td>2.5</td>
      <td>2.5</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>2.5</td>
    </tr>
    <tr>
      <th>18</th>
      <td>11</td>
      <td>L-I</td>
      <td>A-S</td>
      <td>NaN</td>
      <td>3.0</td>
      <td>3.0</td>
      <td>3.0</td>
      <td>3.0</td>
      <td>3.0</td>
      <td>3.0</td>
      <td>2.5</td>
      <td>2.5</td>
      <td>3.5</td>
    </tr>
    <tr>
      <th>19</th>
      <td>11</td>
      <td>L-T</td>
      <td>A-S</td>
      <td>NaN</td>
      <td>3.0</td>
      <td>2.5</td>
      <td>2.5</td>
      <td>3.0</td>
      <td>2.0</td>
      <td>2.5</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>2.5</td>
    </tr>
  </tbody>
</table>
</div>




```python
'''
calculate correlation using pearsonr 
'''
import pandas as pd
from scipy.stats import pearsonr

correlation_table = pd.DataFrame([],columns=["item","correlation","pvalue"])

for name in ["B-2","B-3","B-4","B-5","B-6","B-9"]:
    corr_data = pd.DataFrame({"localized":localized_data[name],"generic":generic_data[name]})
    corr_data = corr_data.dropna(axis=0,how='any')
    correlation, pvalue = pearsonr(corr_data["localized"], corr_data["generic"])
    row = pd.DataFrame({"item":[name],"correlation":[correlation],"pvalue":[pvalue]})
    correlation_table=pd.concat([correlation_table,row])

correlation_table.to_csv(f"{out_dir}/pearsonr_correlation.csv",encoding="utf_8_sig",index=False)
correlation_table
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
      <th>item</th>
      <th>correlation</th>
      <th>pvalue</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>B-2</td>
      <td>0.703914</td>
      <td>0.000533</td>
    </tr>
    <tr>
      <th>0</th>
      <td>B-3</td>
      <td>0.69838</td>
      <td>0.000615</td>
    </tr>
    <tr>
      <th>0</th>
      <td>B-4</td>
      <td>0.507262</td>
      <td>0.022435</td>
    </tr>
    <tr>
      <th>0</th>
      <td>B-5</td>
      <td>0.082409</td>
      <td>0.729793</td>
    </tr>
    <tr>
      <th>0</th>
      <td>B-6</td>
      <td>0.043574</td>
      <td>0.85941</td>
    </tr>
    <tr>
      <th>0</th>
      <td>B-9</td>
      <td>0.611463</td>
      <td>0.004174</td>
    </tr>
  </tbody>
</table>
</div>




```python
'''
calculate correlation using spearmanr 
'''
import pandas as pd
from scipy.stats import spearmanr

correlation_table = pd.DataFrame([],columns=["item","correlation","pvalue"])

for name in ["B-2","B-3","B-4","B-5","B-6","B-9"]:
    corr_data = pd.DataFrame({"localized":localized_data[name],"generic":generic_data[name]})
    corr_data = corr_data.dropna(axis=0,how='any')
    correlation, pvalue = spearmanr(corr_data["localized"], corr_data["generic"])
    row = pd.DataFrame({"item":[name],"correlation":[correlation],"pvalue":[pvalue]})
    correlation_table=pd.concat([correlation_table,row])

correlation_table.to_csv(f"{out_dir}/spearmanr_correlation.csv",encoding="utf_8_sig",index=False)
correlation_table

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
      <th>item</th>
      <th>correlation</th>
      <th>pvalue</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>B-2</td>
      <td>0.641968</td>
      <td>0.002276</td>
    </tr>
    <tr>
      <th>0</th>
      <td>B-3</td>
      <td>0.589217</td>
      <td>0.006262</td>
    </tr>
    <tr>
      <th>0</th>
      <td>B-4</td>
      <td>0.543306</td>
      <td>0.013296</td>
    </tr>
    <tr>
      <th>0</th>
      <td>B-5</td>
      <td>0.170996</td>
      <td>0.471023</td>
    </tr>
    <tr>
      <th>0</th>
      <td>B-6</td>
      <td>0.074463</td>
      <td>0.761918</td>
    </tr>
    <tr>
      <th>0</th>
      <td>B-9</td>
      <td>0.536465</td>
      <td>0.014746</td>
    </tr>
  </tbody>
</table>
</div>




```python
'''
calculate cohen kappa in generic rubric
'''


from sklearn.metrics import cohen_kappa_score
generic_scores = generic_data.loc[~generic_data["double-assessment"].isna(),:]\
    .iloc[:,4:]\
    .dropna(how='any', axis=1)\
    .applymap(lambda x:int(x*10))
generic_kappa=cohen_kappa_score(generic_scores.iloc[0,:], generic_scores.iloc[1,:])

print(f"generic tools kappa: {generic_kappa}")

generic_scores


```

    generic tools kappa: -0.25





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
      <th>B-1</th>
      <th>B-2</th>
      <th>B-3</th>
      <th>B-4</th>
      <th>B-5</th>
      <th>B-8</th>
      <th>B-9</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>6</th>
      <td>30</td>
      <td>35</td>
      <td>25</td>
      <td>30</td>
      <td>30</td>
      <td>35</td>
      <td>35</td>
    </tr>
    <tr>
      <th>7</th>
      <td>30</td>
      <td>30</td>
      <td>30</td>
      <td>35</td>
      <td>30</td>
      <td>30</td>
      <td>30</td>
    </tr>
  </tbody>
</table>
</div>




```python
'''
calculate cohen kappa in generic rubric
'''
localized_scores = localized_data.loc[~generic_data["double-assessment"].isna(),:]\
    .iloc[:,4:]\
    .dropna(how='any', axis=1)\
    .select_dtypes(include=int)
localized_kappa=cohen_kappa_score(localized_scores.iloc[0,:], localized_scores.iloc[1,:])

kappa_table = pd.DataFrame([],columns=["assessment_tool","kappa"])
kappa_table = pd.concat([kappa_table,pd.DataFrame({"assessment_tool":["generic rubric"],"kappa":[generic_kappa]})])
kappa_table = pd.concat([kappa_table,pd.DataFrame({"assessment_tool":["localized tools"],"kappa":[localized_kappa]})])
kappa_table.to_csv(f"{out_dir}/cohen_kappa.csv",encoding="utf_8_sig",index=False)

print(localized_scores)
        


kappa_table

```

       L1  L3  L4  L5  L6  L7  L8  L11  B-5
    6   1   2   2   2   2   2   3    4    4
    7   1   2   1   2   3   2   3    4    4





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
      <th>assessment_tool</th>
      <th>kappa</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>generic rubric</td>
      <td>-0.25</td>
    </tr>
    <tr>
      <th>0</th>
      <td>localized tools</td>
      <td>0.689655</td>
    </tr>
  </tbody>
</table>
</div>


