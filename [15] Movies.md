[toc]

# Movies

## 1. 기본 설정

```python
import numpy as np
import pandas as pd
```

## 2. 영화 목록 엑셀 파일 불러오기

```python
path = 'movies.xls'
movies = pd.read_excel(path)
movies.head()
```

## 3. 형태 알아보기

```python
movies.count()
# 영화명        45549
# 영화명(영문)    34635
# 제작연도       45549
# 제작국가       45247
# 유형         45537
# 장르         44124
# 제작상태       45340
# 감독         31704
# 제작사         6358
# dtype: int64

movies.shape
# (45549, 9)
```

## 4. 제작연도 순으로 정렬 `sort_values()` 

```python
movies.sort_values('제작연도').head()
```

## 5. 감독판 불러오기`str.contatins()` 

```python
con = movies['영화명'].str.contains('감독판')
movies[con].head()

movies[con].count()['영화명'] # 감독판 영화 갯수
# 153
```

## 6. 감독판 영화를 제작연도로 정렬

```python
movies[con].sort_values('제작연도') # 내림차순
movies[con].sort_values('제작연도', ascending=False) # 오름차순
```

## 7. 2015~2020년 영화 출력 `&` 

```python
con = (movies['제작연도'] >= 2015) & (movies['제작연도'] <= 2020)
movies[con]
```

