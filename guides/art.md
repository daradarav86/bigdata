# art.csv — 프로젝트용

관심 진로: 미술, 디자인, 건축, 사진, 미술사, 큐레이터

가공본 1,037행 × 14열. 이 파일은 분석·시각화 전 학생이 전처리하는 자료입니다.

## 원자료 및 준비 기준
The Museum of Modern Art (MoMA) Collection, Artworks.csv (160,920건). https://doi.org/10.5281/zenodo.23493633. Retrieved 2026-10-24 (commit 4566f41).

https://github.com/MuseumofModernArt/collection

7개 분류(Painting, Sculpture, Photograph, Print, Drawing, Design, Architecture)에서 분류별 150점을 고정 난수42로 무작위 추출해 ObjectID 순으로 정렬한 표본에서, 완전히 같은 중복 행 13개를 뺀 1,037점입니다. 원자료의 괄호 표기(`(male)`, `(American)`), 여러 작가가 이어 붙은 값, 연도 문자열(`c. 1950`, `1960–65`)은 학생이 문자열 가공 없이 쓸 수 있도록 정리했고, 재료 설명(`Medium`, 쉼표로 이어진 재료 목록)과 뜻이 모호한 `EndDate`는 뺐습니다.

## 열 설명
| 열 | 뜻·단위 |
|---|---|
| `title` | 작품 제목 |
| `artist` | 작가명, 여러 명이면 `,`로 이어짐 |
| `nationality` | 작가 국적(예: American). 정보 없음은 빈칸, 작가가 여럿이고 국적이 다르면 `multiple` |
| `nationality_group` | 국적 묶음(가공 열): 작품이 많은 5개 국적(American, French, German, British, Italian)과 Other |
| `gender` | 작가 성별 male/female/mixed. 정보 없음은 빈칸, 작가가 여럿이고 성별이 섞이면 `mixed` |
| `birth_year` | 작가 출생연도. 작가가 여럿이고 출생연도가 다르면 빈칸 |
| `year_made` | 작품 제작 연도(`Date` 문자열에서 처음 나오는 4자리 연도). 알 수 없거나 "1900-1945"처럼 20년이 넘는 범위이면 빈칸 |
| `period_made` | 제작 시기 구간(가공 열): 1_before_1930 / 2_1930_1959 / 3_1960_1989 / 4_1990_plus |
| `classification` | 작품 분류 (Painting, Sculpture, Photograph, Print, Drawing, Design, Architecture) |
| `department` | 소장 부서. 작품이 30점 미만인 부서는 `Other` |
| `year_acquired` | 미술관이 소장한 연도 |
| `height_cm` | 높이, cm |
| `width_cm` | 너비, cm |
| `size_group` | 작품 크기 구간(가공 열): 면적(높이×너비)이 1_small(1,000cm² 미만) / 2_medium(5,000 미만) / 3_large(5,000 이상) |

## 수업용 가공
**2026-11-07에 학생이 분석하기 쉽게 다시 정리했습니다.**

- 열 이름은 영어 소문자와 밑줄(`_`)로 짧게 바꿨습니다(아래 대응표). 열 이름에 공백·괄호·단위가 없어서 `df["열이름"]`으로 그대로 쓸 수 있습니다.
- 원자료의 완전 중복 행 13개를 뺐습니다.
- `gender`: `(male)`·`(female)` 표기와 `(male) (male)` 같은 이어 붙은 값을 male / female / mixed로 정리했습니다. 정보 없음(`()`)은 빈칸입니다.
- `birth_year`, `year_made`, `year_acquired`는 숫자라서 "작가가 몇 살에 만들었나"(`year_made - birth_year`) 같은 새 열을 만들 수 있습니다.
- 분류별로 비슷한 수를 뽑은 표본이라 **작품 수 비교는 의미가 없고** 평균·중앙값 비교에 쓰세요. 면적(`height_cm × width_cm`)은 건축 모형·대형 설치 같은 극단값의 영향이 커서 평균과 중앙값을 함께 보세요.
- `period_made`, `size_group`으로 "시대에 따라 작품이 커졌나"를 살펴볼 수 있습니다. 제작 연도·크기가 빈칸이면 구간도 빈칸입니다.
- 빈칸(결측값): `title` 1개, `artist` 4개, `nationality` 36개, `nationality_group` 36개, `gender` 59개, `birth_year` 118개, `year_made` 23개, `period_made` 23개, `year_acquired` 10개, `height_cm` 134개, `width_cm` 135개, `size_group` 155개.
- `df.dropna()`를 하면 빈칸이 하나라도 있는 행이 사라져 전체의 약 28%가 줄어듭니다.
- 있을 수 없는 값(음수 나이, 범위 밖 점수, -999 등)은 모두 빈칸으로 바꿨으므로 **현재 파일에는 결측치(빈칸) 외의 이상값이 없습니다.** 전처리는 `isnull().sum()` → `dropna()`/`fillna()`로 끝납니다.

원자료의 `()`(정보 없음), `(0)`(출생연도 정보 없음), 높이·너비 0·-1·`not_a_date`는 모두 빈칸으로 바꿨습니다. 높이·너비의 빈칸이 약 13%로 많은 편이라 `dropna()`와 `fillna()`의 결과가 달라지는 점을 비교해 볼 수 있습니다.

열 이름 대응표(예전 → 새):

| 예전 열 이름 | 새 열 이름 |
|---|---|
| Title | `title` |
| Artist | `artist` |
| Nationality | nationality (+ nationality_group) |
| Gender | `gender` |
| BeginDate | `birth_year` |
| EndDate | (뺌) |
| Date | `year_made` |
| Medium | (뺌) |
| Classification | `classification` |
| Department | `department` |
| DateAcquired | `year_acquired` |
| Height (cm) | `height_cm` |
| Width (cm) | `width_cm` |

## 분석 아이디어
학생들이 고를 수 있는 주제 예시입니다. 모두 이 파일로 계산해서 결과가 나오는 것을 확인했습니다(그룹마다 행이 충분하고 값이 서로 다릅니다). **그대로 베끼지 말고 우리 팀의 진로에 맞게 질문을 바꿔 쓰세요.** 결과가 "차이가 거의 없음"으로 나와도 괜찮습니다. 그것도 분석 결과이고, 왜 그런지 생각해 볼 수 있습니다. 이 질문들은 사이트의 [기획] 탭에서도 눌러서 시작할 수 있습니다.

| 질문 | 묶는 기준 | 계산할 열 | 통계 | 그래프 | 새 열 만들기 |
|---|---|---|---|---|---|
| 작품 분류(classification)별 면적(height_cm × width_cm)의 중앙값은 어떻게 다를까? | `classification` | `height_cm * width_cm` | 중앙값 | 막대 | `df["area"] = df["height_cm"] * df["width_cm"]` |
| 작가 성별(gender)별 작품 수는 어떻게 다를까? | `gender` | 개수(빈도) | 개수 | 막대 | — |
| 작품 분류(classification)별 평균 제작 연도(year_made)는 어떻게 다를까? | `classification` | `year_made` | 평균 | 막대 | — |
| 제작 시기(period_made)에 따라 평균 높이(height_cm)는 어떻게 변할까? | `period_made` | `height_cm` | 평균 | 선 | — |
| 작품 분류(classification)별로 작가가 작품을 만든 나이(year_made - birth_year)는 평균 어떻게 다를까? | `classification` | `year_made - birth_year` | 평균 | 막대 | `df["age_made"] = df["year_made"] - df["birth_year"]` |
| 작가 국적 묶음(nationality_group)별 평균 너비(width_cm)는 어떻게 다를까? | `nationality_group` | `width_cm` | 평균 | 막대 | — |

이 데이터를 쓸 때 알아 둘 것:

- 분류별로 비슷한 수를 뽑은 표본이라 작품 수 비교는 의미가 없고, 평균·중앙값을 비교해요.
- 면적은 대형 설치 같은 극단값의 영향이 커서 중앙값도 함께 봐요. 높이·너비는 결측이 약 13%예요.

## 공개 배포 조건
원 데이터 CC0 1.0 https://creativecommons.org/publicdomain/zero/1.0/. MoMA의 요청에 따라 출처(MoMA)와 DOI를 표시하고, 이 파일이 원자료를 수정한 가공본임을 밝힙니다. MoMA가 이 가공본이나 수업을 보증하지 않습니다. 원자료는 큐레이터 검증이 끝나지 않은 정보를 포함합니다. licenses/MoMA-collection-original-README.md 참고.
