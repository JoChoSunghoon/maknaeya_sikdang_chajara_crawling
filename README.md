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
<p>크게 2번의 과정으로 진행</p>
<p>chromedriver를 사용해 크롤링할 음식점의 url을 수집하고 저장한다</p>
<p>수집한 음식점 url를 통해 html 코드를 받아오고 파싱해서 태그 단위로 접근한다</p>
<p>MySQL과 연동하여 크롤링한 데이터를 관리한다</p>
<p>Python에서 MySQL의 데이터를 받아올 때 변환하기 쉽게 dataframe으로 받는다</p>
<p>DB에 저장되는 table은 2개로 1개는 음식점의 전반적인 정보를 관리하고 1개는 음식점의 리뷰들을 관리한다</p>

### 참고사항
<p> 보통 버튼을 눌러 실행할 때 url이 변경되는 경우는 webdriver의 사용없이 가능하나 위의 참조 사이트의 경우 #주소를 사용하여 진행되므로 webdriver를 사용하여 계속 버튼을 눌러주는 방식으로 원하는 정보를 계속 뽑아야 했다</p>
