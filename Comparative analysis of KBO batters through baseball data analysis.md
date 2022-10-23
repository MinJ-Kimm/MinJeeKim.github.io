# 야구 데이터 분석을 통한 KBO 타자 비교분석/ Comparative analysis of KBO batters through baseball data analysis


```python
import pandas as pd

```


```python
file = "/Users/margokim/Documents/Learning Spoons Data 2/파이썬 기초/PJT1)Baseball_Analysis/data/KBO_2019_player_gamestats.csv"

raw = pd.read_csv(file, encoding = 'cp949')

raw.info()
```

    <class 'pandas.core.frame.DataFrame'>
    RangeIndex: 15311 entries, 0 to 15310
    Data columns (total 34 columns):
     #   Column  Non-Null Count  Dtype  
    ---  ------  --------------  -----  
     0   팀       15311 non-null  object 
     1   이름      15311 non-null  object 
     2   생일      15311 non-null  object 
     3   일자      15311 non-null  object 
     4   상대      15311 non-null  object 
     5   결과      15311 non-null  object 
     6   타순      15311 non-null  int64  
     7   P       15311 non-null  object 
     8   선발      15311 non-null  int64  
     9   타수      15311 non-null  int64  
     10  득점      15311 non-null  int64  
     11  안타      15311 non-null  int64  
     12  2타      15311 non-null  int64  
     13  3타      15311 non-null  int64  
     14  홈런      15311 non-null  int64  
     15  루타      15311 non-null  int64  
     16  타점      15311 non-null  int64  
     17  도루      15311 non-null  int64  
     18  도실      15311 non-null  int64  
     19  볼넷      15311 non-null  int64  
     20  사구      15311 non-null  int64  
     21  고4      15311 non-null  int64  
     22  삼진      15311 non-null  int64  
     23  병살      15311 non-null  int64  
     24  희타      15311 non-null  int64  
     25  희비      15311 non-null  int64  
     26  타율      15311 non-null  float64
     27  출루      15311 non-null  float64
     28  장타      15311 non-null  float64
     29  OPS     15311 non-null  float64
     30  투구      15311 non-null  int64  
     31  avLI    15311 non-null  float64
     32  RE24    15311 non-null  float64
     33  WPA     15311 non-null  float64
    dtypes: float64(7), int64(20), object(7)
    memory usage: 4.0+ MB



```python
# 데이터 분석에 활용할 컬럼만 선택

raw.columns

columns_select = ['팀', '이름', '생일','일자', '상대', '타수', 
                  '안타','홈런', '루타', '타점', '볼넷', '사구', '희비' ]

data = raw[columns_select]

data
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
      <th>팀</th>
      <th>이름</th>
      <th>생일</th>
      <th>일자</th>
      <th>상대</th>
      <th>타수</th>
      <th>안타</th>
      <th>홈런</th>
      <th>루타</th>
      <th>타점</th>
      <th>볼넷</th>
      <th>사구</th>
      <th>희비</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>두산</td>
      <td>페르난데스</td>
      <td>1988-04-27</td>
      <td>03-23</td>
      <td>한화</td>
      <td>4</td>
      <td>2</td>
      <td>0</td>
      <td>3</td>
      <td>3</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>두산</td>
      <td>페르난데스</td>
      <td>1988-04-27</td>
      <td>03-24</td>
      <td>한화</td>
      <td>2</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>두산</td>
      <td>페르난데스</td>
      <td>1988-04-27</td>
      <td>03-26</td>
      <td>키움</td>
      <td>2</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>2</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>두산</td>
      <td>페르난데스</td>
      <td>1988-04-27</td>
      <td>03-27</td>
      <td>키움</td>
      <td>4</td>
      <td>3</td>
      <td>0</td>
      <td>3</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>두산</td>
      <td>페르난데스</td>
      <td>1988-04-27</td>
      <td>03-28</td>
      <td>키움</td>
      <td>3</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>2</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>15306</th>
      <td>SK</td>
      <td>정현</td>
      <td>1994-06-01</td>
      <td>09-19</td>
      <td>두산</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>15307</th>
      <td>SK</td>
      <td>정현</td>
      <td>1994-06-01</td>
      <td>09-20</td>
      <td>키움</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>15308</th>
      <td>SK</td>
      <td>정현</td>
      <td>1994-06-01</td>
      <td>09-28</td>
      <td>@삼성</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>15309</th>
      <td>SK</td>
      <td>정현</td>
      <td>1994-06-01</td>
      <td>09-30</td>
      <td>@한화</td>
      <td>2</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>15310</th>
      <td>SK</td>
      <td>정현</td>
      <td>1994-06-01</td>
      <td>10-17</td>
      <td>@키움</td>
      <td>2</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
    </tr>
  </tbody>
</table>
<p>15311 rows × 13 columns</p>
</div>



# Q1 : Best KBO player?


```python
data_player = data.pivot_table (index = ['팀', '이름', '생일'],
                 values = ['타수', 
                  '안타','홈런', '루타', '타점', '볼넷', '사구', '희비'], 
                  aggfunc = 'sum')

data_player
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
      <th></th>
      <th></th>
      <th>루타</th>
      <th>볼넷</th>
      <th>사구</th>
      <th>안타</th>
      <th>타수</th>
      <th>타점</th>
      <th>홈런</th>
      <th>희비</th>
    </tr>
    <tr>
      <th>팀</th>
      <th>이름</th>
      <th>생일</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th rowspan="5" valign="top">KIA</th>
      <th>고영창</th>
      <th>1989-02-24</th>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>김선빈</th>
      <th>1989-12-18</th>
      <td>146</td>
      <td>43</td>
      <td>1</td>
      <td>115</td>
      <td>394</td>
      <td>40</td>
      <td>3</td>
      <td>4</td>
    </tr>
    <tr>
      <th>김세현</th>
      <th>1987-08-07</th>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>김주찬</th>
      <th>1981-03-25</th>
      <td>126</td>
      <td>17</td>
      <td>5</td>
      <td>101</td>
      <td>337</td>
      <td>32</td>
      <td>3</td>
      <td>3</td>
    </tr>
    <tr>
      <th>나지완</th>
      <th>1985-05-19</th>
      <td>47</td>
      <td>19</td>
      <td>3</td>
      <td>24</td>
      <td>129</td>
      <td>17</td>
      <td>6</td>
      <td>2</td>
    </tr>
    <tr>
      <th>...</th>
      <th>...</th>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th rowspan="5" valign="top">한화</th>
      <th>최윤석</th>
      <th>1987-03-28</th>
      <td>3</td>
      <td>3</td>
      <td>0</td>
      <td>3</td>
      <td>12</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>최재훈</th>
      <th>1989-08-27</th>
      <td>135</td>
      <td>56</td>
      <td>14</td>
      <td>108</td>
      <td>373</td>
      <td>31</td>
      <td>3</td>
      <td>4</td>
    </tr>
    <tr>
      <th>최진행</th>
      <th>1985-08-17</th>
      <td>51</td>
      <td>9</td>
      <td>2</td>
      <td>27</td>
      <td>117</td>
      <td>19</td>
      <td>6</td>
      <td>1</td>
    </tr>
    <tr>
      <th>하주석</th>
      <th>1994-02-25</th>
      <td>7</td>
      <td>0</td>
      <td>0</td>
      <td>5</td>
      <td>19</td>
      <td>2</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>호잉</th>
      <th>1989-05-18</th>
      <td>219</td>
      <td>38</td>
      <td>5</td>
      <td>135</td>
      <td>476</td>
      <td>73</td>
      <td>18</td>
      <td>5</td>
    </tr>
  </tbody>
</table>
<p>285 rows × 8 columns</p>
</div>




```python
#타수가 적은 경우, 타율 등 데이터에 영향을 주기때문에 타수 데이터 분포도 파악을 먼저 
#타수 데이터 분포도를 통해 타수가 적은 선수는 제외 후 진행
#If the number of at-bats is small, it is important to understand the distribution of the at-bats data first because it affects data such as batting average.
#Proceed after excluding players with a small number of at-bats through the at-bat data distribution
```


```python
data_player ['타수'].hist()
```




    <AxesSubplot:>




    
![png](output_7_1.png)
    



```python
#타수가 적다의 기준을 50으로 잡고 진행

cond = data_player ['타수'] > 50 

data_player = data_player[cond].reset_index()

```


```python
#타율/출루율/장타율/OPS 를 계산하는 함수
#타율 : 타격에 성공해서 진루하는 비율 (안타/타수)
#출루율 : 살아서 진루하는 비율 (안타+볼넷+몸에맞는 볼)/(타수+볼넷+몸에맞는볼+희생플레이)
#장타율 : 타율에 진루한 베이스 가중치 추가 (루타 / 타수)
#OPS : 출루율 + 장타율

#Function to calculate batting average/on-base percentage/slugging percentage/OPS
#batting average: percentage of advances by successful hitting (hit/number of strokes)
#On-Base Rate: Ratio of living and advancing to base (hit + walk + body-fitting ball)/(at-bat + walk + body-fitting ball + sacrifice play)
#Slugging percentage: Add base weight to the batting average (Routes / batting average)
#OPS: On-base percentage + slugging percentage

def cal_hit(df):
    
    df['타율'] = df['안타'] / df['타수']
    df['출루율'] = (df['안타'] + df['볼넷'] + df['사구'])/(df['타수'] + df['볼넷'] + df['사구']+df['희비'])
    df['장타율'] = df['루타'] / df['타수']
    df['OPS'] = df['출루율'] + df['장타율']
    
    return df


player_stat = cal_hit(data_player)

player_stat.head()
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
      <th>팀</th>
      <th>이름</th>
      <th>생일</th>
      <th>루타</th>
      <th>볼넷</th>
      <th>사구</th>
      <th>안타</th>
      <th>타수</th>
      <th>타점</th>
      <th>홈런</th>
      <th>희비</th>
      <th>타율</th>
      <th>출루율</th>
      <th>장타율</th>
      <th>OPS</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>KIA</td>
      <td>김선빈</td>
      <td>1989-12-18</td>
      <td>146</td>
      <td>43</td>
      <td>1</td>
      <td>115</td>
      <td>394</td>
      <td>40</td>
      <td>3</td>
      <td>4</td>
      <td>0.291878</td>
      <td>0.359729</td>
      <td>0.370558</td>
      <td>0.730287</td>
    </tr>
    <tr>
      <th>1</th>
      <td>KIA</td>
      <td>김주찬</td>
      <td>1981-03-25</td>
      <td>126</td>
      <td>17</td>
      <td>5</td>
      <td>101</td>
      <td>337</td>
      <td>32</td>
      <td>3</td>
      <td>3</td>
      <td>0.299703</td>
      <td>0.339779</td>
      <td>0.373887</td>
      <td>0.713666</td>
    </tr>
    <tr>
      <th>2</th>
      <td>KIA</td>
      <td>나지완</td>
      <td>1985-05-19</td>
      <td>47</td>
      <td>19</td>
      <td>3</td>
      <td>24</td>
      <td>129</td>
      <td>17</td>
      <td>6</td>
      <td>2</td>
      <td>0.186047</td>
      <td>0.300654</td>
      <td>0.364341</td>
      <td>0.664995</td>
    </tr>
    <tr>
      <th>3</th>
      <td>KIA</td>
      <td>류승현</td>
      <td>1997-07-01</td>
      <td>48</td>
      <td>9</td>
      <td>4</td>
      <td>38</td>
      <td>150</td>
      <td>14</td>
      <td>0</td>
      <td>0</td>
      <td>0.253333</td>
      <td>0.312883</td>
      <td>0.320000</td>
      <td>0.632883</td>
    </tr>
    <tr>
      <th>4</th>
      <td>KIA</td>
      <td>박찬호</td>
      <td>1995-06-05</td>
      <td>160</td>
      <td>26</td>
      <td>4</td>
      <td>131</td>
      <td>504</td>
      <td>49</td>
      <td>2</td>
      <td>2</td>
      <td>0.259921</td>
      <td>0.300373</td>
      <td>0.317460</td>
      <td>0.617833</td>
    </tr>
  </tbody>
</table>
</div>




```python
player_stat = player_stat.sort_values(by = ['출루율', '장타율','OPS','타율'], ascending = False)
player_stat = player_stat.reset_index(drop = True)
player_stat
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
      <th>팀</th>
      <th>이름</th>
      <th>생일</th>
      <th>루타</th>
      <th>볼넷</th>
      <th>사구</th>
      <th>안타</th>
      <th>타수</th>
      <th>타점</th>
      <th>홈런</th>
      <th>희비</th>
      <th>타율</th>
      <th>출루율</th>
      <th>장타율</th>
      <th>OPS</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>NC</td>
      <td>나성범</td>
      <td>1989-10-03</td>
      <td>60</td>
      <td>12</td>
      <td>1</td>
      <td>34</td>
      <td>93</td>
      <td>14</td>
      <td>4</td>
      <td>0</td>
      <td>0.365591</td>
      <td>0.443396</td>
      <td>0.645161</td>
      <td>1.088558</td>
    </tr>
    <tr>
      <th>1</th>
      <td>NC</td>
      <td>양의지</td>
      <td>1987-06-05</td>
      <td>225</td>
      <td>48</td>
      <td>15</td>
      <td>139</td>
      <td>394</td>
      <td>68</td>
      <td>20</td>
      <td>6</td>
      <td>0.352792</td>
      <td>0.436285</td>
      <td>0.571066</td>
      <td>1.007351</td>
    </tr>
    <tr>
      <th>2</th>
      <td>KT</td>
      <td>강백호</td>
      <td>1999-07-29</td>
      <td>217</td>
      <td>61</td>
      <td>2</td>
      <td>147</td>
      <td>438</td>
      <td>65</td>
      <td>13</td>
      <td>4</td>
      <td>0.335616</td>
      <td>0.415842</td>
      <td>0.495434</td>
      <td>0.911275</td>
    </tr>
    <tr>
      <th>3</th>
      <td>KIA</td>
      <td>최형우</td>
      <td>1983-12-16</td>
      <td>221</td>
      <td>85</td>
      <td>7</td>
      <td>137</td>
      <td>456</td>
      <td>86</td>
      <td>17</td>
      <td>7</td>
      <td>0.300439</td>
      <td>0.412613</td>
      <td>0.484649</td>
      <td>0.897262</td>
    </tr>
    <tr>
      <th>4</th>
      <td>두산</td>
      <td>페르난데스</td>
      <td>1988-04-27</td>
      <td>277</td>
      <td>63</td>
      <td>6</td>
      <td>197</td>
      <td>581</td>
      <td>90</td>
      <td>15</td>
      <td>6</td>
      <td>0.339071</td>
      <td>0.405488</td>
      <td>0.476764</td>
      <td>0.882252</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>132</th>
      <td>롯데</td>
      <td>강로한</td>
      <td>1992-05-13</td>
      <td>108</td>
      <td>13</td>
      <td>3</td>
      <td>69</td>
      <td>288</td>
      <td>25</td>
      <td>4</td>
      <td>1</td>
      <td>0.239583</td>
      <td>0.278689</td>
      <td>0.375000</td>
      <td>0.653689</td>
    </tr>
    <tr>
      <th>133</th>
      <td>삼성</td>
      <td>송준석</td>
      <td>1994-05-04</td>
      <td>18</td>
      <td>2</td>
      <td>1</td>
      <td>12</td>
      <td>51</td>
      <td>4</td>
      <td>1</td>
      <td>1</td>
      <td>0.235294</td>
      <td>0.272727</td>
      <td>0.352941</td>
      <td>0.625668</td>
    </tr>
    <tr>
      <th>134</th>
      <td>롯데</td>
      <td>김문호</td>
      <td>1987-06-22</td>
      <td>32</td>
      <td>4</td>
      <td>0</td>
      <td>25</td>
      <td>103</td>
      <td>4</td>
      <td>0</td>
      <td>1</td>
      <td>0.242718</td>
      <td>0.268519</td>
      <td>0.310680</td>
      <td>0.579198</td>
    </tr>
    <tr>
      <th>135</th>
      <td>삼성</td>
      <td>김도환</td>
      <td>2000-04-14</td>
      <td>31</td>
      <td>8</td>
      <td>0</td>
      <td>19</td>
      <td>93</td>
      <td>7</td>
      <td>2</td>
      <td>1</td>
      <td>0.204301</td>
      <td>0.264706</td>
      <td>0.333333</td>
      <td>0.598039</td>
    </tr>
    <tr>
      <th>136</th>
      <td>KT</td>
      <td>문상철</td>
      <td>1991-04-06</td>
      <td>19</td>
      <td>4</td>
      <td>2</td>
      <td>12</td>
      <td>60</td>
      <td>7</td>
      <td>2</td>
      <td>2</td>
      <td>0.200000</td>
      <td>0.264706</td>
      <td>0.316667</td>
      <td>0.581373</td>
    </tr>
  </tbody>
</table>
<p>137 rows × 15 columns</p>
</div>




```python
#팀별 선수 출루율 분포
# #Distribution of player on-base percentage by team 

import seaborn as sns

# 아래 코드는 seaborn, matplotlib으로 시각화를 진행할때 데이터에 한글이 들어있다면 copy&paste 한 뒤 사용하시면 됩니다. 
# 이미지 상에 들어있는 한글을 표시하기 위한 한글 폰트를 지정하고, 필요한 라이브러리를 불러들이는 코드입니다. 
import matplotlib
from matplotlib import font_manager, rc
import platform
import matplotlib.pyplot as plt
import seaborn as sns

# 이미지 한글 표시 설정
if platform.system() == 'Windows':  # 윈도우인 경우 맑은고딕
    font_name = font_manager.FontProperties(fname="c:/Windows/Fonts/malgun.ttf").get_name()
    rc('font', family=font_name)
else:    # Mac 인 경우 애플고딕
    rc('font', family='AppleGothic')

#그래프에서 마이너스 기호가 표시되도록 하는 설정입니다.
matplotlib.rcParams['axes.unicode_minus'] = False 
```


```python
sns.boxplot(data = player_stat, x ="팀" , y="출루율",
           showcaps = False, whiskerprops = {'linewidth' : 0}
           ,showfliers = False, boxprops = {'facecolor' : 'None'})
sns.swarmplot(data = player_stat, x ="팀" , y="출루율")
```




    <AxesSubplot:xlabel='팀', ylabel='출루율'>




    
![png](output_12_1.png)
    



```python
file = "/Users/margokim/Documents/Learning Spoons Data 2/파이썬 기초/PJT1)Baseball_Analysis/data/player_stat2.csv"
player_stat.to_csv(file, encoding = 'cp949', index = False)
```


```python

```
