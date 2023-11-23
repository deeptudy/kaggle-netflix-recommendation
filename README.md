# kaggle-netflix-recommendation
Kaggle, Netflix data analysis and visualization, NLP, Recommendation Model

## 1. Intro
#### 1-1. Topic
- 넷플릭스 추천 텍스트 데이터의 전처리와 시각화를 경험해보기 위함.

#### 1-2. Contents
1. EDA
2. 시각화
3. 모델선정

#### 1-3. Dataset
[캐글 넷플릭스 데이터](https://www.kaggle.com/datasets/shivamb/netflix-shows)

- Total: 12 columns
    
    
    | no. | column name | description | type | note |
    | --- | --- | --- | --- | --- |
    | 0 | show_id | 영상의 고유 ID값 | object |  |
    | 1 | type | 영상이 영화인지, TV show인지를 구분 | object |  |
    | 2 | title | 제목 | object |  |
    | 3 | director | 감독 이름 | object |  |
    | 4 | cast | 배우 이름 | object |  |
    | 5 | country | 제작 국가 | object |  |
    | 6 | date_added | Netflix에 해당 영상이 추가된 날짜 | object |  |
    | 7 | release_year | 실제 영상이 방영된 날짜 | int64 |  |
    | 8 | rating | 영상물 등급 (예: 15세 이상, 청불) | object |  |
    | 9 | duration | 총 영상 길이 (분 단위 혹은 시즌 개수 단위) | object |  |
    | 10 | listed_in | 장르 | object |  |
    | 11 | description | 영상에 대한 짧은 소개 | object |  |



#### 1-4. Roles
1. Player1 : 안지우
2. Player2 : 김선들
3. Player3 : 한상준
4. Player4 : 정서익

## 2. Review

### 용어 정리
#### 란?
    - 
#### 2-1. 결측치 및 데이터 오류확인

- director 2634
- cast 825
- country 831 --> 오류 없음
- date_added 10
- rating 4 --> 데이터 오류 존재 --> 해결
- duration 3

##### 결측치 처리 아이디어 
- IMDB 데이터를 추가로 이용 title(original_title)로 동일한 영화를 매치해서 Netflix 데이터셋에 있는 결측값을 처리하는데 이용

#### 2-2. 시각화
#### Netflix 데이터 시각화

##### release_year과 type과의 관계 그래프 
![image](https://github.com/deeptudy/kaggle-netflix_recommendation/assets/92513469/4fa01aea-fde1-4a76-b364-2bd07390feeb)
- TV show 보다 Movie 의 제작량이 많은 것을 확인할 수 있다.
- 2000 년도부터 꾸준히 상승세를 보이다 2020 년도부터 하락세를 보인다.

##### year_added과 type과의 관계 그래프( year_added 칼럼을 추가)
![image](https://github.com/deeptudy/kaggle-netflix_recommendation/assets/92513469/3ac3c924-b147-4aa7-9b39-d0d616f6ef82)
- 2015 년도부터 급격한 상승세를 보이다 2020 년도부터 하락세를 보인다
  
##### month_added과 type과의 관계 그래프( month_added 칼럼을 추가)
![image](https://github.com/deeptudy/kaggle-netflix_recommendation/assets/92513469/ca22abdf-16bf-4762-bab9-2b5e6e2b67cb)
- July, December에 영화 상영 많음, May, February 영화 상영 적음 성수기와 비수기 구분 가능하다.
  
##### country(나라별) show_id(영상) 관계 그래프
![image](https://github.com/deeptudy/kaggle-netflix_recommendation/assets/92513469/1390af4e-8ab5-4ef3-b3fb-88ba0d9d25f6)
- United States, India, United Kingdom 순으로 상영작들에서 차이가 남을 알 수 있음 미국이 가장 큰 시장
  
##### country(나라별) show_id(영상) count 관계 그래프
![image](https://github.com/deeptudy/kaggle-netflix_recommendation/assets/92513469/151f39a4-5f31-4cd7-96df-58b12a8d7d3b)

##### release_year(개봉연도별) country(나라별) show_id(영상) count 관계 그래프
![image](https://github.com/deeptudy/kaggle-netflix_recommendation/assets/92513469/e3058016-bb65-4d65-be98-7c440c6835e4)

##### duration별 분포 그래프
![image](https://github.com/deeptudy/kaggle-netflix_recommendation/assets/92513469/8718905a-31b4-406a-a78c-17685f1aeaa3)
- 75~120 사이에 상영시간 분포를 보임 100분 정도의 영상시간이 가장 많음
  
#### Netflix & IMDB 데이터 시각화
- 평점을 얻어오기 위해 IMDB movies 데이터셋을 추가해서 사용합니다. (Inner Join)

#### 가장 평점이 좋은 영화나 드라마 10개를 시각화
![image](https://github.com/deeptudy/kaggle-netflix_recommendation/assets/92513469/426f370e-aae1-4978-9ec1-47c1fe85285e)

#### 가장 많은 영화를 상영했던 연도 시각화
![image](https://github.com/deeptudy/kaggle-netflix_recommendation/assets/92513469/1254cb47-e1a5-424c-8650-262f5e9d7ea7)
- 2018 2017 2019 2020 은 많은 영화를 상영했던 연도로 보임
- 
#### 영화의 상영 시간 분포도
![image](https://github.com/deeptudy/kaggle-netflix_recommendation/assets/92513469/a9b895de-e269-4ed1-aa6d-2e6615ac3b70)

#### WordCloud
![image](https://github.com/deeptudy/kaggle-netflix_recommendation/assets/92513469/d6366ec0-0476-4e6c-8b56-a05ef267ed78)

#### Lolipop plots to see the counts of movies based on genres
![image](https://github.com/deeptudy/kaggle-netflix_recommendation/assets/92513469/6babe9e3-3e6e-4286-aa71-7d89b3b26a54)


## 3. Conclusion
### 분석결과
- United States 가 제작 참여한 영상이 압도적으로 많다.
  - United States 다음으론 India, United Kingdom 등 영어권 나라가 있었다.
  - 시장규모와 비례할 것이라 생각함
- 시간대별 나라별 영상의 제작 추이는 특이사항이 없다.
- 상영작 개수는 2015 년도부터 급격한 상승세를 보이다 2020 년도부터 하락세 보인다.
- 상영시간을 100분 정도로 많은 영화들이 제작되는걸 알 수 있음
- July, December에 영화 상영 많음, May, February 영화 상영 적음 이를 통해 성수기, 비수기를 추론가능
  - 경쟁을 피하기위한 적절한 상영시기(달) 추론 가능
  - 2018년도는 가장 많은 영화를 상영한 해
  - 

### Content-Based Recommendation System
- Content-Based Filtering: 사용자가 소비한 아이템에 대해 아이템의 내용(content)이 비슷하거나 특별한 관계가 있는 다른 아이템을 추천하는 방법
- using TF-IDF(Term Frequency-Inverse Document Frequency) scores and consine similarity
-- 정보검색에 사용되는 전통적인 방법인 TF-IDF와 넷플릭스 데이터를 이용하여 추천 시스템을 구축해보는것을 시도함
  
1) Use 'description' to recommend similar movies or TV shows
2) Strings handling (stopwords, empty string, etc.)
3) Create TF-IDF matrix 
4) Use consine similarity score to recommend

EX) "Pulp Fiction" 을 입력하면

<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>title_x</th>
      <th>director_x</th>
      <th>listed_in</th>
      <th>avg_vote</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>598</th>
      <td>Rango</td>
      <td>Gore Verbinski</td>
      <td>Children &amp; Family Movies, Comedies</td>
      <td>7.2</td>
    </tr>
    <tr>
      <th>3003</th>
      <td>Hükümet Kadin</td>
      <td>Sermiyan Midyat</td>
      <td>Comedies, International Movies</td>
      <td>6.5</td>
    </tr>
    <tr>
      <th>3130</th>
      <td>Jericho</td>
      <td>Merlin Miller</td>
      <td>Classic &amp; Cult TV, TV Action &amp; Adventure, TV D...</td>
      <td>6.1</td>
    </tr>
    <tr>
      <th>3129</th>
      <td>Jericho</td>
      <td>Thornton Freeland</td>
      <td>Classic &amp; Cult TV, TV Action &amp; Adventure, TV D...</td>
      <td>6.1</td>
    </tr>
    <tr>
      <th>721</th>
      <td>In a Valley of Violence</td>
      <td>Ti West</td>
      <td>Action &amp; Adventure</td>
      <td>6.0</td>
    </tr>
    <tr>
      <th>2409</th>
      <td>Rainbow Time</td>
      <td>Linas Phillips</td>
      <td>Comedies, Dramas, Independent Movies</td>
      <td>5.9</td>
    </tr>
    <tr>
      <th>2157</th>
      <td>Fun Mom Dinner</td>
      <td>Alethea Jones</td>
      <td>Comedies, International Movies</td>
      <td>5.2</td>
    </tr>
    <tr>
      <th>2189</th>
      <td>The Killer</td>
      <td>Marcelo Galvão</td>
      <td>Action &amp; Adventure, International Movies</td>
      <td>4.6</td>
    </tr>
    <tr>
      <th>1224</th>
      <td>Justice</td>
      <td>Richard Gabai</td>
      <td>Movies</td>
      <td>4.5</td>
    </tr>
    <tr>
      <th>1225</th>
      <td>Justice</td>
      <td>Richard Gabai</td>
      <td>Movies</td>
      <td>4.0</td>
    </tr>
  </tbody>
</table>
</div>

- 다음과 같은 결과 리턴
    
