# tourism_food.csv — 프로젝트용

관심 진로: 관광, 외식·조리, 식품, 호텔·서비스경영, 소비자 분석

가공본 1,161행 × 12열. 이 파일은 분석·시각화 전 학생이 전처리하는 자료입니다.

## 원자료 및 준비 기준
Ponce Medellín, R. & González Serna, J. G. (2011). Restaurant & consumer data. UCI. https://doi.org/10.24432/C5DP41 (기증: Vargas-Govea, B. & González Serna, J. G.)

https://archive.ics.uci.edu/dataset/232/restaurant+consumer+data

멕시코 산루이스포토시·쿠에르나바카·시우다드빅토리아 지역 식당 130곳에 대한 소비자 138명의 평가 1,161건 전체입니다(rating_final.csv에 식당 정보 geoplaces2.csv, 요리 종류 chefmozcuisine.csv, 고객 예산 userprofile.csv를 교사가 미리 병합). 학생이 읽기 쉽게 열 이름과 값을 정리했습니다: 요리 종류는 `;`로 이어 붙은 여러 값 중 첫 번째만 쓰고, 요리 정보가 없는 식당은 `unknown`으로 적었습니다.

## 열 설명
| 열 | 뜻·단위 |
|---|---|
| `user_id` | 평가한 소비자 번호 |
| `user_budget` | 소비자 예산 1_low / 2_medium / 3_high, 빈칸은 원자료 결측 |
| `place_id` | 식당 번호 |
| `place_name` | 식당 이름 |
| `city` | 도시(San Luis Potosi, Cuernavaca, Ciudad Victoria). 평가가 30건 미만인 도시(Jiutepec, Soledad)는 Other, 빈칸은 원자료 결측 |
| `cuisine` | 요리 종류(Mexican, Bar, Fast_Food 등). 식당에 여러 종류가 있으면 첫 번째만 쓰고, 평가가 30건 미만인 종류는 other, 요리 정보가 없는 식당은 unknown |
| `price_level` | 식당 가격대 1_low / 2_medium / 3_high |
| `alcohol_service` | 주류 판매 No_Alcohol_Served / Wine-Beer / Full_Bar |
| `smoking_policy` | 흡연 구역: no_area(흡연 구역 없음) / section / not permitted / permitted / only at bar |
| `overall_rating` | 전체 평가 0/1/2 |
| `food_rating` | 음식 평가 0/1/2 |
| `service_rating` | 서비스 평가 0/1/2 |

## 수업용 가공
**2026-11-07에 학생이 분석하기 쉽게 다시 정리했습니다.**

- 열 이름은 영어 소문자와 밑줄(`_`)로 짧게 바꿨습니다(아래 대응표). 열 이름에 공백·괄호·단위가 없어서 `df["열이름"]`으로 그대로 쓸 수 있습니다.
- `smoking_policy`의 `no_area`는 "흡연 구역이 없다"는 값이지 결측이 아닙니다(원자료 표기 `none`을 바꿨습니다).
- `overall_rating`, `food_rating`, `service_rating`은 0·1·2 세 값뿐이라 평균이 0~2 사이에서 나옵니다. `(food_rating + service_rating) / 2` 같은 새 열을 만들어 볼 수 있습니다.
- 앞에 번호가 붙은 `1_low`, `2_medium`, `3_high`는 그래프에서 낮음 → 높음 순서로 나오게 한 것입니다.
- 빈칸(결측값): `user_budget` 69개, `city` 114개, `overall_rating` 5개, `food_rating` 6개, `service_rating` 6개.
- `df.dropna()`를 하면 빈칸이 하나라도 있는 행이 사라져 전체의 약 17%가 줄어듭니다.
- 있을 수 없는 값(음수 나이, 범위 밖 점수, -999 등)은 모두 빈칸으로 바꿨으므로 **현재 파일에는 결측치(빈칸) 외의 이상값이 없습니다.** 전처리는 `isnull().sum()` → `dropna()`/`fillna()`로 끝납니다.

`city`, `user_budget`의 빈칸은 원자료의 결측입니다(원자료의 `?`는 빈칸으로 바꿨습니다). 같은 도시가 여러 철자로 적혀 있던 189행은 도시명으로 통일했습니다.

열 이름 대응표(예전 → 새):

| 예전 열 이름 | 새 열 이름 |
|---|---|
| userID | `user_id` |
| budget | `user_budget` |
| placeID | `place_id` |
| name | `place_name` |
| Rcuisine | `cuisine` |
| price | `price_level` |
| alcohol | `alcohol_service` |
| smoking_area | `smoking_policy` |
| rating | `overall_rating` |

## 분석 아이디어
학생들이 고를 수 있는 주제 예시입니다. 모두 이 파일로 계산해서 결과가 나오는 것을 확인했습니다(그룹마다 행이 충분하고 값이 서로 다릅니다). **그대로 베끼지 말고 우리 팀의 진로에 맞게 질문을 바꿔 쓰세요.** 결과가 "차이가 거의 없음"으로 나와도 괜찮습니다. 그것도 분석 결과이고, 왜 그런지 생각해 볼 수 있습니다. 이 질문들은 사이트의 [기획] 탭에서도 눌러서 시작할 수 있습니다.

| 질문 | 묶는 기준 | 계산할 열 | 통계 | 그래프 | 새 열 만들기 |
|---|---|---|---|---|---|
| 식당 가격대(price_level)별 평균 전체 평가(overall_rating)는 어떻게 다를까? | `price_level` | `overall_rating` | 평균 | 막대 | — |
| 요리 종류(cuisine)별 평균 전체 평가(overall_rating)는 어떻게 다를까? | `cuisine` | `overall_rating` | 평균 | 막대 | — |
| 주류 판매 방식(alcohol_service)별 평균 음식 평가(food_rating)는 어떻게 다를까? | `alcohol_service` | `food_rating` | 평균 | 막대 | — |
| 도시(city)별 평균 서비스 평가(service_rating)는 어떻게 다를까? | `city` | `service_rating` | 평균 | 막대 | — |
| 흡연 정책(smoking_policy)별 평균 전체 평가(overall_rating)는 어떻게 다를까? | `smoking_policy` | `overall_rating` | 평균 | 막대 | — |
| 손님의 예산(user_budget)별 평균 평가(overall_rating)는 어떻게 다를까? | `user_budget` | `overall_rating` | 평균 | 막대 | — |
| 가격대(price_level)별 음식·서비스 평가(food_rating + service_rating)의 평균은 어떻게 다를까? | `price_level` | `(food_rating + service_rating) / 2` | 평균 | 막대 | `df["avg_rating"] = (df["food_rating"] + df["service_rating"]) / 2` |

이 데이터를 쓸 때 알아 둘 것:

- 평가(overall_rating·food_rating·service_rating)는 0·1·2 세 값뿐이라 평균이 0~2 사이에서 나와요.
- smoking_policy의 no_area는 "흡연 구역이 없다"는 값이지 결측이 아니에요.

## 공개 배포 조건
CC BY 4.0 https://creativecommons.org/licenses/by/4.0/. 출처·가공 사실·원조건을 함께 표시하세요. 원자료에서 바꾼 내용은 이 안내의 "원자료 및 준비 기준"과 "수업용 가공"에 적었습니다. 제공자가 이 가공본을 보증하거나 추천하지 않습니다.
