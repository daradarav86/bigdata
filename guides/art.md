# art.csv — 프로젝트용

관심 진로: 미술, 디자인, 건축, 사진, 미술사, 큐레이터

가공본 2,105행 × 13열. 이 파일은 분석·시각화 전 학생이 전처리하는 자료입니다.

## 원자료 및 준비 기준
The Museum of Modern Art (MoMA) Collection, Artworks.csv (160,920건). https://doi.org/10.5281/zenodo.23493633. Retrieved 2026-10-24 (commit 4566f41).

https://github.com/MuseumofModernArt/collection

7개 분류(Painting, Sculpture, Photograph, Print, Drawing, Design, Architecture)에서 분류별 300점을 고정 난수42로 무작위 추출해 ObjectID 순으로 정렬. 원 30열 중 13열을 원 열 이름 그대로 선택하고 URL·이미지 주소·세부 치수 열은 제외. 괄호 표기, 여러 작가가 이어 붙은 값, 연도 문자열(c. 1950, 1960–65 등)을 정리하지 않음. 작품 이미지는 포함하지 않음.

## 열 설명
| 열 | 뜻·단위 |
|---|---|
| `Title` | 작품 제목 |
| `Artist` | 작가명, 여러 명이면 `,`로 이어짐 |
| `Nationality` | 작가 국적, `(American)` 형태. `()`는 정보 없음 |
| `Gender` | 작가 성별, `(male)` 형태. `()`는 정보 없음, 여러 작가면 이어짐 |
| `BeginDate` | 작가 출생연도, `(1881)` 형태. `(0)`은 정보 없음 |
| `EndDate` | 작가 사망연도, `(0)`은 생존 또는 정보 없음 |
| `Date` | 작품 제작 시기 문자열 |
| `Medium` | 재료·기법 |
| `Classification` | 작품 분류 |
| `Department` | 소장 부서 |
| `DateAcquired` | 미술관 소장 날짜 YYYY-MM-DD |
| `Height (cm)` | 높이, cm |
| `Width (cm)` | 너비, cm |

## 수업용 가공
전처리 연습을 위해 원자료를 다음과 같이 바꿨습니다.
- 있을 수 없는 값: `Height (cm)` -1 5개, `Width (cm)` 0 5개
- 날짜가 아닌 값: `DateAcquired`의 `not_a_date` 5개
- 중복 행: 작품 5개를 한 번 더 넣음

빈칸과 `()`, `(0)` 표기는 원자료 그대로입니다. 표본 2,100점 기준 원자료 빈칸 수: `Title` 1, `Artist`·`Nationality`·`Gender`·`BeginDate`·`EndDate` 각 8, `Date` 15, `Medium` 23, `DateAcquired` 13, `Height (cm)` 201, `Width (cm)` 210. 선택한 13열이 모두 같은 50행은 같은 판화·사진의 서로 다른 소장품(에디션)이므로 원자료에서는 중복이 아닙니다.

## 공개 배포 조건
원 데이터 CC0 1.0 https://creativecommons.org/publicdomain/zero/1.0/. MoMA의 요청에 따라 출처(MoMA)와 DOI를 표시하고, 이 파일이 원자료를 수정한 가공본임을 밝힙니다. MoMA가 이 가공본이나 수업을 보증하지 않습니다. 원자료는 큐레이터 검증이 끝나지 않은 정보를 포함합니다. licenses/MoMA-collection-original-README.md 참고.
