# Project-Visualization-transportation-usage
2021 Fall - Project in Electronics Manufacturing Data Analysis - SeoulTech, Department of Data Science  
팀원 : 이예빈, 정주현

## Data Visualization - 위드 코로나 시대의 이동수단 개선 방안 도출
### 분석 목표 - 2019년(COVID-19 이전), 2020년, 2021년을 비교하여 전염병이 장기화 됨에 따른 서울시의 이동 수단 이용 변화를 분석하고자 함
1. 이동 수단별 전체 이용량의 증감률 분석
  - 승용차, 지하철, 버스, 공공자전거(서울시 따릉이)의 전체 이용량 패턴 변화를 시각화  
2. 통행 목적에 따른 수단별 이용량의 증감률 분석  
  - 통행 목적을 세가지로 분류  
    -  일반적 통행: 주말과 공휴일을 제외한 평일 전체 시간대의 통행  
    -  필수 통행: 주말과 공휴일을 제외한 평일 출퇴근 시간대의 통행  
    -  비필수 통행: 주말과 공휴일의 전체 시간대의 통행  
  - 각 목적별 수단별 이용량 패턴 변화를 시각화
3. 지도 시각화
  - 각 수단별 증감률 분포에서 상 하위 지역을 지도로 시각화   

=> 각 이동 수단의 이용 변화 분석 결과를 확진자 추세, 정부 정책, 장기화에 따른 전염병에 대한 사람들의 인식 변화를 고려하여 해석한 후 위드 코로나 시대에 걸맞는 이동 수단 개선 방안을 도출

### data
![dataset](https://user-images.githubusercontent.com/46666833/163773725-fd00592d-9fb4-4649-b282-d7226cadcb76.PNG)

### process
#### 1. 데이터 전처리
  - 모든 데이터는 csv 또는 excel 형식으로 제공됨
  - 월별로 수집된 각 데이터를 합하여 각 연도별 통합데이터 구축
  - pandas 라이브러리를 활용하여 DataFrame 을 다루는 여러가지 함수 사용
    -  2021년의 데이터의 수집 기간 기준으로 2019, 2020년의 데이터를 축소  
    -  날짜 기준 데이터 분리  
       -  평일 전체 시간대, 평일 출퇴근 시간대, 주말 전체 시간대로 구분  
          -  출퇴근 시간은 버스 전용 차로 운행 시간을 기준으로 구분 (출근: 07시-10시, 퇴근: 17시-20시)  
       -  groupby 를 통해 일별 평균, 합계를 구하여 사용  
          -  승용차는 관측소의 문제로 결측치가 다수 존재 (관측소의 작동 오류, 점검 시간 등) 하므로 평균 사용, 나머지는 합계 사용  
          -  버스, 지하철은 승차와 하차 정보가 함께 존재하므로 승차 자료를 기준으로 사용  
    -  위치 기준 데이터 분리  
       -  수단별 위치를 기준으로 groupby 를 통해 각 위치의 이용량 평균, 합계를 구하여 사용  
          -  승용차는 관측소의 문제로 결측치가 다수 존재 (관측소의 작동 오류, 점검 시간 등) 하므로 평균 사용, 나머지는 합계 사용  
          -  각 관측소, 역, 정류소, 대여소의 위도, 경도 정보 활용  
#### 2. 데이터 시각화
  - matplotlib, seaborn 라이브러리를 활용하여 그래프 시각화, 지리적 시각화는 geopandas 라이브러리 등을 사용

### conclusion
- 이동 수단별 전체 이용량의 증감률 분석
  - 승용차
    - 개인 이동 수단이기 때문에 2020년 이용량이 크게 감소한 후, 2021년 이용량이 회복할 것이라 예상했으나 약간의 회복세를 제외하고는 전체적으로 감소세를 보임  
  - 지하철, 버스  
    - 대중교통을 피하는 경향에 맞게 급격하고 꾸준한 감소세를 보임  
    - 그러나 2021년에는 감소 후 회복되는 기간이 짧아짐을 알 수 있음  
  - 공공자전거
    - 타 이동 수단 대비 증가폭이 매우 크며 개인 이동 수단 답게 감염병 시기에 적극적으로 활용됨을 알 수 있음  
- 통행 목적에 따른 수단별 이용량의 증감률 분석
  - 필수 통행  
    - 재택 근무, 온라인 수업 등으로 승용차, 지하철, 버스에서 감소세를 보이긴 하나 출퇴근 시간대의 감소폭은 이외 시간대보다 낮음  
  - 비필수 통행  
    - 전염병에 대한 경각심에 따라 승용차, 지하철, 버스에서 꾸준한 감소세를 보임  
    - 그러나 승용차의 경우 휴가 시즌의 영향이 거의 없음    

=> 위드 코로나 정책과 더불어 대중교통 이용을 장려하고 승용차 이용을 억제하기 위한 개인의 인식 개선 및 홍보 정책이 필요함  
=> 서울시의 공공자전거를 활성화하기 위한 정책은 이미 많이 시행되고 있으며 이는 긍정적인 결과를 가져옴, 자전거 이외의 개인 이동 수단(전동킥보드 등)의 활성화 또한 앞으로 고려해볼 수 있음

한계)
  - 관측소의 결측치, 날짜의 결측치(공휴일에 맞춘 휴가 시기)등에 대한 구체적인 대체 방법이 필요함
  - 이용률 증감이 단순 코로나의 영향인지 다른 영향 또한 포함되었는지 불분명함
    - 정책 변화, 대여소의 설치 시기, 대여소 증가 등의 영향도 고려한 더욱 구체적인 분석이 필요함
    - 날씨의 영향 또한 무시할 수 없기 때문에 날씨 데이터를 추가로 확보한 더욱 구체적인 분석이 필요함
    - 온라인 수업, 재택 근무의 비율 등을 고려한 더욱 구체적인 분석이 필요함
