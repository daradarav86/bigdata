# 원묵고 빅데이터 원리 탐구 진로별 데이터 프로젝트

고등학교 「빅데이터 원리 탐구」 수업에서 쓰는 진로 분야별 공개 데이터입니다. 학생은 자기 진로에 맞는 CSV 하나를 골라 12~17차시 동안 불러오기 → 선택·필터링 → 결측치·중복값 처리 → 이상치 수정 → 분석 → 시각화 순서로 프로젝트를 진행합니다.

모든 파일은 공개 라이선스 원자료를 교사가 수업용으로 줄이고 다듬은 가공본입니다. 원출처와 바꾼 내용은 `guides/`의 파일별 안내에 적었습니다.

## 진로 분야별 데이터

| 분야 | 파일 | 내용 | 행 × 열 | 관련 진로 |
|---|---|---|---:|---|
| 교육 | `students.csv` | 포르투갈 고등학생의 생활과 세 학기 성적 | 649 × 15 | 교육, 상담, 심리, 사회복지 |
| 생명 | `biology.csv` | 붓꽃 3종의 꽃잎·꽃받침 측정값 | 150 × 5 | 생명과학, 생태, 농업, 생물정보 |
| 의료 | `health.csv` | 심장질환 검사 기록 | 303 × 8 | 보건, 간호, 의학, 의료정보 |
| 환경 | `environment.csv` | 베이징 대기질 시간별 관측 | 8,856 × 9 | 환경, 화학, 기상, 도시계획 |
| 경제 | `economy.csv` | 11개국 소비자물가 상승률 | 165 × 4 | 경제, 금융, 국제통상, 정책 |
| 유통 | `retail.csv` | 온라인 쇼핑몰 거래명세 | 6,103 × 7 | 경영, 마케팅, 회계, 물류 |
| 미디어 | `movies.csv` | 영화 9,742편과 평점 | 9,742 × 5 | 미디어, 영화, 문화콘텐츠 |
| 체육 | `sports.csv` | 메이저리그 팀 시즌 기록 | 1,028 × 11 | 체육, 스포츠경영, 스포츠 통계 |
| 공학 | `engineering.csv` | 콘크리트 배합별 압축강도 실험 | 1,030 × 9 | 토목, 건축, 재료, 화학·환경공학 |
| 컴퓨터 | `computer.csv` | 전 세계 개발자 설문 2025 | 2,005 × 14 | 소프트웨어, 인공지능, 정보보안, IT |
| 미술 | `art.csv` | 뉴욕현대미술관(MoMA) 소장품 | 2,105 × 13 | 미술, 디자인, 건축, 사진, 미술사 |
| 관광·식품 | `tourism_food.csv` | 멕시코 관광도시 식당 평가 | 1,165 × 12 | 관광, 외식·조리, 식품, 서비스경영 |
| 행정 | `administration.csv` | 18개국 거버넌스 지표 | 489 × 7 | 행정, 공무원, 정책, 법·정치외교 |

수업 시간 예제용으로 `students_lesson.csv`(649 × 11, 결측 없음)가 따로 있습니다.

## 전처리 포인트와 분석 예시

| 파일 | 필요한 전처리 | 그룹별 분석 및 시각화 예시 |
|---|---|---|
| students.csv | 빈칸·이상 성적 처리, 도시/농촌 코드 정리, 성적 변화 열 생성 | 공부 구간별 성적 변화 막대 |
| biology.csv | 빈칸·이상 측정값 처리, 종명 정리, 꽃잎 길이/너비 비율 생성 | 종별 평균 비율 막대 |
| health.csv | `?`를 결측으로 변환, 이상값 처리, 연령구간 생성 | 연령구간별 평균 심박수 막대 |
| environment.csv | 빈칸·-999 같은 이상값 처리, 날짜 정리 | 월별 초미세먼지 선 |
| economy.csv | 물가 상승률 결측 처리, 부호별 범주 생성 | 국가별 상승률 막대·연도별 선 |
| retail.csv | 빈칸·음수 단가·잘못된 날짜 처리, 취소 주문 확인, 명세금액 생성 | 국가별 평균금액 막대·월별 선 |
| movies.csv | 평가 결측·범위 밖 평점 처리, 장르 분리, 연도 추출 | 장르별 평점 막대 |
| sports.csv | 빈칸·음수 기록 처리, 우승 여부 결측의 의미 확인, 승률 생성 | 리그별 경기당 홈런 막대·팀 승률 선 |
| engineering.csv | 긴 열 이름 정리, 빈칸·중복 행·이상값 처리, 물-시멘트비 생성 | 재령별 평균 압축강도 막대 |
| computer.csv | 무응답·중복 응답·범위 밖 값 처리, 연봉 극단값 확인, `;` 언어 목록 분리 | AI 도구 사용 빈도별 만족도 막대 |
| art.csv | 괄호·`()`·`(0)` 정리, 제작연도 추출, 잘못된 날짜·치수 처리 | 분류별 작가 성별 비율 막대·소장 연도별 선 |
| tourism_food.csv | `?`를 결측으로 변환, 도시 철자 통일, 중복 평가 처리, 요리 종류 분리 | 요리 종류별 음식 평가 막대 |
| administration.csv | 결측과 빠진 연도 확인, 범위 밖 점수·중복 행 처리 | 국가별 정부효과성 막대·연도별 선 |

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
data/       CSV 14개 (수업용 1, 프로젝트용 13), UTF-8 BOM
guides/     파일별 안내: 원자료, 준비 기준, 열 설명, 수업용 가공, 배포 조건
licenses/   데이터별 이용조건과 원 제공자 README·고지문
```

## 수업용 가공 안내

전처리 연습을 위해 대부분의 파일에 원자료에 없던 **빈칸**, **있을 수 없는 값**(음수 나이, 범위 밖 점수, -999, `not_a_date` 등), 일부 파일에는 **중복 행**을 넣었습니다. 열별 개수는 각 guides 파일의 "수업용 가공"에 적었습니다. 원자료의 실제 결측과 수업용으로 만든 값을 구분해 두었으니, 분석 결과를 원자료의 사실로 인용하지 마세요.

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

- CC BY 4.0: https://creativecommons.org/licenses/by/4.0/
- CC BY-SA 3.0: https://creativecommons.org/licenses/by-sa/3.0/
- ODbL 1.0: https://opendatacommons.org/licenses/odbl/1-0/
- CC0 1.0: https://creativecommons.org/publicdomain/zero/1.0/

저장소 전체에 하나의 데이터 라이선스를 적용하지 않습니다. 파일마다 원출처·가공 사실·각 이용조건을 유지하며, 원 제공자가 이 가공본이나 수업을 보증하거나 추천하지 않습니다. 자료 확인·수업용 준비일: 2026-10-11 (공학·컴퓨터·미술·관광식품·행정 2026-10-24).
