# 원묵고 빅데이터 원리 탐구 진로별 데이터 프로젝트

| 용도/파일 | 행 수 | 필요한 전처리 | 그룹별 분석 및 시각화 예시 |
|---|---:|---|---|
| 수업: students_lesson.csv | 649 |수업용  | 공부 구간별 평균 성적 막대 |
| students.csv | 649 | 열 이름·도시/농촌 코드 정리, 성적 변화 열 생성 | 공부 구간별 성적 변화 막대 |
| movies.csv | 9,742 | 평가 결측·장르 미등록 처리, 장르 분리, 연도 추출 | 첫 장르 태그별 평점 막대 |
| environment.csv | 8,856 | 질문에 필요한 관측 결측 처리, 열 이름·날짜 정리 | 선정 월별 초미세먼지 선 |
| economy.csv | 165 | 물가 상승률 결측 처리, 부호별 범주 생성 | 국가별 상승률 막대·국가별 연도 선 |
| sports.csv | 1,028 | 우승 여부 결측의 의미 처리, 열 이름 정리, 승률·경기당 값 생성 | 리그별 경기당 홈런 막대·팀의 승률 선 |
| health.csv | 303 | ?를 숫자 결측으로 변환, 연령구간 생성 | 연령구간별 평균 심박수 막대 |
| biology.csv | 150 | 종명 정리, 동일 측정 표본 확인, 꽃잎 길이/너비 비율 생성 | 종별 평균 비율 막대 |
| retail.csv | 6,103 | 취소·음수·0단가 확인, 날짜 변환, 명세금액 생성 | 국가별 표본 명세 평균금액 막대·월별 선 |

## Colab 데이터 읽기

```python
import pandas as pd
url = 'https://raw.githubusercontent.com/daradarav86/bigdata/main/data/students_lesson.csv'
df = pd.read_csv(url)
```

프로젝트에서는 파일명을 students_project.csv, movies.csv 등으로 바꿉니다.

## 학생 안내와 공개 배포

- data/: CSV 9개(수업용1, 프로젝트용8)
- guides/: 데이터에 대한 상세 설명
- licenses/: 원 데이터 이용조건
- 일부 파일은 전처리 연습을 위해 원자료의 값 일부를 비웠습니다. 열별 내용은 guides의 "수업용 가공"을 읽으세요.

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

CC BY 4.0: https://creativecommons.org/licenses/by/4.0/
CC BY-SA 3.0: https://creativecommons.org/licenses/by-sa/3.0/

모든 파일에 하나의 MIT/CC0 데이터 라이선스를 적용하지 않습니다. 원출처·가공 사실·각 이용조건을 유지하고 제공자의 공식 추천을 암시하지 않습니다. CSV는 UTF-8 BOM입니다. 자료 확인·수업용 준비일 2026-10-11. 단위와 코드 설명은 guides를 읽으세요.
