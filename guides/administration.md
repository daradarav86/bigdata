# administration.csv — 프로젝트용

관심 진로: 행정, 공무원, 정책, 법·정치외교, 공공기관

가공본 489행 × 7열. 이 파일은 분석·시각화 전 학생이 전처리하는 자료입니다.

## 원자료 및 준비 기준
Worldwide Governance Indicators, 2026 Update, World Bank (www.govindicators.org). Governance score (0-100): GOV_WGI_GE.SC, GOV_WGI_RQ.SC, GOV_WGI_RL.SC, GOV_WGI_CC.SC. Retrieved 2026-10-24 via World Bank API (source 3).

https://www.worldbank.org/en/publication/worldwide-governance-indicators

18개국 1996~2025년 27개 연도. 원자료에 1997·1999·2001년 값이 발표되지 않아 해당 연도 행이 없음. 실제 결측(남수단 독립 전, 코소보·몬테네그로 분리 전 등)을 보존. 점수를 소수 첫째 자리로 반올림. 4개 지표를 한 표로 합치고 열 이름을 영어 약칭으로 바꿈.

## 열 설명
| 열 | 뜻·단위 |
|---|---|
| `country` | 국가 영문명 |
| `country_code` | ISO3 코드 |
| `year` | 1996~2025 (1997·1999·2001 없음) |
| `gov_effectiveness` | 정부 효과성: 공공서비스·공무원 역량·정책 집행 품질, 0~100 |
| `regulatory_quality` | 규제 품질, 0~100 |
| `rule_of_law` | 법치, 0~100 |
| `control_of_corruption` | 부패 통제, 0~100 |

## 수업용 가공
전처리 연습을 위해 원자료를 다음과 같이 바꿨습니다.
- 빈칸: `gov_effectiveness` 5개, `rule_of_law` 5개
- 있을 수 없는 값: `control_of_corruption` -1 3개, `regulatory_quality` 999 3개(점수 범위 0~100 밖)
- 중복 행: 3행을 한 번 더 넣음

원자료 결측: `gov_effectiveness` 26, `regulatory_quality` 28, `rule_of_law` 15, `control_of_corruption` 14 (South Sudan, Kosovo, Montenegro).

## 공개 배포 조건
CC BY 4.0 https://creativecommons.org/licenses/by/4.0/ 및 World Bank 이용조건 https://www.worldbank.org/en/about/legal/terms-of-use-for-datasets. 출처·가공 사실·원조건을 함께 표시하세요. 원자료에서 바꾼 내용은 이 안내의 "원자료 및 준비 기준"과 "수업용 가공"에 적었습니다. 점수는 설문·전문가 인식 기반 추정치이며 World Bank는 신용평가·투자 판단 기준으로 쓰지 말 것을 권고합니다. 제공자가 이 가공본을 보증하거나 추천하지 않습니다.
