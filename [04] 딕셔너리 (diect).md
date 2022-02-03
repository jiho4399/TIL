[toc]

# 01/11. 딕셔너리 (diect)

## [딕셔너리]

- 형식 : {`key:value`, `key:value` ...... }
- 변수 명으로 예약어는 쓰지 않기

### [1] 딕셔너리 생성하기

```python
dic = {'name' : '지호', 'age':24, 'phone' :'010-1234-1234', 'birth' : '990101'} 
#강사님 픽!

dic2 = {1 : '지호', 2 : 24} #key가 숫자

dic3 = {'a' : [1, 2, 3]} #value가 리스트
```

### [2] 딕셔너리에 추가하기

```python
dic4 = {1:'a'}
dic4[2] = 'b'
dic4

# {1: 'a', 2: 'b'}

dic4['name'] = '홍길동'
dic4

# {1: 'a', 2: 'b', 'name': '홍길동'}
```

### [3] 딕셔너리 안에 값 삭제하기

- [] 안에 `key값` 이 들어감 (인덱스 X)

```python
del dic4[2]
dic4

# {1: 'a', 'name': '홍길동'}
```

### [4] key가 겹치면 ? 

- 마지막 value 값으로 출력됨

```python
a = {1:'a', 1:'b'}
a

# {1: 'b'}
```

### [5] key 값은 유일한 값이 되어야 한다.

- `리스트`는 수정이 가능하므로 key값이 될 수 없다.
- `튜플` 은 수정이 불가능 하므로 key값이 될 수 있다.

```python
a = {[2, 3]:'hi'}
a

# ERROR 발생 
```

### [6] 딕셔너리의 key 값들 반환하기 `.keys()` 

```python
dic = {'name' : '지호', 'age':24, 'phone' :'010-1234-1234', 'birth' : '990101'}
print(dic.keys())
print(type(dic.keys()))

# dict_keys(['name', 'age', 'phone', 'birth'])
# <class 'dict_keys'>
```

- `for 문` 으로 key 값들 출력학

  ```python
  for d in dic.keys():
    print(d)
   
  # name
  # age
  # phone
  # birth
  ```

- `list` 로 key 값들 출력하기

  ```python
  list(dic.keys())
  
  # ['name', 'age', 'phone', 'birth']
  ```

### [7] 딕셔너리의 value 값 출력하기 `.values()`  

```python
print(dic.values())
print(type(dic.values()))

# dict_values(['지호', 24, '010-1234-1234', '990101'])
# <class 'dict_values'>
```

### [8] key와 value값 한번에 얻기 `.items()` 

```python
print(dic.items())
print(type(dic.items()))

# dict_items([('name', '지호'), ('age', 24), ('phone', '010-1234-1234'), ('birth', '990101')])
# <class 'dict_items'>
```

### [9] 딕셔너리 내용 모두 지우기 `.clear()` 

```python
dic.clear()
dic

# {}
```

### [10] 딕셔너리에서 원하는 값 출력하기 

- key가 인덱스 역할!!

```python
dic = {'name' : '지호', 'age':24, 'phone' :'010-1234-1234', 'birth' : '990101'}
dic['name']

# '지호'
```

### [11] 딕셔너리 안에 key가 있는지 확인 `in` 

```python
'name' in dic

# True
```

### [실습]

1. 빈 딕셔너리 만들기

   ```python
   tmp = {}
   print(tmp)
   print(type(tmp))
   
   # {}
   # <class 'dict'>
   ```

2. 스타벅스 커피 가격

   ```python
   price = {'돌체라떼':5500, '화이트초콜릿모카':5600, '카페모카':5100}
   print(price)
   print(type(price))
   
   # {'돌체라떼': 5500, '화이트초콜릿모카': 5600, '카페모카': 5100}
   # <class 'dict'>
   ```

3. 딕셔너리에 값 추가하기

   ```python
   price['카페라떼'] = 4600
   price['아메리카노'] = 4100
   
   print(price)
   print(type(price))
   
   # {'돌체라떼': 5500, '화이트초콜릿모카': 5600, '카페모카': 5100, '카페라떼': 4600, '아메리카노': 4100}
   # <class 'dict'>
   ```

4. 아메리카노 가격 출력하기

   ```python
   print(price['아메리카노'])
   
   # 4100
   
   ## 아메를 10% 할인된 가격으로 수정하기
   price['아메리카노'] = int(price['아메리카노']*0.9) 
   	#int : 소숫점 버림
   print(price['아메리카노'])
   
   # 3690
   ```

5. 메뉴에서 돌체라떼 빼기

   ```python
   del price['돌체라떼']
   price
   
   # {'아메리카노': 3690, '카페라떼': 4600, '카페모카': 5100, '화이트초콜릿모카': 5600}
   ```

6. 코드 구조화 하기 (사이즈 별 가격 추가)

   - 방법 1 : 딕셔너리 안에 딕셔너리

   ```python
   price2 = {'돌체라떼': {'톨': 5600, '그란데':6100, '벤티':6600}, 
            '라떼':{'톨': 4600, '그란데':5100, '벤티':5600}, 
            '아메리카노': {'톨': 4100, '그란데':4600, '벤티':5100}}
   
   price2['돌체라떼']['그란데']
   
   # 6100
   ```

   - 방법 2 : 딕셔너리 안에 리스트 (더 빠름)

   ```python
   price3 = {'돌체라떼': [5600, 6100, 6600], 
            '라떼':[4600, 5100, 5600], 
            '아메리카노': [4100, 4600, 5100]}
         
   price3['돌체라떼'][1]
   
   # 6100
   ```

7. 메뉴 추가하기

   ```python
   ## 1.
   price2['카페모카'] = {'톨':5100, '그란데':5600, '벤티':6100}
   price2['화이트초콜릿모카'] = {'톨':5600, '그란데':6100, '벤티':6600}
   
   ## 2.
   price3['카페모카'] = [5100, 5600, 6100]
   price3['화이트초콜릿모카'] = [5600, 6100, 6600]
   
   print(price2['카페모카']['벤티']) #dict
   print(price3['카페모카'][2]) #list
   
   # 6100
   # 6100
   ```

8. 메뉴 명만 리스트로 얻어오기

   ```python
   print(list(price2.keys()))
   print(type(list(price2.keys())))
   
   print(list(price3.keys()))
   print(type(list(price3.keys())))
   
   # ['돌체라떼', '라떼', '아메리카노', '카페모카', '화이트초콜릿모카']
   # <class 'list'>
   
   # ['돌체라떼', '라떼', '아메리카노', '카페모카', '화이트초콜릿모카']
   # <class 'list'>
   ```

9. 가격을 리스트로 가져오기

   ```python
   print(list(price2.values())) #dict
   print(list(price3.values())) #list
   
   # [{'톨': 5600, '그란데': 6100, '벤티': 6600}, {'톨': 4600, '그란데': 5100, '벤티': 5600}, {'톨': 4100, '그란데': 4600, '벤티': 5100}, {'톨': 5100, '그란데': 5600, '벤티': 6100}, {'톨': 5600, '그란데': 6100, '벤티': 6600}]
   
   # [[5600, 6100, 6600], [4600, 5100, 5600], [4100, 4600, 5100], [5100, 5600, 6100], [5600, 6100, 6600]]
   ```

   