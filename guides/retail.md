# retail.csv — 프로젝트용

관심 진로: 유통, 경영, 마케팅, 회계, 전자상거래, 물류

가공본 4,812행 × 13열. 이 파일은 분석·시각화 전 학생이 전처리하는 자료입니다.

## 원자료 및 준비 기준
Chen, D. (2015). Online Retail. UCI. https://doi.org/10.24432/C5BW33

https://archive.ics.uci.edu/dataset/352/online+retail

2011년 1~11월, 국가×월×거래상태별 최대 20개 거래명세를 고정 난수42로 추출한 원자료 6,103건에서 **취소·반품**(주문번호가 C로 시작하거나 수량이 음수)과 **상품이 아닌 항목**(POST·M·S·D·DOT처럼 글자뿐인 상품코드: 배송비, 수동 입력 등), 완전히 같은 중복 행을 뺀 4,812건입니다. 단가가 0인 행은 단가를 빈칸으로 바꿨습니다. 고객 ID는 제외했습니다. 열 이름을 짧게 바꾸고, 학생이 날짜 문자열을 자를 필요가 없도록 `month` 열을, 37개 국가를 5개 지역으로 묶은 `region` 열을 더했습니다.

## 열 설명
| 열 | 뜻·단위 |
|---|---|
| `invoice_no` | 주문번호 |
| `stock_code` | 상품코드 |
| `product_name` | 상품 이름, 빈칸 존재 |
| `quantity` | 명세 수량(양수만) |
| `order_size` | 주문 규모(가공 열): 수량이 1_small(6개 미만) / 2_medium(6~12개) / 3_bulk(13개 이상) |
| `invoice_date` | 거래 시각 문자열 |
| `month` | 거래 월 1~11(가공 열). 날짜가 잘못 적힌 행은 빈칸 |
| `weekday` | 거래 요일(가공 열): 1_mon … 5_fri, 7_sun (토요일 거래는 없음) |
| `time_of_day` | 거래 시간대(가공 열): 1_morning(12시 전) / 2_afternoon(12~14시) / 3_evening(15시 이후) |
| `unit_price_gbp` | 단가, 영국 파운드(GBP). 단가가 0이던 행은 빈칸 |
| `price_level` | 가격 구간(가공 열): 1_cheap(1.25파운드 미만) / 2_mid(2.95 미만) / 3_pricey(2.95 이상) |
| `country` | 고객 거주 국가 (37개) |
| `region` | 지역 묶음(가공 열): uk / europe / asia_pacific / middle_east_africa / americas. 국가가 Unspecified이면 빈칸 |

## 수업용 가공
**2026-11-07에 학생이 분석하기 쉽게 다시 정리했습니다.**

- 열 이름은 영어 소문자와 밑줄(`_`)로 짧게 바꿨습니다(아래 대응표). 열 이름에 공백·괄호·단위가 없어서 `df["열이름"]`으로 그대로 쓸 수 있습니다.
- **취소·반품과 상품이 아닌 항목을 뺀 이유**: 이를 남기면 `quantity × unit_price_gbp`(명세 금액)의 평균이 국가에 따라 음수로 나오는 등 결과가 이상해지고, 수업에서 배우지 않은 필터링이 필요해집니다.
- 국가·월별로 비슷한 수를 뽑은 표본이라 **지역별·국가별 거래 수 비교는 의미가 없고** 평균 비교에 쓰세요. `country`는 37개라 막대가 빽빽합니다. `region`(5개)이나 `month`(11개)로 묶으면 읽기 좋습니다.
- `month`는 숫자 1~11이라 선그래프로 월별 변화를 그릴 수 있습니다.
- `weekday`, `time_of_day`, `price_level`, `order_size`로 "언제·얼마짜리를·얼마나 사는가"를 살펴볼 수 있습니다. 이 구간들은 표본에서 정한 기준이라 판매 전체의 비율은 아닙니다.
- 빈칸(결측값): `product_name` 98개, `quantity` 54개, `order_size` 54개, `invoice_date` 24개, `month` 24개, `weekday` 24개, `time_of_day` 24개, `unit_price_gbp` 176개, `price_level` 176개, `region` 125개.
- `df.dropna()`를 하면 빈칸이 하나라도 있는 행이 사라져 전체의 약 8%가 줄어듭니다.
- 있을 수 없는 값(음수 나이, 범위 밖 점수, -999 등)은 모두 빈칸으로 바꿨으므로 **현재 파일에는 결측치(빈칸) 외의 이상값이 없습니다.** 전처리는 `isnull().sum()` → `dropna()`/`fillna()`로 끝납니다.

빈칸: 원자료의 `Description` 빈칸과 수업용으로 넣은 빈칸, 단가 0을 비운 것이 섞여 있습니다.

열 이름 대응표(예전 → 새):

| 예전 열 이름 | 새 열 이름 |
|---|---|
| InvoiceNo | `invoice_no` |
| StockCode | `stock_code` |
| Description | `product_name` |
| Quantity | `quantity` |
| InvoiceDate | `invoice_date` |
| UnitPrice | `unit_price_gbp` |
| Country | `country` |

## 분석 아이디어
학생들이 고를 수 있는 주제 예시입니다. 모두 이 파일로 계산해서 결과가 나오는 것을 확인했습니다(그룹마다 행이 충분하고 값이 서로 다릅니다). **그대로 베끼지 말고 우리 팀의 진로에 맞게 질문을 바꿔 쓰세요.** 결과가 "차이가 거의 없음"으로 나와도 괜찮습니다. 그것도 분석 결과이고, 왜 그런지 생각해 볼 수 있습니다. 이 질문들은 사이트의 [기획] 탭에서도 눌러서 시작할 수 있습니다.

| 질문 | 묶는 기준 | 계산할 열 | 통계 | 그래프 | 새 열 만들기 |
|---|---|---|---|---|---|
| 어느 요일(weekday)에 한 건당 구매 금액(quantity × unit_price_gbp)이 가장 클까? | `weekday` | `quantity * unit_price_gbp` | 평균 | 막대 | `df["amount"] = df["quantity"] * df["unit_price_gbp"]` |
| 하루 중 시간대(time_of_day)별 평균 구매 수량(quantity)은 어떻게 다를까? | `time_of_day` | `quantity` | 평균 | 막대 | — |
| 월(month)에 따라 구매 금액(quantity × unit_price_gbp) 평균은 어떻게 변할까? | `month` | `quantity * unit_price_gbp` | 평균 | 선 | `df["amount"] = df["quantity"] * df["unit_price_gbp"]` |
| 상품 가격 구간(price_level)별로 한 번에 사는 수량(quantity) 평균은 어떻게 다를까? | `price_level` | `quantity` | 평균 | 막대 | — |
| 대량 주문(order_size)일수록 상품 단가(unit_price_gbp)가 낮을까? | `order_size` | `unit_price_gbp` | 평균 | 막대 | — |
| 지역(region)별 평균 단가(unit_price_gbp)는 어떻게 다를까? | `region` | `unit_price_gbp` | 평균 | 막대 | — |

이 데이터를 쓸 때 알아 둘 것:

- 국가·월별로 비슷한 수를 뽑은 표본이라 지역별 거래 수를 비교하는 건 의미가 없어요. 평균을 비교해요.
- 취소·반품과 배송비 같은 항목은 이미 뺐어요. 새 열 quantity × unit_price_gbp는 모두 양수예요.

## 공개 배포 조건
CC BY 4.0 https://creativecommons.org/licenses/by/4.0/. 출처·가공 사실·원조건을 함께 표시하세요. 원자료에서 바꾼 내용은 이 안내의 "원자료 및 준비 기준"과 "수업용 가공"에 적었습니다. 제공자가 이 가공본을 보증하거나 추천하지 않습니다.
