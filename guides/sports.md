# sports.csv — 프로젝트용

관심 진로: 체육, 스포츠경영, 스포츠 통계, 데이터 분석

가공본 1,028행 × 13열. 이 파일은 분석·시각화 전 학생이 전처리하는 자료입니다.

## 원자료 및 준비 기준
Sean Lahman / SABR, Lahman Baseball Database, Teams table; CSV retrieved via Rdatasets. https://sabr.org/lahman-database/

https://sabr.org/lahman-database/

1990~2024년 AL/NL 팀·시즌 1,028건 전체입니다. 원 열 이름은 야구 기록 약어(`G`, `W`, `L`, `R`, `RA`, `HR`)라서 뜻이 보이는 이름으로 바꾸고, 시즌을 10년 단위로 묶은 `decade` 열을 더했습니다. 1994년 월드시리즈 미개최에 따른 `world_series_win` 결측은 유지했습니다. 승률·경기당 홈런은 미리 계산하지 않았습니다.

## 열 설명
| 열 | 뜻·단위 |
|---|---|
| `year` | 시즌 연도 1990~2024 |
| `decade` | 시즌의 10년 단위(가공 열): 1990s / 2000s / 2010s / 2020s |
| `team_id` | 팀 코드 |
| `team_name` | 팀 이름 |
| `league` | 리그 AL(아메리칸)/NL(내셔널) |
| `games` | 경기 수 |
| `wins` | 승 |
| `losses` | 패 |
| `winning_season` | 승리 시즌 여부(가공 열): 승이 패보다 많으면 yes, 아니면 no |
| `runs_scored` | 득점 |
| `runs_allowed` | 실점 |
| `home_runs` | 홈런 |
| `world_series_win` | 월드시리즈 우승 Y/N, 빈칸은 결측 |

## 수업용 가공
**2026-11-07에 학생이 분석하기 쉽게 다시 정리했습니다.**

- 열 이름은 영어 소문자와 밑줄(`_`)로 짧게 바꿨습니다(아래 대응표). 열 이름에 공백·괄호·단위가 없어서 `df["열이름"]`으로 그대로 쓸 수 있습니다.
- 1994·1995년과 2020년은 경기 수가 적은 시즌(58~145경기)입니다. 시즌끼리 승·홈런을 비교할 때는 `games`를 함께 보거나 승률(`wins / games`)로 바꿔 보세요.
- 승률은 리그 전체 평균이 늘 약 0.5라서 `decade`·`league`로 묶으면 차이가 없습니다. `world_series_win`(우승 여부)처럼 팀 성적과 관련 있는 기준으로 묶어 비교하세요.
- `winning_season`은 승이 패보다 많은 시즌이 yes입니다. 승·패가 같은 시즌(20개)은 no입니다.
- 빈칸(결측값): `games` 4개, `wins` 10개, `winning_season` 10개, `runs_scored` 7개, `home_runs` 10개, `world_series_win` 28개.
- `df.dropna()`를 하면 빈칸이 하나라도 있는 행이 사라져 전체의 약 6%가 줄어듭니다.
- 있을 수 없는 값(음수 나이, 범위 밖 점수, -999 등)은 모두 빈칸으로 바꿨으므로 **현재 파일에는 결측치(빈칸) 외의 이상값이 없습니다.** 전처리는 `isnull().sum()` → `dropna()`/`fillna()`로 끝납니다.

`world_series_win`의 빈칸 28개는 1994년 월드시리즈 미개최에 따른 원자료의 결측입니다. 2020년 팀별 58~60경기는 단축 시즌의 원자료 값입니다.

열 이름 대응표(예전 → 새):

| 예전 열 이름 | 새 열 이름 |
|---|---|
| yearID | `year` |
| teamID | `team_id` |
| name | `team_name` |
| lgID | `league` |
| G | `games` |
| W | `wins` |
| L | `losses` |
| R | `runs_scored` |
| RA | `runs_allowed` |
| HR | `home_runs` |
| WSWin | `world_series_win` |

## 분석 아이디어
학생들이 고를 수 있는 주제 예시입니다. 모두 이 파일로 계산해서 결과가 나오는 것을 확인했습니다(그룹마다 행이 충분하고 값이 서로 다릅니다). **그대로 베끼지 말고 우리 팀의 진로에 맞게 질문을 바꿔 쓰세요.** 결과가 "차이가 거의 없음"으로 나와도 괜찮습니다. 그것도 분석 결과이고, 왜 그런지 생각해 볼 수 있습니다. 이 질문들은 사이트의 [기획] 탭에서도 눌러서 시작할 수 있습니다.

| 질문 | 묶는 기준 | 계산할 열 | 통계 | 그래프 | 새 열 만들기 |
|---|---|---|---|---|---|
| 연대(decade)별 팀의 평균 홈런(home_runs)은 어떻게 다를까? | `decade` | `home_runs` | 평균 | 막대 | — |
| 아메리칸 리그와 내셔널 리그(league)의 평균 홈런(home_runs)은 어떻게 다를까? | `league` | `home_runs` | 평균 | 막대 | — |
| 승리 시즌(winning_season)을 보낸 팀과 아닌 팀의 평균 득점(runs_scored)은 어떻게 다를까? | `winning_season` | `runs_scored` | 평균 | 막대 | — |
| 월드시리즈 우승 여부(world_series_win)별 정규 시즌 평균 승(wins)은 어떻게 다를까? | `world_series_win` | `wins` | 평균 | 막대 | — |
| 시즌(year)에 따라 팀 평균 홈런(home_runs)은 어떻게 변할까? | `year` | `home_runs` | 평균 | 선 | — |
| 승리 시즌(winning_season) 여부별 득실차(runs_scored - runs_allowed) 평균은 어떻게 다를까? | `winning_season` | `runs_scored - runs_allowed` | 평균 | 막대 | `df["run_diff"] = df["runs_scored"] - df["runs_allowed"]` |

이 데이터를 쓸 때 알아 둘 것:

- 1994·1995·2020년은 경기 수가 적은 시즌이라 승·홈런 합계는 games와 함께 봐요.
- 승률은 리그 평균이 늘 0.5 근처라 decade·league로 묶으면 차이가 없어요. 우승 여부나 승리 시즌으로 비교해요.

## 공개 배포 조건
원 데이터 CC BY-SA 3.0; sports.csv 가공본도 CC BY-SA 3.0 https://creativecommons.org/licenses/by-sa/3.0/. 출처·가공 사실·원조건을 함께 표시하세요. 원자료에서 바꾼 내용은 이 안내의 "원자료 및 준비 기준"과 "수업용 가공"에 적었습니다. 제공자가 이 가공본을 보증하거나 추천하지 않습니다.
