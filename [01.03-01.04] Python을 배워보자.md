[toc]





# 01/03. Python을 배워보자

## **1. 파이썬이란?**

### [1] Anaconda

- 터미널에 anaconda 입력 (아나콘다 실행)
- 가상환경 만들기 : `conda create -n basic python = 3.8`
- 가상환경 활성화 : `conda activate basic`
- 가상환경 비활성화 : `conda deactivate`
- 가상환경 리스트 확인 : `conda env list`
- 가상환경 없애기 : `conda env remove -n basic`



### [2] 구글 코랩 개발환경

- #### 숫자 연산자 

  `+` : 더하기 , `- ` : 빼기 , `*` : 곱하기 , `/` : 나누기 , `%`  : 나머지 , `//` : 몫 , `**` : 제곱

- #### 문자열 : `type()` : str

  - 여러 줄에 걸쳐 문장 작성 시 `''' '''` or `""" """` 사용

  - ##### 이스케이프 코드 `\` 

     문자를 그대로 사용

    - ```python
      h = 'It\'s mine.'
      ```

  - ##### 이스케이프 코드 `\n` 

    줄 바꿈

    - ```python
      multiline = 'Life is too short\nYou need python'
      print(multiline)
      ```

  - ##### 문자열 연산자 : `+` : 더하기 ,  `*` : 반복

  - `len()` : 공백 포함 문자열 길이 구하기

    

  - ##### 문자열 인덱싱 (0부터 시작)

  - ##### 문자열 슬라이싱

    - ```python
      a = 'Life is too short'
      a[0:4] #'Life'
      a[:] #'Life is too short'
      ```

    - ##### 문자 고치기

    - ```python
      a = 'pithon'
      a = a[:1] + 'y' + a[2:] #'python'
      ```

  - ##### 문자열 포매팅 (문자열 형식 결정)

    - ```python
      number = 3
      day = 'three'
      'I ate %d apples. So I was sick for %s days.' % (number, day)
      
      #'I ate 3 apples. So I was sick for three days.'
      ```

    - ```python
      ##포매팅 연산자 %d와 %를 같이 쓸 때는 %%를 쓴다.
      'Error is %d%%' % 98
      
      #Error is 98%
      ```

    

    - ```python
      ##10개 자리수에 hi 입력(앞에 공백 8, 뒤에 문자 2)
      '%10s' % 'hi'
      
      #'        hi'
      ```

    - ```python
      ##공백이 뒤에
      '%-10s' % 'hi'
      
      #'hi        '
      ```

    - ```python
      '%10s jane.' % 'hi'
      
      #'        hi jane.'
      ```

    - ```python
      ##f는 실수 .4 는 소숫점 자릿수를 의미(반올림)
      '%0.4f' % 3.42134234
      
      #'3.4213'
      
      '%10.4f' % 3.141592
      
      #'    3.1416'
      
      '%-10.4f' % 3.141592
      
      #'3.1416    '
      ```

# 01/04. Python 함수

### [1] .format () 함수

#### (1) 숫자, 문자 대입하기

- ```python
  ##숫자 바로 대입하기
  'I eat{0} apples.'.format(3)
  
  #I eat3 apples.
  ```

- ```python
  ## 문자열 바로 대입하기
  'I eat {0} apples'.format('five')
  
  #I eat five apples
  ```

- ```python
  ## 2개 이상의 값 넣기
  number = 10
  day = 'three'
  'I ate {0} apples. so I was sick for {1} days.'.format(number, day)
  
  #I ate 10 apples. so I was sick for three days.
  ```

#### (2) 정렬

- ```python
  ## 왼쪽 정렬
  "{0:<10}".format('hi')
  
  #'hi        '
  
  ## 왼쪽 정렬 & 빈칸을 .로 채우기
  "{0:.<10}".format('hi')
  
  #'hi........'
  ```

- 소숫점 표현하기

  - ```python
    ##소숫점 표현하기
    y = 3.42134234
    '{0:0.4f}'.format(y)
    
    #'3.4213'
    
    '{0:10.4f}'.format(y)
    
    #'    3.4213'
    ```

- `{문자}` 그대로 표현하기

  - ```python
    '{{and}}'.format()
    
    #'{and}'
    ```

  - ```python
    '{0}, {1}, {2}'.format('a', 'b', 'c')
    
    #'a, b, c'
    
    '{2}, {1}, {0}'.format(*'abc')
    
    #'c, b, a'
    
    '{0}{1}{0}'.format(*'abc')
    
    #'aba'
    
    '{0}{1}{0}'.format('abra', 'cad')
    
    #'abracadabra'
    
    
    ```

  - 



### [2] f 문자열 포매팅

#### (1) f 문자열 포매팅

- ```python
  name = '홍길동'
  age = 30
  f'나의 이름은 {name}입니다. 나이는 {age}입니다.'
  
  #'나의 이름은 홍길동입니다. 나이는 30입니다.'
  ```

- 표현식

  ```python
  age = 30
  f'나는 내년이면 {age+1}살이 된다.'
  
  #'나는 내년이면 31살이 된다.'
  ```

- 딕셔너리

  ```python
  d = {'name' : '홍길동', 'age' : 30}
  f'나의 이름은 {d["name"]}입니다. 나이는 {d["age"]}입니다.'
  
  #'나의 이름은 홍길동입니다. 나이는 30입니다.'

- 정렬

  ```python
  f'{"hi":-<10}' #왼쪽 정렬, 공백 채우기
  
  # 'hi--------'
  
  f'{"hi":>10}' #오른쪽 정렬
  
  #'        hi'
  
  f'{"hi":^10}' #가운데 정렬
  
  #'    hi    '
  ```

  

### [3] 문자열 함수

#### (1) 문자열 함수

- `count()` 함수 : 해당 알파벳 개수 세기

  ```python
  a = 'Hello World'
  a.count('l')
  
  #3
  ```

- `find()` 함수 : 알파벳 위치 찾기

  - 인덱스 값을 반환해준다.
  - 해당 알파벳이 없으면 `-1` 값을 반환한다.

  ```python
  a = 'Python is the best choice'
  a.find('b')
  
  #14
  ```

- `index()` 함수 : 알파벳 위치 찾기
  - 인덱스 값을 반환해준다.
  - 해당 알파벳이 없으면 오류가 발생한다.

```python
a = 'Life is too short'
a.index('t')

#8
```

- `join()` 함수 : 문자열 사이에 특정 문자 삽입하기

  ```python
  '.'.join('abcd')
  
  #'a.b.c.d'
  
  '.'.join(['a', 'b', 'c', 'd'])
  
  #'a.b.c.d'
  ```

- `upper()` 함수 : 대문자로 변경, `lower()` 함수 : 소문자로 변경

  ```python
  a = 'Welcome'
  a.upper()
  
  #'WELCOME'
  
  a.lower()
  
  #'welcome'
  ```

- `srtip()` 함수 : 공백 지우기

  ```python
  #왼쪽 공백 지우기
  a = '   hi   '
  a.lstrip()
  
  #오른쪽 공백 지우기
  a.rstrip()
  
  #양쪽 공백 지우기
  a.strip()
  ```

- `replace()` 함수 : 문자열 다시 만들기

  - a는 바뀌지 않음

  ```python
  a = 'Life is too short'
  b = a.replace('Life', 'Your leg')
  b
  
  #'Your leg is too short'
  ```

- `split()` 함수 : 문자열 나누기

  ```python
  a.split()
  
  #['Life', 'is', 'too', 'short']
  ```



### [4] 리스트

- 대괄호를 사용하여 생성한다.

- 인덱스가 있으며 리스트에는 숫자, 문자, 리스트가 들어갈 수 있다.

- 상대적으로 조금 느리다.

  ```python
  a = [1, 2, ['I', 'love', 'you']]
  a[-1]
  
  #['I', 'love', 'you']
  ```

#### (1) 리스트의 차원

```python
##2차원
a[-1][1]

#'love'

##3차원
a = [1, 2, ['a', 'b', ['Life', 'is', 'good']]]
a[2][2][0]

#'Life'

##4차원
a = [1, 2, ['a', 'b', ['Life', 'is', 'good', [1, 2, 3]]]]
a[2][2][3][0]

#1
```

