# retail.csv — 프로젝트용

관심 진로: 유통, 경영, 마케팅, 회계, 전자상거래, 물류

가공본 6,103행 × 7열. 이 파일은 분석·시각화 전 학생이 전처리하는 자료입니다.

## 원자료 및 준비 기준
Chen, D. (2015). Online Retail. UCI. https://doi.org/10.24432/C5BW33

https://archive.ics.uci.edu/dataset/352/online+retail

2011년 1~11월, 국가×월×거래상태(취소/기타/설명결측)별 최대20개 거래명세를 고정 난수42로 추출. 취소·음수·0단가·설명 결측 유지. 고객 ID 제외. 국가·월 집계 전 원명세 형태.

## 열 설명
| 열 | 뜻·단위 |
|---|---|
| `InvoiceNo` | 주문번호, C로 시작하면 취소 |
| `StockCode` | 상품코드 |
| `Description` | 상품설명, 빈칸 존재 |
| `Quantity` | 명세수량, 음수는 취소/반품 등이므로 확인 |
| `InvoiceDate` | 거래시각 문자열 |
| `UnitPrice` | 단가GBP |
| `Country` | 고객 거주국가 |

## 수업용 가공
전처리 연습을 위해 원자료에 없던 빈칸을 넣었습니다: `Quantity` 61개, `UnitPrice` 61개. `Description`의 빈칸은 원자료의 결측입니다.

## 공개 배포 조건
CC BY 4.0 https://creativecommons.org/licenses/by/4.0/. 출처·가공 사실·원조건을 함께 표시하세요. 원자료에서 바꾼 내용은 이 안내의 "원자료 및 준비 기준"과 "수업용 가공"에 적었습니다. 제공자가 이 가공본을 보증하거나 추천하지 않습니다.
