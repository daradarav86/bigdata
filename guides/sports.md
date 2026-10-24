# sports.csv — 프로젝트용

관심 진로: 체육, 스포츠경영, 스포츠 통계, 데이터 분석

가공본 1,028행 × 11열. 이 파일은 분석·시각화 전 학생이 전처리하는 자료입니다.

## 원자료 및 준비 기준
Sean Lahman / SABR, Lahman Baseball Database, Teams table; CSV retrieved via Rdatasets. https://sabr.org/lahman-database/

https://sabr.org/lahman-database/

1990~2024년 AL/NL 팀·시즌의 원열 이름 유지. 1994년 월드시리즈 미개최에 따른 WSWin 결측 유지. 승률·경기당 홈런을 미리 계산하지 않음.

## 열 설명
| 열 | 뜻·단위 |
|---|---|
| `yearID` | 시즌 연도 1990~2024 |
| `teamID` | 팀 코드 |
| `name` | 팀 이름 |
| `lgID` | 리그 AL(아메리칸)/NL(내셔널) |
| `G` | 경기 수 |
| `W` | 승 |
| `L` | 패 |
| `R` | 득점 |
| `RA` | 실점 |
| `HR` | 홈런 |
| `WSWin` | 월드시리즈 우승 Y/N, 빈칸은 결측 |

## 수업용 가공
전처리 연습을 위해 원자료를 다음과 같이 바꿨습니다.
- 빈칸: `W` 7개, `R` 7개, `HR` 7개
- 있을 수 없는 값: `G` -1 4개, `W` -10 3개, `HR` -5 3개

`WSWin`의 빈칸 28개는 1994년 월드시리즈 미개최에 따른 원자료의 결측입니다. 2020년 팀별 58~60경기는 단축 시즌에 따른 원자료 값입니다.

## 공개 배포 조건
원 데이터 CC BY-SA 3.0; sports.csv 가공본도 CC BY-SA 3.0 https://creativecommons.org/licenses/by-sa/3.0/. 출처·가공 사실·원조건을 함께 표시하세요. 원자료에서 바꾼 내용은 이 안내의 "원자료 및 준비 기준"과 "수업용 가공"에 적었습니다. 제공자가 이 가공본을 보증하거나 추천하지 않습니다.
