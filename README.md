# 원묵고 빅데이터 원리 탐구 진로별 데이터 프로젝트

고등학교 「빅데이터 원리 탐구」 수업에서 쓰는 진로 분야별 공개 데이터입니다. 학생은 자기 진로에 맞는 CSV 하나를 골라 불러오기 → 구조 확인 → 기초 통계 → 결측치 처리 → 새 열·그룹별 분석 → 시각화 순서로 프로젝트를 진행합니다. 필터링·정렬·문자열 가공은 쓰지 않아도 되도록 데이터를 다듬었습니다.

모든 파일은 공개 라이선스 원자료를 교사가 수업용으로 줄이고 다듬은 가공본입니다. 원출처와 바꾼 내용은 `guides/`의 파일별 안내에 적었습니다.

## 진로 분야별 데이터

| 분야 | 파일 | 내용 | 행 × 열 | 관련 진로 |
|---|---|---|---:|---|
| 교육 | `students.csv` | 포르투갈 고등학생의 생활과 세 학기 성적 | 649 × 15 | 교육, 상담, 심리, 사회복지 |
| 생명 | `biology.csv` | 붓꽃 3종의 꽃잎·꽃받침 측정값 | 150 × 5 | 생명과학, 생태, 농업, 생물정보 |
| 의료 | `health.csv` | 심장질환 검사 기록 | 303 × 12 | 보건, 간호, 의학, 의료정보 |
| 환경 | `environment.csv` | 베이징 대기질 시간별 관측 | 8,856 × 12 | 환경, 화학, 기상, 도시계획 |
| 경제 | `economy.csv` | 11개국 소비자물가 상승률 | 165 × 7 | 경제, 금융, 국제통상, 정책 |
| 유통 | `retail.csv` | 온라인 쇼핑몰 거래명세(취소·반품 제외) | 4,812 × 13 | 경영, 마케팅, 회계, 물류 |
| 미디어 | `movies.csv` | 평가가 충분한 1970년 이후 영화와 평점 | 3,455 × 9 | 미디어, 영화, 문화콘텐츠 |
| 체육 | `sports.csv` | 메이저리그 팀 시즌 기록 | 1,028 × 13 | 체육, 스포츠경영, 스포츠 통계 |
| 공학 | `engineering.csv` | 콘크리트 배합별 압축강도 실험 | 1,005 × 14 | 토목, 건축, 재료, 화학·환경공학 |
| 컴퓨터 | `computer.csv` | 전 세계 개발자 설문 2025 | 470 × 17 | 소프트웨어, 인공지능, 정보보안, IT |
| 미술 | `art.csv` | 뉴욕현대미술관(MoMA) 소장품 | 1,037 × 14 | 미술, 디자인, 건축, 사진, 미술사 |
| 관광·식품 | `tourism_food.csv` | 멕시코 관광도시 식당 평가 | 1,161 × 12 | 관광, 외식·조리, 식품, 서비스경영 |
| 행정 | `administration.csv` | 18개국 거버넌스 지표 | 486 × 9 | 행정, 공무원, 정책, 법·정치외교 |
| 천문 | `astronomy.csv` | 맨눈으로 보이는 별의 거리·밝기·색·분광형 | 936 × 13 | 천문, 우주과학, 물리, 지구과학, 항공우주 |

수업 시간 예제용으로 `students_lesson.csv`(649 × 11, 결측 없음)가 따로 있습니다.

## 전처리 포인트와 분석 예시

| 파일 | 필요한 전처리 | 그룹별 분석 및 시각화 예시 |
|---|---|---|
| students.csv | 빈칸 확인·처리, 성적 변화 열 생성 | 공부 구간별 평균 성적 막대
| biology.csv | 빈칸 확인·처리, 꽃잎 길이/너비 비율 열 생성 | 종·꽃잎 크기별 꽃잎·꽃받침 길이와 너비, 종별 비율 막대
| health.csv | 빈칸 확인·처리, 예상 최대 심박수 대비 비율 열 생성(`max_heart_rate / (220 - age)`) | 흉통 유형·심장질환 여부별 최대 심박수, 혈압·콜레스테롤 수준별 진단 단계, 나이 구간별 콜레스테롤
| environment.csv | 빈칸 확인·처리, 초미세먼지/미세먼지 비율 열 생성 | 계절·시간대·바람 세기·평일/주말·측정소별 초미세먼지 막대, 시각별 선
| economy.csv | 물가 상승률 결측 확인·처리(베네수엘라 8년 연속 결측), 물가 목표(2%)와의 차이 열 생성(`inflation_rate - 2`) | 국가·대륙·경제 유형·시기별 평균·중앙값 막대, 연도별 선
| retail.csv | 빈칸 확인·처리, 명세금액(`quantity × unit_price_gbp`) 열 생성 | 요일·시간대·가격 구간·주문 규모·지역별 구매 금액·수량 막대, 월별 선
| movies.csv | 평가 결측 확인·처리, 영화 나이(`2018 - release_year`) 열 생성 | 장르·연대·인기 구간별 평균 평점 막대, 연대별 선
| sports.csv | 빈칸 확인·처리, 승률(`wins / games`) 열 생성 | 연대·리그·승리 시즌 여부·우승 여부별 홈런·득점·승 막대, 연도별 선
| engineering.csv | 빈칸 확인·처리, 물-시멘트비(`water / cement`) 열 생성 | 재령 구간·플라이애시 사용 여부·감수제 사용 여부·시멘트 양별 압축강도 막대, 재령별 선
| computer.csv | 빈칸 확인·처리(직무 만족도 약 19% 결측), 월 소득(`salary_usd / 12`) 열 생성 | AI·Python 사용, 경력 단계, 회사 규모, 국가별 연봉 막대, 근무 형태별 직무 만족도
| art.csv | 빈칸 확인·처리, 면적(`height_cm × width_cm`)·제작 시 작가 나이(`year_made - birth_year`) 열 생성 | 분류·제작 시기·국적·성별별 크기·제작 연도·작품 수 막대
| tourism_food.csv | 빈칸 확인·처리, 음식·서비스 평가 평균 열 생성 | 가격대·요리 종류·주류·도시·흡연 정책·손님 예산별 평가 막대
| administration.csv | 결측과 빠진 연도 확인·처리, 4개 지표 평균 열 생성 | 대륙·국가·시기별 정부효과성·법치·부패 통제 막대, 연도별 선
| astronomy.csv | 빈칸 확인·처리, 광년 환산(`distance_pc × 3.262`) 열 생성 | 분광형·거리 구간·반구별 색지수·절대/겉보기 등급 막대

## Colab에서 불러오기

```python
import pandas as pd

url = "https://raw.githubusercontent.com/daradarav86/bigdata/main/data/engineering.csv"
df = pd.read_csv(url)
display(df.head())
```

`engineering.csv` 자리에 위 표의 파일 이름을 넣으면 됩니다.

## 폴더 구성

```
data/       CSV 15개 (수업용 1, 프로젝트용 14), UTF-8 BOM
guides/     파일별 안내: 원자료, 준비 기준, 열 설명, 수업용 가공, 배포 조건
licenses/   데이터별 이용조건과 원 제공자 README·고지문
```

## 수업용 가공 안내

전처리 연습을 위해 대부분의 파일에 원자료에 없던 **빈칸**을 넣었습니다. 있을 수 없는 값(음수 나이, 범위 밖 점수, -999, `not_a_date`, `?` 등)은 모두 **빈칸으로 바꿔 두었으므로, 이 저장소의 파일에는 결측치(빈칸) 외의 이상값이 없습니다.** 열별 개수는 각 guides 파일의 "수업용 가공"에 적었습니다. 원자료의 실제 결측과 수업용으로 만든 빈칸을 구분해 두었으니, 분석 결과를 원자료의 사실로 인용하지 마세요.

**2026-11-07에 학생이 분석하기 쉽게 다시 정리했습니다.** (`students_lesson`은 바뀌지 않았습니다. `students`는 열 이름만 바뀌었고, `biology`·`economy`·`administration`은 열 이름은 그대로이고 열을 더했습니다.)

- **열 이름**: 약어·공백·괄호·단위가 들어간 이름(`trestbps`, `G3`, `Height (cm)`, `Cement (component 1)(kg in a m^3 mixture)` 등)을 영어 소문자·밑줄의 짧은 이름으로 바꿨습니다. 예전 이름과의 대응표는 각 guides 파일에 있습니다. `students`는 수업용 `students_lesson`과 같은 이름(`study_level`, `final_score` 등)으로 맞췄습니다.
- **한 칸에 여러 값이 든 열**(영화 장르 `Comedy|Drama`, 개발자 사용 언어 `Python;C#`, 식당 요리 종류, 작가 여러 명)은 `groupby`로 묶을 수 없어서 첫 번째 값, 개수, 예/아니오 열로 바꿨습니다.
- **숫자 코드**(흉통 유형 1~4, 운동유발협심증 0/1)는 평균이 의미 없어서 단어(`typical_angina`, `yes`/`no`)로 바꿨습니다.
- **비교할 수 있는 그룹 열을 더했습니다**: 나이·연대·계절·시간대·지역·시기 같은 구간 열과 `yes`/`no` 열(`uses_fly_ash`, `winning_season`, `uses_python` 등)입니다. 학생이 구간을 만들거나 문자열을 자르지 않아도 되고, 데이터마다 서로 다른 주제의 질문 6개 안팎을 해 볼 수 있습니다. 질문 예시는 각 guides 파일의 "분석 아이디어" 표에 있습니다(모두 이 파일로 계산해 확인함).
- **그래프 순서**: 이름 순서대로 나오는 막대그래프가 시간·크기 순서가 되도록, 순서가 있는 그룹은 이름 앞에 번호를 붙였습니다(`1_winter`, `3_afternoon`, `2_medium`, `stage2_14_28d` 등).
- **너무 작은 그룹**(응답·작품·영화가 15~30개 미만)은 `Other`/`other`로 합쳤습니다.
- **분석을 왜곡하던 행을 뺐습니다**: 온라인 쇼핑몰(retail)의 취소·반품과 배송비 같은 상품이 아닌 항목, 영화(movies)의 평가 수 5개 미만, 개발자 설문(computer)의 연봉이 없거나 1,000달러 미만인 응답. 중복 행은 art와 engineering에서 뺐습니다(biology의 1개는 원자료 그대로 둡니다).
- **빈칸 비율을 조정**했습니다. `df.dropna()`로 지워지는 행이 대부분 10% 안팎, 가장 많은 computer도 3분의 1 정도입니다.
- **잘못 들어 있던 값을 고쳤습니다**: economy의 `year`(프랑스 2024년 0 → 2024, 인도 2022년 2099 → 2022).

## 라이선스와 원자료

| 데이터 | 원 출처 | 조건 |
|---|---|---|
| 학생 두 파일 | Paulo Cortez, UCI Student Performance https://doi.org/10.24432/C5TG7T | CC BY 4.0 |
| 영화 | GroupLens MovieLens latest-small, Harper & Konstan 2015 https://doi.org/10.1145/2827872 | MovieLens 자체 조건, 비상업적 사용·동일조건 재배포. licenses의 원 README 유지 |
| 환경 | Song Chen, UCI Beijing Multi-Site Air Quality https://doi.org/10.24432/C5RK5G | CC BY 4.0 |
| 경제 | World Bank WDI FP.CPI.TOTL.ZG, 원 제공자 IMF International Financial Statistics https://databank.worldbank.org/metadataglossary/world-development-indicators/series/FP.CPI.TOTL.ZG | CC BY 4.0 및 https://data.worldbank.org/summary-terms-of-use 추가조건 |
| 스포츠 | SABR / Sean Lahman Teams, CSV via Rdatasets https://sabr.org/lahman-database/ | CC BY-SA 3.0, 가공본에도 동일조건 |
| 의료 | Janosi, Steinbrunn, Pfisterer, Detrano, UCI Heart Disease https://doi.org/10.24432/C52P4X | CC BY 4.0 |
| 생물 | Fisher, UCI Iris bezdekIris.data https://doi.org/10.24432/C56C76 | CC BY 4.0 |
| 유통 | Daqing Chen, UCI Online Retail https://doi.org/10.24432/C5BW33 | CC BY 4.0 |
| 공학 | I-Cheng Yeh, UCI Concrete Compressive Strength https://doi.org/10.24432/C5PK67 | CC BY 4.0 |
| 컴퓨터 | Stack Overflow Annual Developer Survey 2025 https://survey.stackoverflow.co/ | ODbL 1.0(내용 DbCL 1.0), 가공본에도 동일조건 |
| 미술 | The Museum of Modern Art (MoMA) Collection https://doi.org/10.5281/zenodo.23493633 | CC0 1.0, MoMA 출처 표시 요청. licenses의 원 README 유지 |
| 관광·식품 | Ponce Medellín & González Serna, UCI Restaurant & consumer data https://doi.org/10.24432/C5DP41 | CC BY 4.0 |
| 행정 | World Bank Worldwide Governance Indicators 2026 Update https://www.govindicators.org | CC BY 4.0 및 World Bank 데이터 이용조건 |
| 천문 | HYG Star Database v4.4 (Hipparcos·Yale Bright Star·Gliese 통합) https://codeberg.org/astronexus/hyg | CC BY-SA 4.0, 가공본에도 동일조건. licenses의 고지문 유지 |

- CC BY 4.0: https://creativecommons.org/licenses/by/4.0/
- CC BY-SA 3.0: https://creativecommons.org/licenses/by-sa/3.0/
- CC BY-SA 4.0: https://creativecommons.org/licenses/by-sa/4.0/
- ODbL 1.0: https://opendatacommons.org/licenses/odbl/1-0/
- CC0 1.0: https://creativecommons.org/publicdomain/zero/1.0/

저장소 전체에 하나의 데이터 라이선스를 적용하지 않습니다. 파일마다 원출처·가공 사실·각 이용조건을 유지하며, 원 제공자가 이 가공본이나 수업을 보증하거나 추천하지 않습니다. 자료 확인·수업용 준비일: 2026-10-11 (공학·컴퓨터·미술·관광식품·행정 2026-10-24, 천문 2026-10-30).

## 프로젝트 노트북

`notebooks/project_template.ipynb` — 조별·개별 프로젝트용 빈칸 노트북(미션 0~4(질문 틀·추천 짝·막히면 표 포함): 불러오기 → 구조 확인 → 빈칸 처리 → 그룹별 분석 → 그래프 → 해석). `___`을 채우며 진행하고, 파일마다 추천하는 (묶는 기준, 계산할 열) 짝이 첫머리 표에 있습니다.

Colab에서 바로 열기: https://colab.research.google.com/github/daradarav86/bigdata/blob/main/notebooks/project_template.ipynb

예시 완성본(교육·상담 진로): https://colab.research.google.com/github/daradarav86/bigdata/blob/main/notebooks/example_students.ipynb
