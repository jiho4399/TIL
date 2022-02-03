[toc]

# 01/10. 튜플 (tuple)

## [리스트]

- `lst = []` : 리스트 생성
- `lst = list()` : 리스트로 타입 바꾸기

## [튜플]

- `tup = ()` : 튜플 생성
- `tup =  tuple()` : 튜플로 타입 바꾸기
- 튜플은 수정(추가, 삭제)할 수 없음
- 일정 값으로 인식하여 뒤에서 배울 딕셔너리의 key 자리에 들어갈 수 있음

### [1] 튜플 생성하기

```python
t1 = ()
t2 = (1, )
t3 = (1, 2, 3)
t4 = 1, 2, 3
t5 = ('a', 'b', ('ab', 'cd'))
```

### [2] 튜플은 수정이 불가능하다

```python
## 튜플은 지우는 것을 지원하지 않는다
t1 = (1, 2, 'a', 'b')
del t1[0]

# ERROR 발생

## 튜플은 수정이 불가능함
t1[0] = 100
t1

# ERROR 발생
```

### [3] 튜플은 인덱싱이 가능하다

```python
t1 = (1, 2, 'a', 'b')
t1[0]

# 1
```

### [4] 튜플의 슬라이싱

```python
t1 = (1, 2, 'a', 'b')
t1[:2]

# (1, 2)
```

### [5] 튜플의 연산

```python
## 튜플과 튜플 더하기
t1 = (1, 2, 'a', 'b')
t2 = ('c', 'd')

t1 + t2

# (1, 2, 'a', 'b', 'c', 'd')

## 튜플 반복
t1 * 3

#(1, 2, 'a', 'b', 1, 2, 'a', 'b', 1, 2, 'a', 'b')

## 튜플 안 갯수 확인
len(t1)

# 4

## 튜플 특정 문자 갯수 확인
t3 = [1, 2, 1, 2, 1, 2]
t3.count(2)

# 3
```

## [튜플 실습]

### [1] 빈 튜플 만들기

```python
empty_tuple = ()
print(empty_tuple)
print(type(empty_tuple))

# ()
# <class 'tuple'>
```

### [2] 거래 상위 top3 튜플 만들기

```python
stock_top3 = ('SG세계물산', 'KODEX', '휴센텍')
print(stock_top3)
print(type(stock_top3))

# ('SG세계물산', 'KODEX', '휴센텍')
# <class 'tuple'>
```

### [3] 숫자 1만 있는 튜플 만들기 (문자도 똑같음) `,` 

- **`콤마`** : ( )에 의미 부여. 튜플로 만들겠다는 의미 

```python
num_tuple = (1,) 
print(num_tuple)
print(type(num_tuple))

# (1,)
# <class 'tuple'>
```

### [4] 튜플 더 알아가기

1. 튜플 안에 값을 바꿀 수 없음!
2. ( ) 안에 넣지 않아도 자동으로 튜플로 생성
3. 튜플은 수정할 수 없으니 대/소문자로도 바꿀 수 없음

```python
## 1.
t1 = (1, 2, 3)
t1[0] = 'hihihi' 

# ERROR 발생

## 2.
t2 = 1, 2, 3, 4
print(t2)
print(type(t2))

# (1, 2, 3, 4)
# <class 'tuple'>

## 3.
t3 = ('a', 'b', 'c')
print(t3.upper())

# ERROR 발생
```

### [5] 튜플을 리스트로 바꿔보기 `list()` 

```python
electronics = ('삼성전자', 'LG전자')

electronics = list(electronics)
print(type(electronics))
print(electronics)

# <class 'list'>
# ['삼성전자', 'LG전자']
```

### [6] 튜플 값을 각 변수에 지정하기 (`packing` 과 `unpacking` )

```python
##packing
call = ('apple', 'samsung', '샤오미', '화웨이', '레노버')

##unpacking
a, s, x, h, l = (call)

print(a)		# apple
print(s)		# samsung
print(l)		# 레노버
```