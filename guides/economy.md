# economy.csv — 프로젝트용

관심 진로: 경제, 경영, 금융, 국제통상, 정책

가공본 165행 × 7열. 이 파일은 분석·시각화 전 학생이 전처리하는 자료입니다.

## 원자료 및 준비 기준
The World Bank: World Development Indicators: FP.CPI.TOTL.ZG. Original provider: International Monetary Fund, International Financial Statistics. Retrieved 2026-10-11.

https://databank.worldbank.org/metadataglossary/world-development-indicators/series/FP.CPI.TOTL.ZG

기존 10개 국가에 실제 결측이 있는 베네수엘라를 추가. 2010~2024년 11국가 165행. 실제 결측 8개 보존. 파생 상태열은 제공하지 않음. 2026-11-07에 `year`가 잘못 들어 있던 두 칸(프랑스 2024년이 0, 인도 2022년이 2099)을 바로잡았습니다. 국가 이름의 쉼표(`Korea, Rep.`, `Venezuela, RB`)를 없애 `South Korea`, `Venezuela`로 썼고, 시기(`period`)와 경제 유형(`economy_type`) 열을 더했습니다.

## 열 설명
| 열 | 뜻·단위 |
|---|---|
| `country` | 국가 영문명 |
| `country_code` | ISO3 코드 |
| `continent` | 대륙(가공 열): asia / europe / north_america / oceania / south_america |
| `year` | 2010~2024 |
| `period` | 시기(가공 열): 2010_2014 / 2015_2019 / 2020_2024 (코로나19 이후가 2020_2024) |
| `economy_type` | 경제 유형(가공 열): advanced(선진국: Australia, Canada, France, Germany, Japan, South Korea, United Kingdom, United States) / emerging(신흥국: China, India, Venezuela) |
| `inflation_rate` | 전년 대비 소비자물가 상승률 %, 빈칸은 결측(베네수엘라 8개는 원자료 결측, 3개는 수업용으로 비움) |

## 수업용 가공
**2026-11-07에 학생이 분석하기 쉽게 다시 정리했습니다.**

- 열 이름은 영어 소문자와 밑줄(`_`)로 짧게 바꿨습니다(아래 대응표). 열 이름에 공백·괄호·단위가 없어서 `df["열이름"]`으로 그대로 쓸 수 있습니다.
- 베네수엘라는 2016년 물가상승률이 254.9%이고 2017~2024년 8년은 원자료의 결측입니다. 평균이 크게 흔들리므로 평균과 중앙값을 함께 보고, `economy_type`으로 나누어 비교해 보세요.
- `dropna()`를 쓰면 베네수엘라의 절반 가까운 행이 사라집니다. 결측을 지우는 것과 두는 것의 차이를 설명할 수 있어야 합니다.
- `continent`, `economy_type`, `period`로 서로 다른 기준의 비교(지역·발전 단계·시기)를 해 볼 수 있습니다.
- 빈칸(결측값): `inflation_rate` 11개.
- `df.dropna()`를 하면 빈칸이 하나라도 있는 행이 사라져 전체의 약 7%가 줄어듭니다.
- 있을 수 없는 값(음수 나이, 범위 밖 점수, -999 등)은 모두 빈칸으로 바꿨으므로 **현재 파일에는 결측치(빈칸) 외의 이상값이 없습니다.** 전처리는 `isnull().sum()` → `dropna()`/`fillna()`로 끝납니다.

전처리 연습을 위해 원자료에 있던 값 3개를 비웠습니다: 캐나다 2021년, 인도 2012년, 대한민국 2010년의 `inflation_rate`. 베네수엘라 2017~2024년 8개는 원자료의 결측입니다.

열 이름 대응표(예전 → 새):

| 예전 열 이름 | 새 열 이름 |
|---|---|
| country (Korea, Rep. / Venezuela, RB) | country (South Korea / Venezuela) |

## 분석 아이디어
학생들이 고를 수 있는 주제 예시입니다. 모두 이 파일로 계산해서 결과가 나오는 것을 확인했습니다(그룹마다 행이 충분하고 값이 서로 다릅니다). **그대로 베끼지 말고 우리 팀의 진로에 맞게 질문을 바꿔 쓰세요.** 결과가 "차이가 거의 없음"으로 나와도 괜찮습니다. 그것도 분석 결과이고, 왜 그런지 생각해 볼 수 있습니다. 이 질문들은 사이트의 [기획] 탭에서도 눌러서 시작할 수 있습니다.

| 질문 | 묶는 기준 | 계산할 열 | 통계 | 그래프 | 새 열 만들기 |
|---|---|---|---|---|---|
| 국가(country)별 평균 물가상승률(inflation_rate)은 어떻게 다를까? | `country` | `inflation_rate` | 평균 | 막대 | — |
| 선진국과 신흥국(economy_type)의 물가상승률(inflation_rate) 평균은 어떻게 다를까? | `economy_type` | `inflation_rate` | 평균 | 막대 | — |
| 대륙(continent)별 물가상승률(inflation_rate)의 중앙값은 어떻게 다를까? | `continent` | `inflation_rate` | 중앙값 | 막대 | — |
| 코로나19 전후(period)로 물가상승률(inflation_rate) 평균은 어떻게 다를까? | `period` | `inflation_rate` | 평균 | 막대 | — |
| 연도(year)에 따라 물가상승률(inflation_rate) 평균은 어떻게 변할까? | `year` | `inflation_rate` | 평균 | 선 | — |
| 국가(country)별로 물가상승률(inflation_rate)과 물가 안정 목표(2%)의 차이는 평균 얼마일까? | `country` | `inflation_rate - 2` | 평균 | 막대 | `df["gap"] = df["inflation_rate"] - 2` |

이 데이터를 쓸 때 알아 둘 것:

- 베네수엘라는 2016년 물가상승률이 254.9%이고 2017~2024년이 결측이라 평균이 크게 흔들려요. 중앙값도 함께 봐요.
- 결측을 평균으로 채우면 베네수엘라 값이 크게 달라져요. 지우는 것과 채우는 것을 비교해 보세요.

## 공개 배포 조건
CC BY 4.0 + World Bank 추가 이용조건 https://data.worldbank.org/summary-terms-of-use. 출처·가공 사실·원조건을 함께 표시하세요. 원자료에서 바꾼 내용은 이 안내의 "원자료 및 준비 기준"과 "수업용 가공"에 적었습니다. 제공자가 이 가공본을 보증하거나 추천하지 않습니다.
