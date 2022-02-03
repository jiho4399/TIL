[toc]

# 01/10. 리스트

## 1. 리스트

- 리스트는 인덱스 존재, 값 위치 가능

[1] 리스트 생성하기

- `a = []`

- `a = list()`

  ```python
  strlist = ['I love you']
  strlist
  
  strlist = list('I love you')
  strlist
  ```

[2] 리스트 값 더하기

```python
data = [1, 2, 3, 4, 5]
data[0] + data[2]

#4
```

[3] 리스트끼리 더하기

```python
a = [1, 2, 3]
b = [4, 5, 6]

a+b

#[1, 2, 3, 4, 5, 6]
```

[4] 리스트 반복

```python
a * 3

# [1, 2, 3, 1, 2, 3, 1, 2, 3]
```

[5] 문자열과 숫자열 합치기

```python
str(a[2]) + 'hihi'

# '3hihihi'
```

- **함수에 대한 정보가 알고 싶다면?**  `help(함수명)` 

### [6] 리스트 값 바꾸기

```python
a = [1, 2, 3]
a[-1] = 5
a

# [1, 2, 5]
```

### [7] 리스트 안에 값 지우기: `del` 

```python
a = [1, 2, 5]
del a[1]
a

# [1, 5]

a = [1, 2, 3, 4, 5]
del a[2:]
a

# [1, 2]
```

### [8] 리스트에 값 추가하기 `.append()`  

```python
#리스트 끝에 값 추가하기
a = [1, 2, 3]
a.append(4)
a

#[1, 2, 3, 4]
```

### [9] 리스트 안 숫자 정렬하기 `.sort()` 

```python
#숫자 정렬하기
a = [1, 2, 4, 3, 5]
a.sort()
a

# [1, 2, 3, 4, 5]

#문자 정렬하기
b = ['a', 'd', 'b']
b.sort()
b

#['a', 'b', 'd']
```

### [10] 리스트 뒤집기 `.reverse()` 

```python
b = ['a', 'b', 'd']
b.reverse()
b

# ['d', 'b', 'a']
```

### [11] 리스트에서 해당 문자 인덱스 값 찾기 `.index()` 

```python
b.index('a')

# 2
```

### [12] 리스트에 값 추가하기`.insert()`  

```python
a = [0, 1, 2, 3]
a.insert(3, 2)
# insert(인덱스 위치, 넣을 값)
a

# [0, 1, 2, 2, 3]
```

### [13] 리스트에서 특정 값 지우기 `.remove()` & `.pop()` & `del` 

```python
## remove() ##
a = [0, 1, 2, 2, 3]
a.remove(3)
a

# [0, 1, 2, 2]

#3을 다 지우고 싶을 때 흐름
a = [1, 2, 3, 1, 2, 3]

while True:
  try:
    a.remove(3)
    print(a)
  except Exception as e:
    print(e)
    break

a

# [1, 2, 1, 2, 3]
# [1, 2, 1, 2]
# list.remove(x): x not in list
# [1, 2, 1, 2]

## pop() ##

a = [1, 2, 3]
a.pop(0)
a

#[2, 3]

## del ##
a = [1, 2, 3]
del a[0]
a

#[2, 3]
```

- **`.remove()` 와 `.pop()` 의 차이점**

  - remove는 완전 삭제하며 괄호 안에 값이 들어가지만

  - pop은 빼와서 다시 사용할 수 있으며 괄호 안에 인덱스가 들어감

    ```python
    ## pop
    a = [1, 2, 3]
    
    val = a.pop(0)
    
    val, a
    
    #(1, [2, 3])
    ```

### [14] 확장 `.extend()`

```python
a = [1, 2, 3]
b = [4, 5, 6]

a.extend(b) # a = a + b
a

#[1, 2, 3, 4, 5, 6]
```

### [15] 최댓값과 최솟값 `max()` & `min()` 

``` python
nums = [1, 2, 3, 4, 5, 6]

print(f'최댓값 : {max(nums)}')
print(f'최솟값 : {min(nums)}')

# 최댓값 : 6
# 최솟값 : 1
```

### [16] 총 합 구하기 `sum()` 

```python
print(f'총 합 : {sum(nums)}')

# 총 합 : 21
```

### [17] 평균 구하기 (직접 계산 or `numpy` )

```python
#평균 구하기
print(f'평균 : {sum(nums)/len(nums)}')

# 평균 : 3.5

#import numpy as np
#array = np.array(nums)
#print(f'평균값 : {np.mean(array)}')
```

### [18] 슬라이싱하여 홀수/짝수 구하기

```python
## 홀수 ##
nums = [1, 2, 3, 4, 5, 6]
nums[::2]
#[start:stop:step]

# [1, 3, 5]

## 짝수 ##
nums = [1, 2, 3, 4, 5, 6]
nums[1::2]

# [2, 4, 6]
```

### [19] 역방향으로 뒤집기 `.reverse()` 

```python
nums = [1, 2, 3, 4, 5, 6]

nums.reverse() #nums 자체를 바꿈
nums  

# [6, 5, 4, 3, 2, 1]

#nums[::-1] #nums는 바뀌지 않음
```

