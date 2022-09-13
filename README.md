# 🐽 Youtube_Comment_Crawler
유튜브 댓글 크롤러 ( Python, BeautifulSoup, Selenium )
<p align="center">
  <img width=800 src="./images/youtube_logo.png">
</p>

### 🗃 사용 라이브러리
- BeautifulSoup
- Selenium
- pandas
- requests

### 📝 참고 페이지 - https://bit.ly/2yyl7F5

### 인스타그램 크롤러 - https://github.com/SOMJANG/Instagram_Crawler

### 🖥 세부 설명

### 💻 get_urls_from_youtube_with_keyword(keyword) 💻
- 원하는 키워드에 대한 유튜브 영상 제목과 URL을 Crawling 하는 함수
- 여러 영상의 제목을 담은 titles와 URL을 담은 urls를 return 함

### 💻 get_channel_video_url_list 💻
- 원하는 채널에 대한 유튜브 영상 제목과 URL 을 Crawling 하는 함수
- 여러 영상의 제목을 담은 titles와 URL을 담은 urls를 return 함

### 💻 crawl_youtube_page_html_sources(urls) 💻
- 여러 영상에 대한 url을 담은 urls 리스트를 인자로 받음
- 각 URL 마다 Selenium으로 접근하여 댓글이 모두 로딩 될 수 있도록 스크롤을 시행하고
- 스크롤이 끝나면 HTML 코드를 Crawl한 후 
- 리스트에 담아 return 함

### 💻 get_user_IDs_and_comments(url_dict, video_type, html_source) 💻
- url과 제목이 담긴 dictionary 그리고 HTML 소스코드와 비디오 타입 (일반영상:watch / 쇼츠영상:shorts) 인자로 받음
- 각 페이지 소스코드에서 댓글 데이터 부분만 추출하고
- 리뷰 데이터에서 ID값과 댓글 부분을 추출한 후
- 페이지 별로 추출 결과를 dictionary 형태로 만든 뒤 return

### 💻 convert_crawl_result_dict_to_csv(crawl_result_dict) 💻
- 영상의 제목과 url 그리고 추출 결과가 담긴 dictionary 를 인자로 받음
- 추출결과를 DataFrame 형식으로 만들어줌
- titles의 제목들에서 특수문자를 제거한 제목을 csv 파일의 이름으로 사용하여
- 각각의 dataframe을 to_csv 를 활용해 csv파일로 저장함


### 🤩 코드 사용 예시
#### 예시 1 - 키워드 검색 > 동영상 목록 url 크롤링 > 각 영상별 결과 dictionary 생성 > dic to csv 저장
```Python3
crawling_result_list = []

titles, urls = get_urls_from_youtube_with_keyword(
    keyword = "레고"
)


watch_url, shorts_url = divide_watch_shorts(titles, urls)

watch_url = watch_url[:1]

# watch_url
html_sources = crawl_youtube_page_html_sources(watch_url)

for url_dict, html_source in zip(watch_url, html_sources):
    crawl_result = get_user_IDs_and_comments(
        url_dict=url_dict, 
        video_type="watch", 
        html_source=html_source
    )
    
    crawling_result_list.append(crawl_result)


for crawl_result in crawling_result_list:
    convert_crawl_result_dict_to_csv(
        crawl_result_dict=crawl_result
    )
```

#### 예시 2 - 채널 이동 > 동영상 목록 url 크롤링 > 각 영상별 결과 dictionary 생성 > dic to csv 저장
```Python3
crawling_result_list = []

titles, urls = get_urls_from_youtube_with_keyword(
    keyword = "레고"
)


watch_url, shorts_url = divide_watch_shorts(titles, urls)

watch_url = watch_url[:1]

# watch_url
html_sources = crawl_youtube_page_html_sources(watch_url)

for url_dict, html_source in zip(watch_url, html_sources):
    crawl_result = get_user_IDs_and_comments(
        url_dict=url_dict, 
        video_type="watch", 
        html_source=html_source
    )
    
    crawling_result_list.append(crawl_result)


for crawl_result in crawling_result_list:
    convert_crawl_result_dict_to_csv(
        crawl_result_dict=crawl_result
    )
```

#### 예시 3 - 채널 이동 > 동영상 목록 url 크롤링 > 각 영상별 결과 dictionary 생성 > dic to csv 저장
```Python3
crawling_result_list = []

titles, urls = get_channel_video_url_list(
    channel_url="https://www.youtube.com/c/%EA%BE%B8%EC%82%90KUPI/videos"
)


watch_url, shorts_url = divide_watch_shorts(titles, urls)

watch_url = watch_url[:1]

# watch_url
html_sources = crawl_youtube_page_html_sources(watch_url)

for url_dict, html_source in zip(watch_url, html_sources):
    crawl_result = get_user_IDs_and_comments(
        url_dict=url_dict, 
        video_type="watch", 
        html_source=html_source
    )
    
    crawling_result_list.append(crawl_result)


for crawl_result in crawling_result_list:
    convert_crawl_result_dict_to_csv(
        crawl_result_dict=crawl_result
    )
```
