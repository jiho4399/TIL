[toc]

# 01/18. VSCode에서 함수 공부

## 1. syslib

- 프로그램을 실행할 때 옵션 주기

```python
import sys

try : 
    if sys.argv[1] == 'call' :
        print(sys.argv[1])
    elif sys.argv[1] == 'exit' :
        sys.exit()
    elif sys.argv[1] == 'path' :
        print(sys.path)
    elif sys.argv[1] == 'append_path' :
        sys.path.append(sys.argv[2])
        print(sys.path)
    else :
        print('Not support')
except Exception as e :
    print('write more data!')

print('finish!!')
```

## 2. pickle _ `dump( )` & `load( )` 

1. 객체를 파일로 저장

```python
import pickle

with open('pickle_test.txt', 'wb') as f : ## wb : write & use data
    data = {1 : 'python', 2 : 'java'}
    pickle.dump(data, f)
```

2. 객체를 불러오기

```python
# import pickle

with open('pickle_test.txt', 'rb') as f :
    data = pickle.load(f)
    print(data)
  
# {1: 'python', 2: 'java'}
```

## 3. OS 함수

```python
import os 

print(os.environ)

# 경로 이동
print(os.getcwd())
os.chdir(os.getcwd()+'/lib')
print(os.getcwd())

# 파일 목록 보기
print(os.system('ls')) 
#0이 출력됨 : 0이 결과값이고 목록은 ls 명령에 의해 출력됨

# 실행하기
f = os.popen('ls')
print(f.read())
#결과값 자체가 목록

# 파일 생성 & 삭제
os.mkdir('lib2')
os.rmdir('lib2')

# 파일 이름 변경
os.mkdir('lib2')
os.rename('lib2', 'lib3')
```

## 4. 파일 복사하기 `shutil` 

- 파일을 복사해주는 파이썬 모듈
- 동일한 파일 이름이 있을 경우에는 덮어쓴다.
- src 파일을 dstFh 복사하기

```python
import shutil
shutil.copy('src.txt', 'dst.txt')
```

## 5. 디렉토리에 있는 파일 이름 모두 알기 `glob(pathname)`

- 디렉토리에 있는 파일들을 리스트로 만들기

```python
import glob
glob.glob('파일경로/mark*') 
# 파일 이름이 mark로 시작하는 파일을 모두 찾아서 읽어들이기
```

