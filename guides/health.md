# health.csv — 프로젝트용

관심 진로: 보건, 간호, 의학, 의료정보, 공중보건

가공본 303행 × 12열. 이 파일은 분석·시각화 전 학생이 전처리하는 자료입니다.

## 원자료 및 준비 기준
Janosi, A., Steinbrunn, W., Pfisterer, M., & Detrano, R. (1989). Heart Disease. UCI. https://doi.org/10.24432/C52P4X

https://archive.ics.uci.edu/dataset/45/heart+disease

Cleveland 303건 전체입니다. 원 열 이름은 의학 약어(`cp`, `trestbps`, `thalach` 등)라서 뜻이 보이는 이름으로 바꿨고, 숫자 코드로 적혀 있던 범주(흉통 유형, 운동유발협심증)는 단어로 바꿨습니다. 학생이 구간을 직접 만들 필요가 없도록 `age_group`과 `disease` 열을 더했습니다. `ca`의 원 결측 기호 `?`는 빈칸으로 바꿨습니다.

## 열 설명
| 열 | 뜻·단위 |
|---|---|
| `age` | 나이(세) |
| `age_group` | 나이 구간(가공 열): 30s_or_younger / 40s / 50s / 60s / 70s_or_older |
| `chest_pain_type` | 흉통 유형: typical_angina(전형적 협심증) / atypical_angina(비전형적 협심증) / non_anginal(협심증이 아닌 흉통) / asymptomatic(무증상). 원 코드 1~4를 단어로 바꿈 |
| `resting_bp` | 입원 시 안정 혈압, mmHg |
| `bp_level` | 안정 혈압 수준(가공 열): 1_normal(120 미만) / 2_elevated(120~139) / 3_high(140 이상) |
| `cholesterol` | 혈청 콜레스테롤, mg/dL |
| `cholesterol_level` | 콜레스테롤 수준(가공 열): 1_normal(200 미만) / 2_elevated(200~239) / 3_high(240 이상) |
| `max_heart_rate` | 검사 중 최대 심박수, 회/분 |
| `exercise_angina` | 운동으로 생기는 협심증 yes/no (원 코드 1/0) |
| `vessels_colored` | 형광 투시로 색이 보인 주요 혈관 수 0~3, 빈칸은 원자료의 결측 |
| `disease_level` | 심장질환 진단 단계 0~4 (0은 없음, 1~4는 있음의 정도 코드) |
| `disease` | 심장질환 여부(가공 열): disease_level이 1 이상이면 yes, 0이면 no |

## 수업용 가공
**2026-11-07에 학생이 분석하기 쉽게 다시 정리했습니다.**

- 열 이름은 영어 소문자와 밑줄(`_`)로 짧게 바꿨습니다(아래 대응표). 열 이름에 공백·괄호·단위가 없어서 `df["열이름"]`으로 그대로 쓸 수 있습니다.
- `chest_pain_type`, `exercise_angina`, `disease`는 코드를 단어로 바꾼 열이라 평균을 내지 않고 **그룹을 나누는 데** 씁니다.
- 환자 수가 303명이라 작은 그룹(30대 이하 15명, 70대 이상 10명)의 평균은 흔들립니다. 그룹 크기도 함께 확인하세요.
- `bp_level`·`cholesterol_level`은 일반적인 의학 구분을 단순화한 구간입니다(구간 값은 위 열 설명 참고). 진단 단계(`disease_level`)와 함께 보면 "수치가 높을수록 위험한가"를 살펴볼 수 있습니다.
- 빈칸(결측값): `age` 1개, `age_group` 1개, `resting_bp` 2개, `bp_level` 2개, `cholesterol` 3개, `cholesterol_level` 3개, `max_heart_rate` 3개, `vessels_colored` 4개.
- `df.dropna()`를 하면 빈칸이 하나라도 있는 행이 사라져 전체의 약 4%가 줄어듭니다.
- 있을 수 없는 값(음수 나이, 범위 밖 점수, -999 등)은 모두 빈칸으로 바꿨으므로 **현재 파일에는 결측치(빈칸) 외의 이상값이 없습니다.** 전처리는 `isnull().sum()` → `dropna()`/`fillna()`로 끝납니다.

`vessels_colored`의 빈칸 4개는 원자료의 결측입니다.

열 이름 대응표(예전 → 새):

| 예전 열 이름 | 새 열 이름 |
|---|---|
| cp | `chest_pain_type` |
| trestbps | `resting_bp` |
| chol | `cholesterol` |
| thalach | `max_heart_rate` |
| exang | `exercise_angina` |
| ca | `vessels_colored` |
| num | `disease_level` |

## 분석 아이디어
학생들이 고를 수 있는 주제 예시입니다. 모두 이 파일로 계산해서 결과가 나오는 것을 확인했습니다(그룹마다 행이 충분하고 값이 서로 다릅니다). **그대로 베끼지 말고 우리 팀의 진로에 맞게 질문을 바꿔 쓰세요.** 결과가 "차이가 거의 없음"으로 나와도 괜찮습니다. 그것도 분석 결과이고, 왜 그런지 생각해 볼 수 있습니다. 이 질문들은 사이트의 [기획] 탭에서도 눌러서 시작할 수 있습니다.

| 질문 | 묶는 기준 | 계산할 열 | 통계 | 그래프 | 새 열 만들기 |
|---|---|---|---|---|---|
| 흉통 유형(chest_pain_type)별 최대 심박수(max_heart_rate) 평균은 어떻게 다를까? | `chest_pain_type` | `max_heart_rate` | 평균 | 막대 | — |
| 심장질환이 있는 사람과 없는 사람(disease)의 최대 심박수(max_heart_rate) 평균은 어떻게 다를까? | `disease` | `max_heart_rate` | 평균 | 막대 | — |
| 나이 구간(age_group)에 따라 콜레스테롤(cholesterol) 평균은 어떻게 변할까? | `age_group` | `cholesterol` | 평균 | 선 | — |
| 혈압 수준(bp_level)이 높을수록 진단 단계(disease_level) 평균이 높을까? | `bp_level` | `disease_level` | 평균 | 막대 | — |
| 콜레스테롤 수준(cholesterol_level)별 진단 단계(disease_level) 평균은 어떻게 다를까? | `cholesterol_level` | `disease_level` | 평균 | 막대 | — |
| 운동 중 협심증(exercise_angina) 여부별로 예상 최대 심박수 대비 비율(max_heart_rate)은 어떻게 다를까? | `exercise_angina` | `max_heart_rate / (220 - age)` | 평균 | 막대 | `df["hr_ratio"] = df["max_heart_rate"] / (220 - df["age"])` |

이 데이터를 쓸 때 알아 둘 것:

- 환자 303명의 기록이라 작은 그룹(30대 이하 15명, 70대 이상 10명)의 평균은 흔들려요.
- chest_pain_type·disease·bp_level 같은 열은 코드를 단어로 바꾼 것이라 평균이 아니라 그룹을 나누는 데 써요.

## 공개 배포 조건
CC BY 4.0 https://creativecommons.org/licenses/by/4.0/. 출처·가공 사실·원조건을 함께 표시하세요. 원자료에서 바꾼 내용은 이 안내의 "원자료 및 준비 기준"과 "수업용 가공"에 적었습니다. 제공자가 이 가공본을 보증하거나 추천하지 않습니다.
