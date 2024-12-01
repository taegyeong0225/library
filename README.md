# 도서 대출량에 영향을 주는 환경 요인 분석
데이터 위치 : 구글 드라이브 > 내 드라이브 > bigdata_processing 폴더 안애 위치

[🙇🏻‍♀️ 분석 과정 보기(.ipynb)](https://github.com/taegyeong0225/bigdata-processing/blob/main/%E1%84%87%E1%85%B5%E1%86%A8%E1%84%83%E1%85%A6%E1%84%8B%E1%85%B5%E1%84%90%E1%85%A5%E1%84%8E%E1%85%A5%E1%84%85%E1%85%B5_%E1%84%80%E1%85%B5%E1%84%86%E1%85%A1%E1%86%AF_%E1%84%83%E1%85%A2%E1%84%8E%E1%85%A6_%E1%84%91%E1%85%B3%E1%84%85%E1%85%A9%E1%84%8C%E1%85%A6%E1%86%A8%E1%84%90%E1%85%B3.ipynb)

[🙇🏻‍♀️ 파이썬 code로 보기(.py)](https://github.com/taegyeong0225/bigdata-processing/blob/main/%E1%84%87%E1%85%B5%E1%86%A8%E1%84%83%E1%85%A6%E1%84%8B%E1%85%B5%E1%84%90%E1%85%A5%E1%84%8E%E1%85%A5%E1%84%85%E1%85%B5_%E1%84%80%E1%85%B5%E1%84%86%E1%85%A1%E1%86%AF_%E1%84%83%E1%85%A2%E1%84%8E%E1%85%A6_%E1%84%91%E1%85%B3%E1%84%85%E1%85%A9%E1%84%8C%E1%85%A6%E1%86%A8%E1%84%90%E1%85%B3.py)

## 1. 프로젝트 개요 및 목표

2023년 국민 독서 실태조사에 따르면 성인의 최근 10년간 종합 독서율 추이는 계속 감소 하고 있는 추세이다.
(출처 : 2023년 국민 독서 실태조사 2p, 성인 국민 독서 실태조사 결과(2013~2023)

 이와 함께, 최근에는 MZ 세대의 문해력 부족이 사회적 논란이 되고 있다. 예를 들어, 2020년 8월 광복절 당시 월요일인 17일을 임시공휴일로 지정하면서 ‘사흘 연휴’라는 표현을 사용하였는데, 이를 ‘4일 연휴’로 오해하거나, 왜 ‘3일 연휴’를 ‘사흘’로 표현했는지 묻는 사례가 있었다. 또한, 2022년 8월에는 웹툰 작가 변덕이 사인회 예약 안내문에서 사용한 ‘심심한 사과’라는 표현을 본래 뜻인 ‘매우 깊고 간절하다’로 이해하지 못하고, ‘지루하고 재미없는 사과’로 해석한 사례가 있었다.

 2024년 10월 7일 발표된 ‘학생 문해력 실태 교원 인식 설문조사’에 따르면, 교사들은 학생들의 문해력 저하의 주요 원인으로 29.2%가 ‘독서 부족’을 꼽았다. 또한, 문해력 개선 방안으로는 32.4%가 ‘독서활동 강화’를 지목한 것으로 나타났다.
 (출처 : 학생 문해력 실태 교원 인식 설문조사 결과 발표(2024.10.07.), 한국 교원 단체 총연합회)


 이처럼 문해력 부족 문제가 논란이 되고 있는 가운데, 독서를 장려해야 한다는 사회적 공감대가 형성되고 있다. 이에 따라 문화체육관광부는 2024년 4월 22일에 ‘제4차 독서문화진흥 기본계획(2024~2028)’을 발표하며, 독서 활성화를 위한 정책적 노력을 강화하고 있다.

 책을 접하기 가장 쉬운 장소 중 하나는 도서관이다. 본 프로젝트에서는 지역별 전국 도서관 도서 대출 수 데이터와 다른 공공 데이터를 추가로 결합하여 도서 대출량에 영향을 미치는 환경 요인을 분석하고자 한다. 또한, 이 결과로 대출량 및 독서율을 높일 수 있는 구체적인 방안을 제안하는 것을 목표로 하고 있다.

해당 프로젝트에 앞서 세 가지 가설을 설정하였다.

**가설 1. 도서관의 수와 도서 대출 수는 비례할 것이다.**
  도서관이 많은 지역은 도서관을 접할 기회가 많기 때문에 도서 대출 수가 정비례할 수 밖에 없을 것이다.

**가설 2. 도서 대출 수는 학원 같은 교육 시설 수에 영향을 받을 것이다.**
  교육 시설이 많은 지역에서 독서 교육을 더 많이 받았을 것이며, 도서 대출을 많이 할 것이다.

**가설 3. 문화시설 수가 많은 곳일 수록 도서 대출 수가 높을 것이다.**
  문화 생활, 독서 모두 취미 생활 중 하나이므로, 문화 시설 수가 많을수록 도서 대출량이 높을 것이다. 

**가설 4. 접근성이 높을 수록 도서 대출 수가 높을 것이다.**
  도서관이 주변에 없거나 가기 힘들다면 도서 대출을 하기가 꺼려질 수 있기 때문에, 접근성이 높은 수록 도서 대출 수가 높을 것이라고 생각했다.

![image](https://github.com/user-attachments/assets/64094484-2355-4369-bfd9-aea770d0bb7d)
