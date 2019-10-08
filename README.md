# 막내야 식당 찾아라

## 소개

## 시스템
> <p>Client : https://github.com/bsshmk/maknaeya_sikdang_chajara_client</p>
> <p>Server : https://github.com/bsshmk/maknaeya_sikdang_chajara_api</p>
> <p>Crawling : https://github.com/bsshmk/maknaeya_sikdang_chajara_crawling</p>

### 참여자
> 조명기(ChoMk), 김보성(bsgreentea), 조성훈(JoChoSunghoon)

# 막내야 식당 찾아라 Crawling

## 개발환경
> Anaconda4.4.10, Jupyter Notebook5.7.8, MySQL8.0.17, Chrome 77.0.3865.90

## 사용 라이브러리
> re, requests, urlopen, BeautifulSoup, webdriver, WebDriverWait, expected_conditions, By, pymysql, pandas

## 개발언어
> Python3.7.3

## Crawling 사이트
> https://www.siksinhot.com/


## Crawling Architecture
<p>크게 2번의 과정으로 진행.</p>
<p>chromedriver를 사용해 크롤링할 음식점의 url을 수집하고 저장한다.</p>
<p>수집한 음식점 url를 통해 html 코드를 받아오고 파싱해서 태그 단위로 접근한다.</p>
<p>MySQL과 연동하여 크롤링한 데이터를 관리한다.</p>
<p>Python에서 MySQL의 데이터를 받아올 때 변환하기 쉽게 dataframe으로 받는다.</p>
<p>DB에 저장되는 table은 2개로 1개는 음식점의 전반적인 정보를 관리하고 1개는 음식점의 리뷰들을 관리한다.</p>


## Database Schema
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/d34b7238-0df8-465c-864d-78daaa774b08/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=ASIAT73L2G45P5Q6UD7K%2F20191008%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20191008T043353Z&X-Amz-Expires=86400&X-Amz-Security-Token=AgoJb3JpZ2luX2VjEJz%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJHMEUCICBD%2BJtbsKwLyqGn3He0exOAqwr5E1ijlTRgqPgEMQCvAiEAwQNFJ6dxc2Bu3zedkqibr3FhbRwqC5gLtDnjjPglUmMq4wMIhf%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FARAAGgwyNzQ1NjcxNDkzNzAiDJE65aslNyD4ctCYNyq3A2tFnalw9o%2BBWZJrIKsmHIjuQQltWolHgJCimkZvcu2CFgBGX4l8%2BYQkS%2F2isaxLdfxFoBzpWiynPqT4EUYNSuu0rHQoCkfPCOgrcpZk9Dm0aUy03K0TUHU3rNGRb92MBOcSOPaeSpZ6SbqBfuRzSvyeewU%2FmC3uJzByqU8FHW3sWvjPx3QOT7mg8vGqkLgOVhMjrj%2B57wmfRRprEgUQ%2Bj7PtBRPYZyLTAMZH5MvcLRunC3hKej%2BIl6n9fMjRkvW7%2FfRQHEn2pE3ELODkeACapyiWBP3yNED%2F1uEKhsoFWyDKVuEFyPEAKr%2FKpSKIFf94ZNgUFxWq%2BPo9nTqL69KBZ14%2F%2FRuTYlLgB4O6xeEpBLRLkcrc%2BwSHQ%2B5eMXzedb96HYdqn5q%2FX8iPf3%2Bwqrz0cReTOkctpJ7p6ZSgAZjv5GMy7EeMXb8Iydt%2FVPYuRzC5oeKiLewpoG5u3rvdT4bMEEmnvLtUp%2FeRS%2FcnwIs2flJdjexFFp5lMLKxa%2BemUHfc%2Fdr26y9F6KaMTqwaO96OobOpEHEUbWMWTyD79lDqrmQ7ZfR%2FSfzlbtwv9J4pgzCM3ERnHs2V%2BMwq4jw7AU6tAGB4zKzY7XAVcER7DYS1kFGajCzMxwVLSQi2sU8u7sIVKqVeFAVfiRDpeIqYh3JVIWmj9d662WIj6FrPpNeKthNpCRDSKg6XkOnREywpP8c9UBJ7OJUcHpbMFhICz%2B0zUJ2TULj3NtPnvCmqFEVxbprK70fQd8byUiyfNg5R5FortR36guHmGjDLTBNFYtuKOSdfdruel8VDgOHh5rsuKztVhPqTwoHaGlIP17%2FQ2Yc3WuC%2BpU%3D&X-Amz-Signature=306fe8cecb6bb56e6841575e9dc412211f93d2379b894be2d71595c51d9a46bb&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22" alt="alt text" width="650px" height="500px">

> https://dbdiagram.io/d/5d50df65ced98361d6dd7fc8

<p>DB에서는 배열을 사용할 수 없으므로 제 1정규화과정을 이용한다.</p>
<p>App에서 음식점의 리뷰는 따로 recyclerview로 관리해서 따로 table을 만들어서 관리해준다.</p>





### 고민
<p>크롤링할 사이트를 저장할 때 더보기 버튼을 a href="#" 과 같이 구현하여 한번에 원하는 정보를 다 펼쳐 볼 수 없었다.</p>

> webdriver를 사용했고 그 중에서 버튼을 눌러주는 기능으로 자동으로 원하는 정보를 다 펼쳤다.

<p>음식점 사이트마다 비슷한 레이아웃을 하고 있지만 세부적인 태그와 각 세부항목의 표현 방식이 다 달라서 일괄적으로 크롤링할 수 없었다.</p>

> 태그중에서 div이름을 통해 찾고 싶었으나 다 child(i)로 관리하여서 직접 비교해야만 했다. 그리고 원하는 정보가 없으면 ""으로 대체하여 저장하였다.

<p>음식점 판매시간 정보의 경우 형식이 너무 달라서 예외처리가 너무 많이 생긴다</p>

<p>각 음식점 사이트에서 마저 리뷰를 더 펼칠 때 a href="#"를 사용했다</p>

> 이때 다시 webdriver를 띄우고 더보기 버튼을 실행하여 리뷰를 다 띄우고 그 다음에 저장하는 코드를 삽입했으나 따로따로 한줄 씩 실행시에는 정상 작동을 했다. 하지만 한번에 실행시에 오류가 생겼다.

<p>html과 js코드에서 태그와 id, 함수와 변수명이 너무 직관적이지 못하고 의미를 갖고 있지 않았다</p>
  
  
  

### 개선점
<p>DB에서 restaurant의 main_menu와 main_menu_price도 제1정규화 과정을 거친다면 따로 테이블로 분리를 해야한다.</p>
<p>크롤링하는 코드가 예외처리로 인해 깔끔하지 못한 점을 해결한다</p>
<p>DB 스키마를 더 효율적으로 작성하여 유저가 늘어났을 때 유지 보수가 쉽게 해야한다</p>
<p>일정 주기로 DB를 업데이트 한다</p>

