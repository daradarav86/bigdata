# administration.csv — 프로젝트용

관심 진로: 행정, 공무원, 정책, 법·정치외교, 공공기관

가공본 486행 × 9열. 이 파일은 분석·시각화 전 학생이 전처리하는 자료입니다.

## 원자료 및 준비 기준
Worldwide Governance Indicators, 2026 Update, World Bank (www.govindicators.org). Governance score (0-100): GOV_WGI_GE.SC, GOV_WGI_RQ.SC, GOV_WGI_RL.SC, GOV_WGI_CC.SC. Retrieved 2026-10-24 via World Bank API (source 3).

https://www.worldbank.org/en/publication/worldwide-governance-indicators

18개국 1996~2025년 27개 연도. 원자료에 1997·1999·2001년 값이 발표되지 않아 해당 연도 행이 없음. 실제 결측(남수단 독립 전, 코소보·몬테네그로 분리 전 등)을 보존. 점수를 소수 첫째 자리로 반올림. 4개 지표를 한 표로 합치고 열 이름을 영어 약칭으로 바꿈. 국가 이름의 쉼표(`Korea, Rep.`)를 없애 `South Korea`로, `Viet Nam`은 `Vietnam`으로 썼고, 대륙 묶음(`region`)과 시기(`period`) 열을 더했습니다.

## 열 설명
| 열 | 뜻·단위 |
|---|---|
| `country` | 국가 영문명 |
| `country_code` | ISO3 코드 |
| `region` | 대륙 묶음(가공 열): asia / europe / americas / africa |
| `year` | 1996~2025 (1997·1999·2001 없음) |
| `period` | 시기(가공 열): 1996_2005 / 2006_2015 / 2016_2025 |
| `gov_effectiveness` | 정부 효과성: 공공서비스·공무원 역량·정책 집행 품질, 0~100 |
| `regulatory_quality` | 규제 품질, 0~100 |
| `rule_of_law` | 법치, 0~100 |
| `control_of_corruption` | 부패 통제, 0~100 |

## 수업용 가공
**2026-11-07에 학생이 분석하기 쉽게 다시 정리했습니다.**

- 열 이름은 영어 소문자와 밑줄(`_`)로 짧게 바꿨습니다(아래 대응표). 열 이름에 공백·괄호·단위가 없어서 `df["열이름"]`으로 그대로 쓸 수 있습니다.
- 4개 지표는 모두 0~100 점수라서 평균 `(gov_effectiveness + regulatory_quality + rule_of_law + control_of_corruption) / 4` 같은 새 열을 만들 수 있습니다.
- 남수단(2011년 독립 전), 코소보·몬테네그로(분리 전) 등의 빈칸은 원자료의 실제 결측입니다.
- 빈칸(결측값): `gov_effectiveness` 31개, `regulatory_quality` 31개, `rule_of_law` 20개, `control_of_corruption` 17개.
- `df.dropna()`를 하면 빈칸이 하나라도 있는 행이 사라져 전체의 약 9%가 줄어듭니다.
- 있을 수 없는 값(음수 나이, 범위 밖 점수, -999 등)은 모두 빈칸으로 바꿨으므로 **현재 파일에는 결측치(빈칸) 외의 이상값이 없습니다.** 전처리는 `isnull().sum()` → `dropna()`/`fillna()`로 끝납니다.



열 이름 대응표(예전 → 새):

| 예전 열 이름 | 새 열 이름 |
|---|---|
| country (Korea, Rep. / Viet Nam) | country (South Korea / Vietnam) |

## 분석 아이디어
학생들이 고를 수 있는 주제 예시입니다. 모두 이 파일로 계산해서 결과가 나오는 것을 확인했습니다(그룹마다 행이 충분하고 값이 서로 다릅니다). **그대로 베끼지 말고 우리 팀의 진로에 맞게 질문을 바꿔 쓰세요.** 결과가 "차이가 거의 없음"으로 나와도 괜찮습니다. 그것도 분석 결과이고, 왜 그런지 생각해 볼 수 있습니다. 이 질문들은 사이트의 [기획] 탭에서도 눌러서 시작할 수 있습니다.

| 질문 | 묶는 기준 | 계산할 열 | 통계 | 그래프 | 새 열 만들기 |
|---|---|---|---|---|---|
| 대륙(region)별 정부 효과성(gov_effectiveness) 평균은 어떻게 다를까? | `region` | `gov_effectiveness` | 평균 | 막대 | — |
| 국가(country)별 법치(rule_of_law) 평균은 어떻게 다를까? | `country` | `rule_of_law` | 평균 | 막대 | — |
| 시기(period)별 부패 통제(control_of_corruption) 평균은 어떻게 다를까? | `period` | `control_of_corruption` | 평균 | 막대 | — |
| 연도(year)에 따라 규제 품질(regulatory_quality) 평균은 어떻게 변할까? | `year` | `regulatory_quality` | 평균 | 선 | — |
| 대륙(region)별 거버넌스 점수(gov_effectiveness 등 4개 지표의 평균)는 어떻게 다를까? | `region` | `(gov_effectiveness + regulatory_quality + rule_of_law + control_of_corruption) / 4` | 평균 | 막대 | `df["avg4"] = (df["gov_effectiveness"] + df["regulatory_quality"] + df["rule_of_law"] + df["control_of_corruption"]) / 4` |
| 대륙(region)별 부패 통제(control_of_corruption)의 중앙값은 어떻게 다를까? | `region` | `control_of_corruption` | 중앙값 | 막대 | — |

이 데이터를 쓸 때 알아 둘 것:

- 점수는 모두 0~100이라 네 지표를 합치거나 평균 내 보기 좋아요.
- 국가(country)는 18개라 막대가 빽빽해요. 대륙(region)이나 시기(period)로 묶어 보세요.

## 공개 배포 조건
CC BY 4.0 https://creativecommons.org/licenses/by/4.0/ 및 World Bank 이용조건 https://www.worldbank.org/en/about/legal/terms-of-use-for-datasets. 출처·가공 사실·원조건을 함께 표시하세요. 원자료에서 바꾼 내용은 이 안내의 "원자료 및 준비 기준"과 "수업용 가공"에 적었습니다. 점수는 설문·전문가 인식 기반 추정치이며 World Bank는 신용평가·투자 판단 기준으로 쓰지 말 것을 권고합니다. 제공자가 이 가공본을 보증하거나 추천하지 않습니다.
