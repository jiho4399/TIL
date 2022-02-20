[toc]

# HTML

- 방구조(뼈대) : HTML
- 인테리어 : CSS
- 가구배치 : Java Script

## 1. HTML 이란?

-   웹 : 세계의 컴퓨터를 연결하여 정보 공유
- 태그 : HTML 문서는 태그로 만들어진다.
  - 시작 태그 : <p>
  - 종료 태그 : </p> 

```
(1) 뿌리 <html>
	큰가지 (2) <head>
	
					 <head>
	큰가지 (3) <body>
	
					 <body>
(1)		 </html>
```

- 태그 – 속성 – 속성 값
  - 테이블 태그 
  - 타이틀 태그 : 웹사이트 제목
  - 앵커 태그 : 사이트 이동
  - 폼 태그 : 사용자의 정보를 서버로 전달하기 위한 태그
    - 인풋 태그
    - 데이터 전송 (GET : 페이지 받아오기, POST : 데이터 업로드하기)

| 특징          | GET                                                          | POST                    |
| ------------- | ------------------------------------------------------------ | ----------------------- |
| 기능          | 데이터를 조회                                                | 데이터를 전송           |
| 데이터 업로드 | url 주소 <br />? : 파라메타를 보내겠다<br />& : 그리고<br />'파라메타 = 파라메타 값' | <br />Body 안           |
| 용량 제한     | 제한적                                                       | 대용량 데이터 전송 가능 |
| 보안          | 취약                                                         | 상대적 안전             |

- http : 일반적
- https : 암호화

## 2. 웹 스크래핑이란?

- 웹 서버에 저장된 데이터를 가져오는 행위
- 에이전트와 파서가 필요하며 에이전트인 requests로 페이지를 다운 받는다.
- 파서가 들어가 있는 beautifulSoup으로 다운받은 페이지를 분석한다.

| 특징                | 스크래핑             | 크롤링                 |
| ------------------- | -------------------- | ---------------------- |
| 데이터 획득         | 필요한 데이터만 추출 | 페이지에서 데이터 참조 |
| 데이터 크기(스케일) | 필요한 만큼          | 대부분 크다            |
| 중복 제거           | 필요하다면           | 필수                   |
| 필요 모듈           | agent & parser       | agent                  |

- `F12` 를 누르면 개발자 툴을 보여줌
- 여기서 네모 + 화살표 누르면 뭐가 뭔지 알려줌
- xpath : 트리구조
  -  //*[@id="account"]/a : 네이버 로그인 버튼의 xpath
  - //*[@id="NM_FAVORITE"]/div[1]/ul[2]/li[1]/a : 사전의 xpath

### [1] VS Code에서 해보기

- HTML > test.html

1. html.5 선택

2.  ```html
    <!DOCTYPE html>
    <html lang="en">
        <head>
            <meta charset="UTF-8">
            <meta http-equiv="X-UA-Compatible" content="IE=edge">
            <meta name="viewport" content="width=device-width, initial-scale=1.0">
            <title>스크레핑을 위한 html</title> 
        </head>
        <body>
            <input type="text" value="아이디를 입력하세요.">
            <input type="password" name="" id="">
            <input type="button" value="로그인">
            <a href="http://google.com">구글로 이동</a>
        </body>
    </html>
    ```

3. 컴퓨터 폴더로 들어가서 크롬으로 열기

## 3. requests 모듈

- http 요청을 보내서 트리 구조로 이루어진 html의 정보를 가져오는 모듈
- id와 pw가 url에 노출되어 보안에 취약한 get 방식과 노출하지 않는 post 방식이 있다.
- http client 모듈 
- 정적 데이터에 한에서만 동작함

```python
!pip install requests
```

```python
import requests
```

### [1] 200 : 완전 정상인 상태를 나타내는 코드

```python
res = requests.get('http://www.naver.com')

# res.status_code
# 200

if res.status_code == requests.codes.ok: # 200
  print('정상')

else:
  print('에러:' + res.status_code)
  
# 정상
```

- 상태 확인

- 위에 코드 _ get으로 사이트 페이지를 가져오는것

- 정상적으로 처리 되었는지 확인 res.status_code

  

- 그래서 `res.raise_for_status()` 로 오류 예외처리

- 오류가 발생하면 익셉션 발생 시킴

- `res.text`  : 해당 주소의 html

```python
res = requests.get('http://google.com')

res.raise_for_status()

print(len(res.text))
# 14124
```

### [2] 'res.text : 해당 주소의 html' 를 파일로 저장

```python
with open('result.html', 'w', encoding='utf-8') as f:
  f.write(res.text)
```

### [3] pc인지 모바일인지 각자 맞는 웹사이트 서비스 제공

- user agent 정보 제공
- http://m.avalon.co.kr/check.html
- 콘솔 창에 `navigator.userAgent` 입력하면 headers 내용 나옴

```python
url = 'http://naver.com'
headers = {
           'User-Agent':'Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/96.0.4664.110 Safari/537.36'
}

res = requests.get(url, headers=headers) # 받아오기
res.raise_for_status() # 잘 받아왔는지 확인

with open('agent.html', 'w', encoding='utf-8') as f:
  f.write(res.text)
  
# 파일 다운 받아서 크롬으로 열면 네이버 나옴
```

## 4. BeautifulSoup4 모듈

- requests로 가져온 html 소스 내용에 접근하는 모듈
- html 구문 분석
- 에이전트 : 불러오기
- 파서 : 불러온 것 분석하기

```python
!pip install bs4
!pip install lxml
```

```python
import requests
from bs4 import BeautifulSoup
```

### [1] title 불러오기 `.title.get_text()` 

```python
url = 'https://comic.naver.com/webtoon/weekday'
res = requests.get(url) # 받아오기
res.raise_for_status() # 잘 받아왔는지 확인

soup = BeautifulSoup(res.text, 'lxml')

soup.title
# <title>네이버 만화 &gt; 요일별  웹툰 &gt; 전체웹툰</title>
```

- 태그 없이 title 불러오기

```python
soup.title.get_text()

# '네이버 만화 > 요일별  웹툰 > 전체웹툰'
```

### [2] 앵커 태그 찾기 `.a` 

- 맨 처음 앵커 태그 리턴해줌

```python
soup.a

soup.a.attrs # 딕셔너리 값이라는 것을 알 수 있음

# soup.a.attrs['href'] # '#menu'
```

### [3] 필요한 앵커 태그 불러오기 `soup.find('태그명', attrs={}` 

- 네이버 '웹툰 올리기' 앵커 태그 찾기

```python
soup.find('a', attrs={'class':'Nbtn_upload'})

# <a class="Nbtn_upload" href="/mypage/myActivity" onclick="nclk_v2(event,'olk.upload');">웹툰 올리기</a>
```

- 인기상승 웹툰 중 1위 태크 찾기

```python
soup.find('li', attrs={'class':'rank01'})
________________________________
## 앵커 태그 찾기
rank1 = soup.find('li', attrs={'class':'rank01'})

rank1.a.get_text() # 출력
# '외모지상주의-377화 일해회 (2계열사) [06]'
```

### [4] 가족 관계로 태그 찾기

- 동생 찾기

```python
# rank2 = rank1.next_sibling.next_sibling # 페이지 구성이 이렇게 되어 있음
rank2 = rank1.find_next_sibling('li')

rank2.a.get_text()
# '나 혼자 만렙 뉴비-28화. 고인물이 성장하는 법(3)'
________________________________________
# rank3 = rank2.next_sibling.next_sibling
rank3 = rank2.find_next_sibling('li')

rank3.a.get_text()
# '재혼 황후-99화'
```

- 형 찾기

```python
# rank2 = rank3.previous_sibling.previous_sibling
rank2 = rank3.find_previous_sibling('li')

rank2.a.get_text()
# '나 혼자 만렙 뉴비-28화. 고인물이 성장하는 법(3)'
```

- 부모 태그

```python
rank2.parent
```

- 형제 모두 찾기

```python
rank1.find_next_siblings('li')
```

### [5] 웹툰으로 실습하기

#### (1) 웹툰 명 출력하기

```python
url = 'https://comic.naver.com/webtoon/weekday'
res = requests.get(url) # 받아오기
res.raise_for_status() # 잘 받아왔는지 확인하기

soup = BeautifulSoup(res.text, 'lxml') # 넘겨주기, 파서는 lxml로 하겠다

cartoons = soup.find_all('a', attrs={'class':'title'})
# 모든걸 찾는데 제목의 테그가 a, 속성명은 class, 속성값은 title인 것 모두 찾음

for cartoon in cartoons:
  print(cartoon.get_text())

# 모든 웹툰 명이 출력됨
```

#### (2) 독립일기

```python
url = 'https://comic.naver.com/webtoon/list?titleId=748105&weekday=thu'
res = requests.get(url) # 받아오기
res.raise_for_status() # 잘 받아왔는지 확인하기
```

```python
soup = BeautifulSoup(res.text, 'lxml') # 넘겨주기, 파서는 lxml로 하겠다
```

```python
cartoons = soup.find_all('td', attrs={'class':'title'}) 
# 모든걸 찾는데 제목의 테그가 td, 속성명은 class, 속성값은 title인 것 모두 찾음

type(cartoons) # set이 있다 > 이터러블 객체, 반복(순환)이 가능하다

# bs4.element.ResultSet
```

- 제목 확인

```python
cartoons[0].a.get_text()
# '시즌2 44화 신년 맞이 스케일링'
```

- 주소 확인

```python
cartoons[0].a['href']
# '/webtoon/detail?titleId=748105&no=147&weekday=thu'
```

- for 문으로  제목 출력하기
- 링크가 앞부문이 생략된 채로 출력됨 그래서 " '[https://comic.naver.com'](https://comic.naver.com'/) + " 해주어야 함

```python
for cartoon in cartoons:
  title = cartoon.a.get_text()
  link = 'https://comic.naver.com' + cartoon.a['href']

  print(title, link)
  
# 시즌2 44화 신년 맞이 스케일링 https://comic.naver.com/webtoon/detail?titleId=748105&no=147&weekday=thu
# 시즌2 43화 부모님 가르쳐드리기 https://comic.naver.com/webtoon/detail?titleId=748105&no=146&weekday=thu
# 시즌2 42화 시간제 캠핑 https://comic.naver.com/webtoon/detail?titleId=748105&no=145&weekday=thu
# 시즌2 41화 우리 집 산타 https://comic.naver.com/webtoon/detail?titleId=748105&no=144&weekday=thu
# 시즌2 40화 깐부 https://comic.naver.com/webtoon/detail?titleId=748105&no=143&weekday=thu
# 시즌2 39화 세상의 모든 알람 https://comic.naver.com/webtoon/detail?titleId=748105&no=142&weekday=thu
# 시즌2 38화 만두 만들기 https://comic.naver.com/webtoon/detail?titleId=748105&no=141&weekday=thu
# 시즌2 37화 나의 20대 (2) https://comic.naver.com/webtoon/detail?titleId=748105&no=140&weekday=thu
# 시즌2 36화 나의 20대 (1) https://comic.naver.com/webtoon/detail?titleId=748105&no=139&weekday=thu
# 시즌2 35화 내스타일 https://comic.naver.com/webtoon/detail?titleId=748105&no=138&weekday=thu
```

- 평균 평점

```python
ratings = soup.find_all('div', attrs={'class':'rating_type'})

sum = 0
for rating in ratings:
  rate = rating.find('strong').get_text()
  sum += float(rate)

# 평균 = sum/ratings의 갯수
round(sum/len(ratings), 2)
```

## 5. Selenium + 

- 동작 페이지 client 모듈 
- 동적 데이터에 한에서만 동작함