# biology.csv — 프로젝트용

관심 진로: 생명과학, 생태, 식물학, 농업, 생물정보, AI 분류

가공본 150행 × 5열. 이 파일은 분석·시각화 전 학생이 전처리하는 자료입니다.

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


## 수업용 가공
전처리 연습을 위해 원자료에 없던 빈칸을 넣었습니다: `sepal_length_cm` 2개, `petal_length_cm` 1개. 원자료(Iris)에는 결측이 없습니다.

## 공개 배포 조건
CC BY 4.0 https://creativecommons.org/licenses/by/4.0/. 출처·가공 사실·원조건을 함께 표시하세요. 원자료에서 바꾼 내용은 이 안내의 "원자료 및 준비 기준"과 "수업용 가공"에 적었습니다. 제공자가 이 가공본을 보증하거나 추천하지 않습니다.
