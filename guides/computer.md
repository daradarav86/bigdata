# computer.csv — 프로젝트용

관심 진로: 컴퓨터공학, 소프트웨어 개발, 인공지능, 정보보안, IT 산업

가공본 470행 × 17열. 이 파일은 분석·시각화 전 학생이 전처리하는 자료입니다.

## 원자료 및 준비 기준
Stack Overflow Annual Developer Survey 2025 (results.csv, 응답 49,191건). Retrieved 2026-10-24.

https://survey.stackoverflow.co/ · https://github.com/StackExchange/Survey/tree/main/packages/archive/2025

원 172열 중 필요한 열을 골라 응답 1,000건을 고정 난수42로 무작위 추출한 표본에서, 연간 총보수가 1,000달러 이상으로 적힌 470건만 남겼습니다(연봉이 비었거나 극단적으로 낮은 응답이 많아 `dropna()`로 행의 3분의 2가 사라지던 것을 줄이려고). 긴 영어 문장이던 응답 값은 짧은 영어 단어로 바꿨고, 한 칸에 여러 답이 `;`로 이어져 그대로 쓸 수 없던 사용 언어 목록은 `language_count`(개수)와 `uses_python`(Python 사용 여부)으로 바꿨습니다.

## 열 설명
| 열 | 뜻·단위 |
|---|---|
| `response_id` | 원자료 응답 번호 |
| `role_type` | 응답자 유형: developer(직업 개발자) / sometimes_codes(직업은 개발자가 아니지만 일·공부로 코딩) / other. 응답이 15명 미만인 유형은 other |
| `age_group` | 나이 구간 18-24 / 25-34 / 35-44 / 45-54 / 55+. 답하지 않은 응답은 빈칸 |
| `education` | 최종 학력: bachelor / master / some_college / doctorate_professional / high_school / associate |
| `years_coding` | 교육 포함 코딩 경력, 년 |
| `work_years` | 직업 경력, 년 |
| `career_stage` | 경력 단계(가공 열): 1_under_5y / 2_5_9y / 3_10_19y / 4_20y_plus |
| `job_type` | 직무: full_stack / back_end / front_end / other_developer / architect / other |
| `company_size` | 회사 규모(직원 수): 1_solo(혼자) / 2_1-19 / 3_20-99 / 4_100-499 / 5_500-999 / 6_1000-4999 / 7_5000-9999 / 8_10000+. 앞의 번호가 작은 순서 |
| `work_style` | 근무 형태: remote / hybrid_mostly_office / hybrid_flexible / in_person / free_choice |
| `country` | 거주 국가 (긴 이름은 United States, United Kingdom 등으로 줄임) |
| `country_group` | 국가 묶음(가공 열): 응답이 20명 이상인 5개 나라(United States, Germany, United Kingdom, France, Canada)와 Other |
| `salary_usd` | 연간 총보수, 미국 달러로 환산, 1,000달러 이상만. 극단값 존재 |
| `ai_use` | 개발에 AI 도구를 쓰는 빈도: daily / weekly / monthly_or_less / plan_to_use / no_plan |
| `job_satisfaction` | 직무 만족도 0~10 |
| `language_count` | 지난 1년간 써 본 프로그래밍 언어의 개수 |
| `uses_python` | Python 사용 여부 yes/no |

## 수업용 가공
**2026-11-07에 학생이 분석하기 쉽게 다시 정리했습니다.**

- 열 이름은 영어 소문자와 밑줄(`_`)로 짧게 바꿨습니다(아래 대응표). 열 이름에 공백·괄호·단위가 없어서 `df["열이름"]`으로 그대로 쓸 수 있습니다.
- 표본이 470명이라 그룹이 작으면(예: `company_size`의 1_solo 11명) 평균이 흔들립니다. 그룹 크기를 함께 확인하세요.
- 연봉(`salary_usd`)은 극단값이 있어 평균과 중앙값이 많이 다릅니다. 두 통계를 비교해 보세요.
- `job_satisfaction`의 빈칸이 약 19%로 가장 많습니다. `dropna()`로 지울 때와 `fillna()`로 채울 때 결과가 어떻게 달라지는지 비교해 볼 수 있습니다.
- `career_stage`로 경력에 따른 연봉 변화를 볼 수 있습니다. 경력이 빈칸이면 단계도 빈칸입니다.
- 빈칸(결측값): `age_group` 4개, `education` 4개, `years_coding` 4개, `work_years` 11개, `career_stage` 11개, `company_size` 49개, `work_style` 45개, `ai_use` 8개, `job_satisfaction` 89개, `language_count` 28개, `uses_python` 28개.
- `df.dropna()`를 하면 빈칸이 하나라도 있는 행이 사라져 전체의 약 34%가 줄어듭니다.
- 있을 수 없는 값(음수 나이, 범위 밖 점수, -999 등)은 모두 빈칸으로 바꿨으므로 **현재 파일에는 결측치(빈칸) 외의 이상값이 없습니다.** 전처리는 `isnull().sum()` → `dropna()`/`fillna()`로 끝납니다.

빈칸은 원자료의 무응답(설문에 답하지 않음)이고, `age_group`의 "답하지 않음"과 `company_size`의 "모름"도 빈칸으로 바꿨습니다.

열 이름 대응표(예전 → 새):

| 예전 열 이름 | 새 열 이름 |
|---|---|
| ResponseId | `response_id` |
| MainBranch | `role_type` |
| Age | `age_group` |
| EdLevel | `education` |
| YearsCode | `years_coding` |
| WorkExp | `work_years` |
| DevType | `job_type` |
| OrgSize | `company_size` |
| RemoteWork | `work_style` |
| Country | country (+ country_group) |
| ConvertedCompYearly | `salary_usd` |
| AISelect | `ai_use` |
| JobSat | `job_satisfaction` |
| LanguageHaveWorkedWith | `language_count`, uses_python (목록 열은 뺌) |

## 분석 아이디어
학생들이 고를 수 있는 주제 예시입니다. 모두 이 파일로 계산해서 결과가 나오는 것을 확인했습니다(그룹마다 행이 충분하고 값이 서로 다릅니다). **그대로 베끼지 말고 우리 팀의 진로에 맞게 질문을 바꿔 쓰세요.** 결과가 "차이가 거의 없음"으로 나와도 괜찮습니다. 그것도 분석 결과이고, 왜 그런지 생각해 볼 수 있습니다. 이 질문들은 사이트의 [기획] 탭에서도 눌러서 시작할 수 있습니다.

| 질문 | 묶는 기준 | 계산할 열 | 통계 | 그래프 | 새 열 만들기 |
|---|---|---|---|---|---|
| AI 도구 사용 빈도(ai_use)별 연봉(salary_usd)의 중앙값은 어떻게 다를까? | `ai_use` | `salary_usd` | 중앙값 | 막대 | — |
| Python을 쓰는 개발자와 안 쓰는 개발자(uses_python)의 연봉(salary_usd) 중앙값은 어떻게 다를까? | `uses_python` | `salary_usd` | 중앙값 | 막대 | — |
| 경력 단계(career_stage)에 따라 평균 연봉(salary_usd)은 어떻게 변할까? | `career_stage` | `salary_usd` | 평균 | 선 | — |
| 회사 규모(company_size)별 연봉(salary_usd) 중앙값은 어떻게 다를까? | `company_size` | `salary_usd` | 중앙값 | 막대 | — |
| 근무 형태(work_style)별 직무 만족도(job_satisfaction) 평균은 어떻게 다를까? | `work_style` | `job_satisfaction` | 평균 | 막대 | — |
| 국가(country_group)별 연봉(salary_usd) 중앙값은 어떻게 다를까? | `country_group` | `salary_usd` | 중앙값 | 막대 | — |
| 직무(job_type)별 월 소득(salary_usd / 12) 평균은 어떻게 다를까? | `job_type` | `salary_usd / 12` | 평균 | 막대 | `df["monthly"] = df["salary_usd"] / 12` |

이 데이터를 쓸 때 알아 둘 것:

- 응답자 470명이라 그룹이 작으면(혼자 일하는 사람 11명) 평균이 흔들려요.
- 연봉은 극단값이 있어 평균과 중앙값이 많이 달라요. 두 통계를 비교해 보세요. job_satisfaction은 결측이 19%예요.

## 공개 배포 조건
Survey data licensed under ODbL 1.0 https://opendatacommons.org/licenses/odbl/1-0/, contents under DbCL 1.0 https://opendatacommons.org/licenses/dbcl/1-0/. computer.csv 가공본도 ODbL 1.0으로 배포합니다(동일조건). 출처·가공 사실·원조건을 함께 표시하세요. 원자료에서 바꾼 내용은 이 안내의 "원자료 및 준비 기준"과 "수업용 가공"에 적었습니다. 제공자가 이 가공본을 보증하거나 추천하지 않습니다.
