# health.csv — 프로젝트용

관심 진로: 보건, 간호, 의학, 의료정보, 공중보건

가공본 303행 × 8열. 이 파일은 분석·시각화 전 학생이 전처리하는 자료입니다.

## 원자료 및 준비 기준
Janosi, A., Steinbrunn, W., Pfisterer, M., & Detrano, R. (1989). Heart Disease. UCI. https://doi.org/10.24432/C52P4X

https://archive.ics.uci.edu/dataset/45/heart+disease

Cleveland 303건의 원 열 이름·범주 코드 보존. ca의 원 결측 기호 ?를 CSV 문자열로 보존. 연령구간은 미리 만들지 않음.

## 열 설명
| 열 | 뜻·단위 |
|---|---|
| `age` | 나이(세) |
| `cp` | 흉통 코드1전형적/2비전형적/3비협심증/4무증상 |
| `trestbps` | 입원시 안정혈압mmHg |
| `chol` | 혈청콜레스테롤mg/dL |
| `thalach` | 검사 최대심박수회/분 |
| `exang` | 운동유발협심증1있음/0없음 |
| `ca` | 주요혈관수0~3, ?결측 |
| `num` | 원진단상태코드0~4;0과1~4를 구분하기도함 |

## 공개 배포 조건
CC BY 4.0 https://creativecommons.org/licenses/by/4.0/. 출처·가공 사실·원조건을 함께 표시하세요. 데이터의 오류를 인위적으로 추가하지 않았습니다.
