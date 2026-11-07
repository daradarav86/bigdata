# students.csv — 프로젝트용

관심 진로: 교육, 상담, 심리, 사회복지

가공본 649행 × 15열. 이 파일은 분석·시각화 전 학생이 전처리하는 자료입니다.

## 원자료 및 준비 기준
Cortez, P. (2008). Student Performance. UCI. https://doi.org/10.24432/C5TG7T

https://archive.ics.uci.edu/dataset/320/student+performance

포르투갈어 649건의 원변수 15개. 수업용과 다른 열 이름·범주 표현, 세 학기 성적을 남김.

## 열 설명
| 열 | 뜻·단위 |
|---|---|
| `school` | 학교 코드 GP/MS |
| `age` | 나이(세) |
| `address` | 도시 U/농촌 R |
| `study_level` | 주간 공부 구간 1:<2시간, 2:2~5시간, 3:5~10시간, 4:>10시간 |
| `travel_level` | 통학 구간 1:<15분, 2:15~30분, 3:30분~1시간, 4:>1시간 |
| `school_support` | 추가 학교 교육지원 yes/no |
| `activities` | 교과 외 활동 yes/no |
| `internet` | 집 인터넷 yes/no |
| `higher_education` | 고등교육 진학 희망 yes/no |
| `freetime` | 자유시간 자기보고1~5 |
| `health` | 건강 자기보고1~5 |
| `absences` | 원자료 결석 횟수 |
| `score_1` | 첫 학기 성적0~20 |
| `score_2` | 두 번째 학기 성적0~20 |
| `final_score` | 마지막 학기 성적0~20 |

## 수업용 가공
전처리 연습을 위해 원자료를 다음과 같이 바꿨습니다.
- 빈칸: `absences` 4개, `G1` 5개, `G3` 4개
- 있을 수 없던 값(→ 모두 빈칸으로 바꿈): `age` -3 3개, `G3` -5 2개, `G3` 99 1개(성적 범위 0~20 밖)

**현재 파일에는 결측치(빈칸) 외의 이상값이 없습니다.** 범위 밖 값은 모두 빈칸으로 바꿨으므로 전처리는 `isnull().sum()` → `dropna()`/`fillna()`만으로 끝납니다. 아래 빈칸 개수에 바꾼 값이 더해져 실제 빈칸은 더 많습니다.

원자료(Student Performance)에는 결측이 없습니다.

**2026-11-07에 열 이름만 바꿨습니다**(값은 그대로). 수업용 `students_lesson.csv`와 같은 이름을 쓰도록 맞춘 것입니다. 나머지 열(`school`, `age`, `address`, `activities`, `internet`, `freetime`, `health`, `absences`)은 그대로입니다.

열 이름 대응표(예전 → 새):

| 예전 열 이름 | 새 열 이름 |
|---|---|
| studytime | `study_level` |
| traveltime | `travel_level` |
| schoolsup | `school_support` |
| higher | `higher_education` |
| G1 | `score_1` |
| G2 | `score_2` |
| G3 | `final_score` |

## 분석 아이디어
학생들이 고를 수 있는 주제 예시입니다. 모두 이 파일로 계산해서 결과가 나오는 것을 확인했습니다(그룹마다 행이 충분하고 값이 서로 다릅니다). **그대로 베끼지 말고 우리 팀의 진로에 맞게 질문을 바꿔 쓰세요.** 결과가 "차이가 거의 없음"으로 나와도 괜찮습니다. 그것도 분석 결과이고, 왜 그런지 생각해 볼 수 있습니다. 이 질문들은 사이트의 [기획] 탭에서도 눌러서 시작할 수 있습니다.

| 질문 | 묶는 기준 | 계산할 열 | 통계 | 그래프 | 새 열 만들기 |
|---|---|---|---|---|---|
| 공부 시간(study_level)이 길수록 최종 성적(final_score) 평균이 높을까? | `study_level` | `final_score` | 평균 | 막대 | — |
| 과외 활동(activities)을 하는 학생과 안 하는 학생의 최종 성적(final_score) 평균은 어떻게 다를까? | `activities` | `final_score` | 평균 | 막대 | — |
| 집에 인터넷(internet)이 있는 학생과 없는 학생의 결석(absences) 평균은 어떻게 다를까? | `internet` | `absences` | 평균 | 막대 | — |
| 대학 진학 희망(higher_education) 여부별로 성적 변화(final_score - score_1) 평균은 어떻게 다를까? | `higher_education` | `final_score - score_1` | 평균 | 막대 | `df["score_change"] = df["final_score"] - df["score_1"]` |
| 도시(U)와 농촌(R) 학생(address)의 통학 시간(travel_level) 평균은 어떻게 다를까? | `address` | `travel_level` | 평균 | 막대 | — |
| 자유 시간(freetime)에 따라 결석(absences) 평균은 어떻게 변할까? | `freetime` | `absences` | 평균 | 선 | — |
| 추가 학교 지원(school_support)을 받는 학생과 안 받는 학생의 최종 성적(final_score) 평균은 어떻게 다를까? | `school_support` | `final_score` | 평균 | 막대 | — |
| 건강 상태(health)가 좋을수록 결석(absences) 평균이 낮을까? | `health` | `absences` | 평균 | 막대 | — |

이 데이터를 쓸 때 알아 둘 것:

- 한 행은 포르투갈 두 학교의 학생 1명이에요.
- 성적(score_1·score_2·final_score)은 0~20점이고, 나이 20세 이상 학생은 수가 적어요.

## 공개 배포 조건
CC BY 4.0. 출처·가공 사실·원조건을 함께 표시하세요. 원자료에서 바꾼 내용은 이 안내의 "원자료 및 준비 기준"과 "수업용 가공"에 적었습니다. 제공자가 이 가공본을 보증하거나 추천하지 않습니다.
