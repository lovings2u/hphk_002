## 20181218

*로또*

```python
import random

# 1~45 까지의 숫자를 가진 numbers라는 배열을 만든다.
# 반복문 1~45까지해서 하나씩 배열에 넣는 방법도 있습니다.
# python make long array / make number array
# python make range to list
# 1.
numbers = []
for i in range(45):
  numbers.append(i+1)

# 2.
#lotto2 = list(range(1,46))
#print(lotto2)

# numbers에서 숫자 6개를 랜덤으로 뽑는다.(당연히 비복원 추출)
# 랜덤으로 뽑은 숫자들을 lotto 변수에 담고 출력한다.
lotto = random.sample(numbers, 6)
print("이번주 로또 추천 번호는 {} 입니다.".format(sorted(lotto)))



# 추가: lotto 변수에 담겨있는 숫자들을 오름차순으로 정렬하기
```



*네이버웹툰*

```python
import requests
import time
from bs4 import BeautifulSoup as bs

today = time.strftime("%a").lower()
#1. 네이버 웹툰을 가져올 수 있는 주소(url)를 파악하고 url 변수에 저장한다.
url = "https://comic.naver.com/webtoon/weekdayList.nhn?week=" + today
#2. 해당 주소로 요청을 보내 정보를 가져온다.
response = requests.get(url).text
#3. 받은 정보를 bs를 이용해 검색하기 좋게 만든다.
soup = bs(response, 'html.parser')
#4. 네이버 웹툰 페이지로 가서, 내가 원하는 정보가 어디에 있는지 파악한다.
toons = []
li = soup.select('.img_list li')
for item in li:
    toon = { 
      "title": item.select_one('dt a').text,
      "url":  item.select('dt a')[0]["href"],
      "img_url": item.select('.thumb img')[0]["src"]
    }
    toons.append(toon)

print(toons)
#오늘자 업데이트 된 웹툰들의 각각 리스트 페이지, 웹툰의 제목 + 해당 웹툰의 썸네일

#5. 3번에서 저장한 문서를 이용해 4번에서 파악한 위치를 뽑아내는 코드를 작성한다.

#6. 출력한다.
```



*다음 웹툰*

```python
import requests
import time
import json
from bs4 import BeautifulSoup as bs

#1. 내가 원하는 정보를 얻을 수 있는 주소를 url이라고 하는 변수에 담는다.
url = "http://webtoon.daum.net/data/pc/webtoon/list_serialized/thu"
#2. 해당 url에 요청을 보내 응답을 받아 저장한다.
response = requests.get(url).text
#3. 구글신에게 python으로 json을 어떻게 파싱(딕셔너리 형으로 변환)하는지 물어본다.
#4. 파싱한다.(변환한다)
document = json.loads(response)
#5. 내가 원하는 데이터를 꺼내서 조합한다.
data = document["data"]
toons = []
for toon in data:
    print(toon["title"])
    print(toon["pcThumbnailImage"]["url"])
    print("http://webtoon.daum.net/webtoon/view/{}".format(toon["nickname"]))
 
```

