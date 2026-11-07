# biology.csv — 프로젝트용

관심 진로: 생명과학, 생태, 식물학, 농업, 생물정보, AI 분류

가공본 150행 × 6열. 이 파일은 분석·시각화 전 학생이 전처리하는 자료입니다.

## 원자료 및 준비 기준
Fisher, R. (1936). Iris. UCI. https://doi.org/10.24432/C56C76 (bezdekIris.data)

https://archive.ics.uci.edu/dataset/53/iris

150개 붓꽃 표본 원 종명 Iris- 접두어 유지. 파생 비율 미제공. 완전히 같은 측정값·종명 한 쌍도 별개 표본일 수 있어 삭제하지 않음.

## 열 설명
| 열 | 뜻·단위 |
|---|---|
| `sepal_length_cm` | 꽃받침길이cm |
| `sepal_width_cm` | 꽃받침너비cm |
| `petal_length_cm` | 꽃잎길이cm |
| `petal_width_cm` | 꽃잎너비cm |
| `species` | Iris-setosa/versicolor/virginica 종명 |
| `petal_size` | 꽃잎 길이 구간(가공 열): 1_short(3cm 미만) / 2_medium(3~4.9cm) / 3_long(5cm 이상) |


## 수업용 가공
전처리 연습을 위해 원자료를 다음과 같이 바꿨습니다.
- 빈칸: `sepal_length_cm` 2개, `petal_length_cm` 1개
- 있을 수 없던 값(→ 모두 빈칸으로 바꿈): `sepal_length_cm` -2.0 1개, `petal_width_cm` 0.0 1개

**현재 파일에는 결측치(빈칸) 외의 이상값이 없습니다.** 범위 밖 값은 모두 빈칸으로 바꿨으므로 전처리는 `isnull().sum()` → `dropna()`/`fillna()`만으로 끝납니다. 아래 빈칸 개수에 바꾼 값이 더해져 실제 빈칸은 더 많습니다.

원자료(Iris)에는 결측이 없습니다. 측정값·종명이 모두 같은 1쌍은 원자료에 있는 별개 표본입니다.

**2026-11-07에** 꽃잎 길이로 꽃을 나누어 비교할 수 있도록 `petal_size` 열을 더했습니다. 열 이름은 그대로입니다.

## 분석 아이디어
학생들이 고를 수 있는 주제 예시입니다. 모두 이 파일로 계산해서 결과가 나오는 것을 확인했습니다(그룹마다 행이 충분하고 값이 서로 다릅니다). **그대로 베끼지 말고 우리 팀의 진로에 맞게 질문을 바꿔 쓰세요.** 결과가 "차이가 거의 없음"으로 나와도 괜찮습니다. 그것도 분석 결과이고, 왜 그런지 생각해 볼 수 있습니다. 이 질문들은 사이트의 [기획] 탭에서도 눌러서 시작할 수 있습니다.

| 질문 | 묶는 기준 | 계산할 열 | 통계 | 그래프 | 새 열 만들기 |
|---|---|---|---|---|---|
| 붓꽃 종(species)별 꽃잎 길이(petal_length_cm) 평균은 어떻게 다를까? | `species` | `petal_length_cm` | 평균 | 막대 | — |
| 붓꽃 종(species)별 꽃받침 너비(sepal_width_cm)의 중앙값은 어떻게 다를까? | `species` | `sepal_width_cm` | 중앙값 | 막대 | — |
| 꽃잎 크기(petal_size)별로 꽃받침 길이(sepal_length_cm) 평균은 어떻게 다를까? | `petal_size` | `sepal_length_cm` | 평균 | 막대 | — |
| 붓꽃 종(species)별 꽃잎 길이(petal_length_cm)와 너비의 비율은 어떻게 다를까? | `species` | `petal_length_cm / petal_width_cm` | 평균 | 막대 | `df["petal_ratio"] = df["petal_length_cm"] / df["petal_width_cm"]` |
| 붓꽃 종(species)별 꽃받침 길이(sepal_length_cm) 평균은 어떻게 다를까? | `species` | `sepal_length_cm` | 평균 | 막대 | — |

이 데이터를 쓸 때 알아 둘 것:

- 붓꽃은 종마다 50송이씩이라 종 사이의 크기 차이가 아주 뚜렷해요.
- 꽃잎 크기 구간(petal_size)으로 나눠서 꽃받침과 비교해 볼 수도 있어요.

## 공개 배포 조건
CC BY 4.0 https://creativecommons.org/licenses/by/4.0/. 출처·가공 사실·원조건을 함께 표시하세요. 원자료에서 바꾼 내용은 이 안내의 "원자료 및 준비 기준"과 "수업용 가공"에 적었습니다. 제공자가 이 가공본을 보증하거나 추천하지 않습니다.
