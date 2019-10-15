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
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/d34b7238-0df8-465c-864d-78daaa774b08/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=ASIAT73L2G45AE22KKW2%2F20191015%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20191015T040338Z&X-Amz-Expires=86400&X-Amz-Security-Token=AgoJb3JpZ2luX2VjED8aCXVzLXdlc3QtMiJIMEYCIQChXcRJl5T3Y8ECQj38fTXV5pN3KI5vdqbDT6LalqM0FAIhAKh1zdW8%2BIcVD%2FJgkSiV0GzSUfyw%2BqIxfIwpg3zTnhj%2BKtoDCDgQABoMMjc0NTY3MTQ5MzcwIgzO8%2FZAu9zYmPB%2BZLEqtwOvSL0tNh0vui%2B7M78LkIIKP%2FpUMYeWBWiNinukm16uGIJIMqgzF7MR9urwl2waLQPGjM04rR%2FctdhxkQgp%2BZ0VZbgDd5Of9jd0YQNQJSoAE2KQmYuDQokDMmwn3hz7pdSRMzMmCvlZV%2FKTwdd2VMu94Mg5Tj4Ougqfj0hHUUDPQnroYYKVbOv13LQ%2B9ZWVbbpuxBnRYw9ZgiSAp6Yu6ZAveydQKiJb9%2FXFiEMTwtouJLvqbCW%2FdUVT5A4dyO%2FotPeMleIUEsZlZ9YTTXvuQ6xw9cqA7rHz7CKK4%2B5P0HLU4Tvz2xgZcUNxsychCXx3O7TUHlfoFPmlnT3BUcTWZHOj4Q4GvQMjbIJ9xKgNANvG6zIFUlpOdkaOqNg6v6sXslagWtVdi2XBJ31tedx9%2Bla8RDW2QkxO8mUlQWgQkfIwEKhK3Yg2g8NQa9WrT98fNmEtHrVJ1jw%2Fhyl3cZiAumi%2Bn7DKe5awHjYyuMnLh6bJ%2BZs%2FJTkZh9p6HDxphea1Ob63FnPhoHVH%2FpwBA%2B0X%2FW0rt74H%2FUCSzdd5%2FqNYQF2N1nw8r6TTDuo3tKW5EPTyylMV0DKa%2FpIzMIf5k%2B0FOrMB3MPSmA1F4wA1SBmGeS0yliTcNp4HwC%2FjTDgIjro00eODfAA9cuM2Mu9Y2P1uO2nD2u0RIxMQZi5A1bHXCG0m1t3q29Df8wZPQHrgHHJ0qIURMaOojtXcGIBW1XpBX2YYkRYDPqgws3iMm7yIFrC%2FsSAkE2ypJsjl7T90H6gtgyC%2BiH99qAcjuMbuTb%2BAv4g20OLBRaRIkEG9lxNwimZdHI9tXbkJ5YN7aWHtcy2VZe9Y82w%3D&X-Amz-Signature=784456fa51c134e4cd0640628e76b512792d529976d393840ac4270a5aee7604&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22" alt="alt text" width="650px" height="500px">

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

