[toc]

# Pandas

- 시계열 분석
  - 시간의 흐름에 따라 흘러가는 것
- 넘파이 기반으로 되어있다

```python
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
```

## 1. Series

- 1차원 데이터
- 출력 : 인덱스 , 값

```python
s = pd.Series([3, 5, 7, 9])
s
# 0    3
# 1    5
# 2    7
# 3    9
```

### [1] 인덱스를 설정할 수 있다 `index` 

- 설정 할거면 의미 있는 인덱스로 하라
- 아니면 그냥 쓰지 말 것 (자동으로 주니까)

```python
s2 = pd.Series([3, 5, 7, 9], index=['a', 'b', 'c', 'd'])
s2

# a    3
# b    5
# c    7
# d    9

s.index
# RangeIndex(start=0, stop=4, step=1)

s.values
# array([3, 5, 7, 9])
```

### [2] 인덱싱

- 지정한 인덱스 값이 아니더라도 숫자로 접근 가능
- 하지만 이왕이면 지정한 인덱스로 접근하는 것이 좋음

```python
s2['a']
# 3
s2[0]
# 3
```

### [3] 딕셔너리로 시리즈 만들기

- 딕셔너리로 시리즈를 만들면 `key가 인덱스`가 되고` value가 값`이 됨

```python
pop_dict = {
    '서울':9543, 
    '도쿄':37340, 
    '토론토':6255, 
    '뉴욕':18823, 
    '파리':11079,
    '베를린':3567,
    '런던':9426
}

population = pd.Series(pop_dict)
population
# 서울      9543
# 도쿄     37340
# 토론토     6255
# 뉴욕     18823
# 파리     11079
# 베를린     3567
# 런던      9426
________________________________________
pop_dict['서울']
# 9543

population['서울']
# 9543
```

- 숫자로 접근하는 것은 시리즈에만 적용 가능
- 딕셔너리에 적용하면 에러 발생

```python
# pop_dict[0]
# 하면 에러 발생

population[0]
# 9543
```

- 시리즈 - 값에 일정 값 곱하기

```python
population * 1000

# 서울      9543000
# 도쿄     37340000
# 토론토     6255000
# 뉴욕     18823000
# 파리     11079000
# 베를린     3567000
# 런던      9426000
```

## 2. DataFrame

- 2차원 (행과 열)
- `시리즈 2개`를 모아 하나의 데이터 프레임을 만듦

### [1] 리스트 안에 리스트

```python
data = [
        ['대한민국', '서울', 9543], 
    ['일본', '도쿄', 37340], 
    ['캐나다', '토론토', 6255], 
    ['미국', '뉴욕', 18823], 
    ['프랑스', '파리', 11079],
    ['독일', '베를린', 3567],
    ['영국', '런던', 9426],
        ]

df = pd.DataFrame(data)
df
# 열 값 설정 
df = pd.DataFrame(data, columns=['Country', 'City', 'Population'])
df
```

### [2] 딕셔너리

- 딕셔너리의 keys가 columns로 들어감

```python
data = {
        'Country':['대한민국', '일본', '캐나다', '미국', '프랑스', '독일', '영국'], 
        'City':['서울', '도쿄', '토론토', '뉴욕', '파리', '베를린', '런던'], 
        'Population':[9543, 37340, 6255, 18823, 11079, 3567, 9426]
}

df = pd.DataFrame(data)
df
```

- 인덱스 수정하기

```python
df2 = pd.DataFrame(data, index=['aa', 'bb', 'cc', 'dd', 'ee', 'ff', 'gg'])
df2
```

- 형태 확인하기

```python
df2.columns
# Index(['Country', 'City', 'Population'], dtype='object')

df2.dtypes
# Country       object
# City          object
# Population     int64
```

### [3] 인덱스 지정하기

```python
df_index_with_country = df.set_index('Country')
df_index_with_country

df_index_with_country_and_city = df.set_index(['Country', 'City'])
df_index_with_country_and_city
```

### [4] 인덱싱

```python
df['Country']
# 0    대한민국
# 1      일본
# 2     캐나다
# 3      미국
# 4     프랑스
# 5      독일
# 6      영국

df.iloc[0, 0]
# '대한민국'

df.loc[0, 'Country']
# '대한민국'

df[0:2]
# 0    대한민국
# 1      일본

df_index_with_country_and_city.loc[('대한민국', '서울')]
# Population    9543
# Name: (대한민국, 서울), dtype: int64
```

### [5] 예시

#### (1) 데이터 프레임 만들기

- 딕셔너리
- 시리즈

```python
# 딕셔너리
data = {
    'col1':[1, 2, 3, 4], 
    'col2':[5, 6, 7, 8], 
    'col3':[9, 10, 11, 12]
}

df3 = pd.DataFrame(data, index=['A', 'B', 'C', 'D'])
df3
___________________________________
# 시리즈
s1 = pd.Series([1, 2, 3, 4], index=['A', 'B', 'C', 'D'])
s2 = pd.Series([5, 6, 7, 8], index=['A', 'B', 'C', 'D'])
s3 = pd.Series([9, 10, 11, 12], index=['A', 'B', 'C', 'D'])

data = {'col1':s1,
        'col2':s2,
        'col3':s3
        }
df4 = pd.DataFrame(data, index=['A', 'B', 'C', 'D'])
df4
```

#### (2) 시리즈의 성질

```python
s = pd.Series([3, 5, 7, 9])
s
# 0    3
# 1    5
# 2    7
# 3    9

s + 10
# 0    13
# 1    15
# 2    17
# 3    19
```

#### (3) 데이터 프레임의 성질

```python
df
df['Population'] * 1000
# 0     9543000
# 1    37340000
# 2     6255000
# 3    18823000
# 4    11079000
# 5     3567000
# 6     9426000
```

```python
df['Country'] + df['City']

# 0    대한민국서울
# 1      일본도쿄
# 2    캐나다토론토
# 3      미국뉴욕
# 4     프랑스파리
# 5     독일베를린
# 6      영국런던
```

#### (4) 시리즈 연산하기

- 인덱스가 달라서 a와 c는 연산이 불가능 (처리는 됨)
- b는 둘 다 값이 있기 때문에 연산 가능

```python
s = pd.Series([3, 4, 5, 9], index=['a', 'b', 'c', 'd'])
s
# a    3
# b    4
# c    5
# d    9

s1 = s[['a', 'b']]
s2 = s[['b', 'c']]

s1 + s2

# a    NaN
# b    8.0
# c    NaN
```

## 3. 퀴즈

```python
df_index_with_country
```

### [1] 대한민국 서울이 다른 나라의 몇 배가 되는지 출력

```python
df_index_with_country['Population']['대한민국']/df_index_with_country['Population']
```

## 4. Json

```python
df
```

- export

```python
json_data = df.to_json()
json_data
```

- import

```python
pd.read_json(json_data)
```

### [1] csv 파일

- iris csv파일 가져오기

```python
!wget -O 'iris_sample.csv' https://raw.githubusercontent.com/duc-ke/edu_jupyter_pandas/master/dataset/iris_sample.csv
```

- 파일 내에 저장되어 있기 때문에 바로 불러들일 수 있음

```python
df_iris = pd.read_csv("iris_sample.csv")
df_iris
```

- iris tsv파일 가져오기

```python
!wget -O 'iris_sample.tsv' https://gist.githubusercontent.com/mbostock/3305937/raw/a5be7c5fd55c4fa0ca8a400cb68d658a40989966/data.tsv
```

- tsv 파일 공백(탭)으로 띄어 읽기

```python
pd.read_csv('iris_sample.tsv', sep='\t')
```

### [2] 다른 이름으로 저장`(.to_csv)`하고 불러오기`(.read_csv)`

- 그러면 인덱스가 하나 더 생기는데 이것을 방지하려면 옵션을 넣어준다.

```python
df_iris2.to_csv('iris_sample2.csv', index=False)

pd.read_csv('iris_sample2.csv')
```

### [3] 엑셀파일 

```python
# 엑셀을 오퍼레이션 하는 라이브러리
!pip install xlsxwriter
```

#### (1) 엑셀 파일 만들고 읽기

- sheet_name= 으로 옵션 가능

- 읽기
- 인덱스가 하나 더 붙음
- 지우고 싶으면 저장할 떄 옵션 설정하기!

```python
df_iris.to_excel('iris_sample2.xlsx', index=False)
pd.read_excel('iris_sample2.xlsx')

# df_iris.to_excel('iris_sample2.xlsx', sheet_name="iris1")
```

## 5. 데이터 베이스 접속 클라이언트 설정

```python
!pip install mysql-connector-python
```

```python
import sqlalchemy

user = 'anonymous'
host = 'ensembldb.ensembl.org' # 101동
port = '3337'
database = 'ailuropoda_melanoleuca_core_79_1'
url = f'mysql+mysqlconnector://{user}@{host}:{port}/{database}'
# url = f'mysql+mysqlconnector://{user}:{password}@{host}:{prot}/{database}'
# https://www.naver.com

connection = sqlalchemy.create_engine(url)
```

- sql 문 : 데이터를 요청하는 문

```python
pd.read_sql('select * from analysis limit 10', connection)
```

## 6. 퀴즈

```python
data ={
    'country': ['Belgium', 'France', 'Germany', 'Netherland', 'United Kingdom'], 
    'population': [11.4, 65.2, 83.7, 17.3, 67.8], 
    'area': [30510, 671308, 357050, 41526, 244820], 
    'capital': ['Brussels', 'Paris', 'Berlin', 'Amsterdam', 'London'],
}

countries = pd.DataFrame(data)
countries = countries.set_index('country')

countries
```

### [1] 인구밀도 density 컬럼 추가

```python
countries['density'] = countries['population'] * 1000000 / countries['area']

countries
```

### [2] 인구밀도가 300이상이 되는 나라의 수도, 인구를 보이기

```python
# 조건식
i = countries['density'] >= 300

# countries[i]

countries.loc[i, ['capital', 'population']]
```

- loc 쓰지 말고 출력

```python
i = countries['density'] >= 300

countries[['capital', 'population']][i]
# countries[i][['capital', 'population']]
```

### [3] density_ratio 컬럼 추가

- density_ratio : 인구 밀도/평균 인구 밀도

```python
# mean = sum(countries['density'])/len(countries['density'])
# countries["density_ratio"] = countries['density'] / mean
# countries

countries["density_ratio"] = countries['density'] / countries['density'].mean()
countries
```

### [4] 영국의 수도 런던을 맨체스터로 바꾸기

- 데이터 프레임에서 데이터 접근은 `컬럼`으로 한다

1. 인덱싱
2. loc

- `countries['capital']` 타입이 `시리즈`여서 `키 값`으로 접근!

```python
# 1.
countries['capital']['United Kingdom'] = 'Manchester'
countries
```

- loc --> [행, 열] (다시 원상복구)

```python
# 2.
countries.loc['United Kingdom', 'capital'] = 'London'
countries
```

### [5] 인구밀도 100이상, 300미만인 나라 구하기

```python
i = countries['density'] < 300 
j = countries['density'] >= 100

countries[i][j]

# countries[(countries['density'] < 300) & (countries['density'] >= 100)]
```

### [6] 수도의 글자가 7자 이상인 나라

```python
# 조건
con = countries['capital'].str.len() >= 7
countries[con]

# countries.loc[con, :]
```

### [7] 수도에 'Lo'가 포함된 나라 찾기

```python
# 조건
con = countries['capital'].str.contains('Lo')
countries[con]

# countries.loc[con, :]
```

### [8] 행/열 삭제`drop()` 

- 행 단위로/열 단위로 삭제
- 특정 데이터를 지울 수 없음
- 지우려면 None으로 바꾸어여 함

```python
df
# 행 지우기
df.drop(1)
df.drop([1, 2, 3])

# 열 지우기
df.drop('City', axis=1)
df.drop(['Country','City'], axis=1)
```

## 7. 판다스에서 제공하는 함수

### [1] 통계적 자료 확인 `describe`

```python
df.describe()
```

### [2] 원하는 갯수만큼 자료 보기 `head()` 

```python
df.head(2)
```

### [3] 정렬

```python
df.sort_values('Population')
df.sort_values('Population', ascending=False)
```

### [4] 값이 없는 것 찾기 isnull

```python
df.isnull()

# 행따라 열 출력 # 하나라도 값이 없다면 출력 any
df.isnull().any()

# 열따라 행 출력
df.isnull().any(axis=1)
```

- 하나라도 비어있는 값이 있으면 True 출력됨

```python
df.isnull().any().any()
```

- 값 하나를 None으로 바꾸고 해보기

```python
df2 = df.copy()
df2.loc[0, 'Population'] = None
df2

df2.isnull().any()

df2.isnull().any(axis=1)

df2.isnull().any().any()
```

### [5] 통계자료

#### (1) 개수

```python
df.count()
# Country       7
# City          7
# Population    7

df.count(axis=1)
# 0    3
# 1    3
# 2    3
# 3    3
# 4    3
# 5    3
# 6    3
```

#### (2) 합

```python
df.sum()
# Country       대한민국일본캐나다미국프랑스독일영국
# City            서울도쿄토론토뉴욕파리베를린런던
# Population                 96033
```

#### (3) 최댓값, 최솟값

```python
df.min()
# Country       대한민국
# City            뉴욕
# Population    3567

df.max()
# Country         프랑스
# City             파리
# Population    37340
```

#### (4) 평균, 중간값

```python
df.mean()
# Population    13719.0

df.median()
# Population    9543.0
```

### [6] apply 함수

```python
df
df.loc[:, 'Population':'Population'] * 1000

df.loc[:, 'Population':'Population'].apply(lambda x : x * 1000)

def mul(x):
  return x * 1000
df.loc[:, 'Population':'Population'].apply(mul)
```

### [7] groupby

- split : key 값에 따라서 나누기
- apply : 함수를 적용
- combine : 합치기

#### (1) score

```python
df2 = pd.DataFrame({
    '과목':['국', '영', '수', '국', '영', '수', '국', '영', '수'], 
    '점수':[100, 90, 80, 95, 85, 75, 70, 60, 50]
})

df2

math = df2['과목'] == '수'
math

df2.groupby('과목').mean()
# 과목별로 평균 출력
```

#### (2) titianic

```python
df = pd.read_csv('https://raw.githubusercontent.com/datasciencedojo/datasets/master/titanic.csv')

df.head()


```

- 성별 평균

```python
# 전체 평균
df.groupby('Sex').mean()

# 나이 평균
df.groupby('Sex')['Age'].mean()
```

- 전체 승객의 평균 생존율 구하기

```python
df['Survived'].mean()
```

- 25세 이하 승객의 생존율

```python
con = df['Age'] <= 25
df[con]['Survived'].mean()
```

- 남성의 생존율

```python
df[df['Sex'] == 'male']['Survived'].mean()
```

- 여성 생존율

```python
df[df['Sex'] == 'female']['Survived'].mean()
```

