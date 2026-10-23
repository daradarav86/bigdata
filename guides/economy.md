# economy.csv — 프로젝트용

관심 진로: 경제, 경영, 금융, 국제통상, 정책

가공본 165행 × 4열. 이 파일은 분석·시각화 전 학생이 전처리하는 자료입니다.

## 원자료 및 준비 기준
The World Bank: World Development Indicators: FP.CPI.TOTL.ZG. Original provider: International Monetary Fund, International Financial Statistics. Retrieved 2026-10-11.

https://databank.worldbank.org/metadataglossary/world-development-indicators/series/FP.CPI.TOTL.ZG

기존 10개 국가에 실제 결측이 있는 베네수엘라를 추가. 2010~2024년 11국가 165행. 실제 결측 8개 보존. 파생 상태열은 제공하지 않음.

## 열 설명
| 열 | 뜻·단위 |
|---|---|
| `country` | 국가 영문명 |
| `country_code` | ISO3 코드 |
| `year` | 2010~2024 |
| `inflation_rate` | 전년 대비 소비자물가 상승률%, 빈칸은 결측(베네수엘라 8개는 원자료 결측, 3개는 수업용으로 비움) |

## 수업용 가공
전처리 연습을 위해 원자료에 있던 값 3개를 비웠습니다: 캐나다 2021년, 인도 2012년, 대한민국 2010년의 `inflation_rate`. 베네수엘라 2017~2024년 8개는 원자료의 결측입니다.

## 공개 배포 조건
CC BY 4.0 + World Bank 추가 이용조건 https://data.worldbank.org/summary-terms-of-use. 출처·가공 사실·원조건을 함께 표시하세요. 원자료에서 바꾼 내용은 이 안내의 "원자료 및 준비 기준"과 "수업용 가공"에 적었습니다. 제공자가 이 가공본을 보증하거나 추천하지 않습니다.
