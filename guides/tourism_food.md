# tourism_food.csv — 프로젝트용

관심 진로: 관광, 외식·조리, 식품, 호텔·서비스경영, 소비자 분석

가공본 1,161행 × 12열. 이 파일은 분석·시각화 전 학생이 전처리하는 자료입니다.

## 원자료 및 준비 기준
Ponce Medellín, R. & González Serna, J. G. (2011). Restaurant & consumer data. UCI. https://doi.org/10.24432/C5DP41 (기증: Vargas-Govea, B. & González Serna, J. G.)

https://archive.ics.uci.edu/dataset/232/restaurant+consumer+data

멕시코 산루이스포토시·쿠에르나바카·시우다드빅토리아 지역 식당 130곳에 대한 소비자 138명의 평가 1,161건 전체. rating_final.csv에 식당 정보(geoplaces2.csv), 요리 종류(chefmozcuisine.csv), 고객 예산(userprofile.csv)을 교사가 미리 병합. 한 식당의 요리 종류가 여러 개이면 `;`로 이어 붙임. 원 값과 철자를 유지하고 `?` 결측 기호를 그대로 둠.

## 열 설명
| 열 | 뜻·단위 |
|---|---|
| `userID` | 평가한 소비자 번호 |
| `budget` | 소비자 예산 low/medium/high, `?`는 원자료 결측 |
| `placeID` | 식당 번호 |
| `name` | 식당 이름 |
| `city` | 도시. 같은 도시가 여러 철자(san luis potosi, s.l.p., slp 등)로 적혀 있고 `?`는 원자료 결측 |
| `Rcuisine` | 요리 종류(Mexican, Fast_Food 등), `;` 구분. 빈칸은 원자료에 요리 정보가 없는 식당 |
| `price` | 식당 가격대 low/medium/high |
| `alcohol` | 주류 판매 No_Alcohol_Served/Wine-Beer/Full_Bar |
| `smoking_area` | 흡연 구역 |
| `rating` | 전체 평가 0/1/2 |
| `food_rating` | 음식 평가 0/1/2 |
| `service_rating` | 서비스 평가 0/1/2 |

## 수업용 가공
전처리 연습을 위해 원자료를 다음과 같이 바꿨습니다.
- 빈칸: `food_rating` 6개, `service_rating` 6개
- 있을 수 없는 값: `rating` 9 5개(평가 범위 0~2 밖)

`city`의 `?` 114행, `budget`의 `?` 69행, `Rcuisine` 빈칸 288행은 원자료의 결측입니다. pandas는 `?`를 결측으로 읽지 않으므로 직접 바꿔야 합니다.

## 공개 배포 조건
CC BY 4.0 https://creativecommons.org/licenses/by/4.0/. 출처·가공 사실·원조건을 함께 표시하세요. 원자료에서 바꾼 내용은 이 안내의 "원자료 및 준비 기준"과 "수업용 가공"에 적었습니다. 제공자가 이 가공본을 보증하거나 추천하지 않습니다.
