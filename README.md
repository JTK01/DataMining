# DataMining 10팀
# 주제 : 상권영역 별 분석 바탕 기반 공원 조성 제안
## 1. 주제 선정 배경 및 분석 목적
  유현준 교수님이 조선일보에 작성한 ‘공원과 스타벅스의 차이’라는 칼럼을 보고 주제를 선정하게 됐다. 교수님은 도심 속 공원이 부족하다고 지적하면서 공원의 필요성을 설명했다. 

  현재 누구든지 현관문을 열고 나왔을 때 만나는 모든 공간은 인도나 차도 같은 ‘이동하는 공간’이다. 이중 대부분은 걸어갈 만한 거리에 공원도 없고, 길거리에 벤치도 없다. 도심 속 ‘공짜로 머무를 수 있는 공간’이 생긴다면 다양한 종류의 사람들 사이에 공통의 추억을 만들어주고 그에 따라 서로를 이해할 가능성이 높아져 갈등 해결에 큰 도움을 줄 것이다.

<img width="1024" alt="image" src="https://github.com/JTK01/DataMining/assets/99972138/1ab0fbc9-f21c-407c-ab78-784b4b2d0156">

  위 사진은 유현준 교수님의 유튜브 채널의 영상 중 ‘건축가가 본 공원으로 세상을 바꾸는 방법’이라는 영상의 일부분이다. 교수님은 기존 공원들의 문제점으로 일반적인 상업 시설과 공원이 분리되어 있다는 점을 지적하셨다. 또한, 공원은 접근성이 매우 중요한데 현재 공원들은 너무 멀리 떨어져 있다는 문제도 언급했다. 이런 문제를 상권의 성격에 맞게 크고 작은 규모의 공원을 조성하면서 해결할 수 있다고 생각해 프로젝트 주제로 선정하게 되었다. 
  
따라서 분석 목적은 상권의 특성에 맞게 어떤 형태의 공원이 가장 적합할지 분석하고 제안하는 것이라고 할 수 있다. 상권의 인구 연령, 점포 수 등을 분석하고 결과에 따라 알맞은 휴식 공간을 제공할 수 있는 공원 조성안을 제안할 계획이다.
  
## 2. 데이터 획득 및 이해
데이터 획득 방법 : 서울 열린 데이터 광장 > 골목상권정보 > 상권 데이터
<img width="512" alt="image" src="https://github.com/JTK01/DataMining/assets/99972138/526de692-dd84-419f-baa9-ccca264f77c2">

위의 데이터 중에서 총 5개의 데이터를 사용했다.
1) 상주 인구 데이터.csv
2) 생활 인구 데이터.csv
3) 직장 인구 데이터.csv
4) 점포 데이터.csv
5) 아파트 데이터.csv

해당 데이터들은 17년 1분기 ~ 22년 4분기까지의 데이터가 모두 있어 가장 최근 데이터인 22년 4분기 데이터만 사용해서 분석을 진행했다. 또한, 사용한 데이터는 대부분 int로 이루어져 있고, null값은 없었다.

1) 상주 인구 데이터
<img width="715" alt="image" src="https://github.com/JTK01/DataMining/assets/99972138/51a4d99d-35d3-44e7-87e6-f8fb520243a1">

- 데이터 병합 과정에 사용하기 위해 상권 코드를 남겨 놓았다.
- 상권의 총 인구 수를 구하기 위해 총 상주인구 수를, 평균 연령을 계산하기 위해 각 연령대 별 상주인구 수를 slice했다.
- 기준 년과 기준 분기는 이미 22년 4분기로 통일을 해 최대한 열의 개수를 줄이기 위해 slice하지 않았다.

2) 생활 인구 데이터
<img width="715" alt="image" src="https://github.com/JTK01/DataMining/assets/99972138/2dcc74f9-612a-4d53-a58c-659e219aebe2">

- 상주 인구와 같은 이유로 상권 코드, 총 생활인구 수, 각 연령대 별 생활인구 수를 slice했다.

3) 직장 인구 데이터
<img width="715" alt="image" src="https://github.com/JTK01/DataMining/assets/99972138/ec97a9b1-6890-437d-bfae-c50b3725e50b">

- 상주 인구, 생활 인구와 같은 이유로 상권 코드, 총 직장인구 수, 각 연령대 별 직장인구 수를 slice했다.

4) 점포 데이터
<img width="715" alt="image" src="https://github.com/JTK01/DataMining/assets/99972138/6e63ca98-65b1-4796-a7ed-94e51eaf3051">

- 위 데이터와 같은 이유로 상권 코드를 slice했다.
- 식품 관련 서비스 업종을 뽑아내기 위해 서비스_업종_코드_명을 slice했고 식품 관련 서비스를 하는 점포의 수를 feature로 사용하기 위해 slice했다.

5) 아파트 데이터
<img width="715" alt="image" src="https://github.com/JTK01/DataMining/assets/99972138/e22f3055-d769-4f8c-813e-22ce9c427a73">

- 위 데이터와 같은 이유로 상권 코드를 slice했다.
- 아파트 단지 수를 slice했고, 아파트 평균 면적, 시가 등은 분석 취지와 맞지 않아 feature로 사용하지 않았다.


## 3. 분석
### 1) 데이터 전처리

- 상주인구, 생활인구, 직장인구의 3개 인구 데이터에서 총 인구 수, 상권 별 평균 나이, 상권 별 나이의 합을 계산해 새로운 dataset을 3개 만들었다.
- 각 dataset 별로 sum_age들을 합치고 총 인구 수로 나누는 방식으로 평균 연령을 계산했다.
###
<img width="624" alt="image" src="https://github.com/JTK01/DataMining/assets/99972138/2d6af7ca-3331-4925-bdcf-55f2918c83d0">

#
- 점포 데이터에서 음식 관련 점포 수를 계산했다.
- traget_name으로 설정한 업종명은 다음과 같다.
<img width="512" alt="image" src="https://github.com/JTK01/DataMining/assets/99972138/bec5a2af-c7d2-414c-99fa-ee0079f9cad3">

- "한식 전문점", "일식 전문점", "중식 전문점" 등은 분석의 취지에 맞지 않다고 생각해 포함하지 않았다.(보통 식당에서 식사를 마치고 나오지 테이크 아웃해서 근처에서 먹는 경우는 드물기 때문)
- 점포 수 데이터와 아파트 단지 수 데이터를 추출한 결과는 다음과 같다.
###
<img width="200" alt="image" src="https://github.com/JTK01/DataMining/assets/99972138/cdf7328e-92e3-4d2c-b5ad-6f72e4eadb90">
<img width="200" alt="image" src="https://github.com/JTK01/DataMining/assets/99972138/7d724ef4-035c-4171-9fa5-c9519bb0425c">

#
-> 위 dataset들을 하나로 합친 최종 dataset은 다음과 같다. 
###
<img width="500" alt="image" src="https://github.com/JTK01/DataMining/assets/99972138/2d851564-36a1-4ddd-9635-e5aaf687c96f">

### 2) Clustering

- Clustering model로 K-Means Clustering을 사용했다.
- K값을 선택하기 위해 inertia와 Silhouette Score를 계산했다.
###
<img width="600" alt="image" src="https://github.com/JTK01/DataMining/assets/99972138/7a3672c5-5071-4404-8773-884d9b1c876b">

- 위의 그래프에서 elbow method를 사용해 inertia가 꺾이는 K = 4를 선택했다.

#

- K = 4인 K-Means Clustering을 진행했고, 아래는 각 Cluster별 개수다.

###

<img width="444" alt="image" src="https://github.com/JTK01/DataMining/assets/99972138/c05d1e4c-2cff-44b5-96d8-87b4833c9d67">

#

- 각 Cluster 별로 feature들의 분포를 살펴보기 위해 Boxplot을 통해 시각화했다.

###

<img width="888" alt="image" src="https://github.com/JTK01/DataMining/assets/99972138/c5cfaa62-4525-4b3c-86f5-9d587ab1f510">

#

## 4. 결과
### 각 Cluster 별 Labeling 및 공원 형태 제시
- Cluster 0 : 아파트 단지 수가 많은 Cluster
  - 잠깐 나와 조깅/산책할 수 있는 산책로
  - 아이들과 함께할 수 있는 공간
- Cluster 1 : 평균 연령이 높은 Clsuter
  - 계산이나 가파른 경사가 없는 공원
  - 편하게 쉴 수 있는 공간 조성
  - 어르신들이 사용할 수 있는 시설(ex: 핀란드 헬싱키의 어르신 놀이터)
- Cluster 2 : 평균 연령이 낮은 Cluster
  - 아이들이 놀 수 있는 놀이기구 및 시설 마련
- Cluster 3 : 식품 관련 점포 수가 많은 Cluster
  - 음식을 먹을 수 있는 테이블 설치
  - 음식물 및 쓰레기 처리를 위한 시설 마련

## 5. 기대효과

아주 작은 공간이라도 주변 특성을 파악해 효율적인 공원을 조성하자는 것이 목표다. 크고 작은 공원들이 생기게 되면 모두가 공유할 수 있는 공통된 추억을 만들 수 있는 공간이 될 것이다. 그렇게 서로가 서로를 마주보는 시간과 공통된 공간이 많이 생기면 어렴풋한 타인이 실체화되고, 세대 간의 단절, 계층 간의 갈등이 감소할 것을 기대할 수 있다.

## 6. 한계점 및 추후 개선 방안

- 상권 근처의 공원 여부는 파악하지 못함
- 실제 사용가능한 공간이 있는지는 고려하지 않음
-> 관련 데이터를 확보하거나 지자체에서 관련 정보를 구해 분석을 진행할 수 있을 것이다.

## 7. 활용 자료 출처

- 조선일보: [유현준의 도시 이야기] 공원과 스타벅스의 차이
https://www.chosun.com/site/data/html_dir/2019/12/19/2019121903847.html
- 유튜브 셜록현준 : 강남문제, 공원과 벤치부터? 건축가가 본 공원으로 세상을 바꾸는 방법
https://www.youtube.com/watch?v=m1WUJETaI2U&t=612s
- 서울 열린데이터 광장 – 인기그룹데이터 – 골목상권분석정보
https://data.seoul.go.kr/dataList/3/literacyView.do
- 서울특별시 빅데이터 캠퍼스 – 데이터 분석 사례 - 지하철 공실 문제 해결을 위한 공유오피스 도입 및 활성화 방안
https://bigdata.seoul.go.kr/noti/selectNoti.do?r_id=P260&bbs_seq=605&ac_type=A1&sch_type=&sch_text=&currentPage=1
