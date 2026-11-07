# astronomy.csv — 프로젝트용

관심 진로: 천문학, 우주과학, 물리, 지구과학, 항공우주

가공본 936행 × 13열. 이 파일은 분석·시각화 전 학생이 전처리하는 자료입니다.

## 원자료 및 준비 기준
HYG Star Database v4.4 (Hipparcos, Yale Bright Star, Gliese 카탈로그를 합친 별 목록, 119,614개). hyg_v44.csv.gz. Retrieved 2026-10-30.

https://codeberg.org/astronexus/hyg · https://github.com/astronexus/HYG-Database

맨눈으로 보이는 별(겉보기 등급 `mag` 6.5 이하)만 골랐습니다. 태양과 거리 정보가 없다는 표시(`dist` 100000 이상)인 별, 분광형이 O·B·A·F·G·K·M으로 시작하지 않는 특수한 별은 뺐습니다. 분광형 첫 글자별로 최대 150개를 고정 난수42로 무작위 추출했고(O형은 30개뿐), 분광형이 빈칸인 별 6개는 모두 넣어 id 순으로 정렬했습니다. 원 37열 중 10열을 원 열 이름 그대로 선택하고 `spectral_class` 열을 하나 더했습니다. `lum`은 소수 넷째 자리까지 반올림했습니다. 열 이름은 약어(`con`, `ra`, `dec`, `dist`, `mag`, `absmag`, `ci`, `lum`, `spect`)에서 뜻이 보이는 이름으로 바꿨습니다.

## 열 설명
| 열 | 뜻·단위 |
|---|---|
| `star_id` | HYG 별 번호 |
| `constellation` | 별자리 3글자 약칭(예: Ori 오리온, UMa 큰곰) |
| `right_ascension_h` | 적경, 시(0~24), 2000년 기준 |
| `declination_deg` | 적위, 도(-90~90), 2000년 기준 |
| `distance_pc` | 지구에서 별까지의 거리, 파섹(pc). 1pc ≈ 3.262광년 |
| `apparent_mag` | 겉보기 등급. 숫자가 작을수록 밝게 보임 |
| `absolute_mag` | 절대 등급. 10pc 거리에서 본 밝기, 숫자가 작을수록 실제로 밝음 |
| `color_index` | 색지수(B−V). 작을수록 푸르고 뜨거운 별, 클수록 붉고 차가운 별 |
| `luminosity` | 광도, 태양을 1로 한 배수 |
| `spectral_type` | 분광형(예: G2V, K5III), 빈칸 존재 |
| `spectral_class` | 분광형의 첫 글자(O·B·A·F·G·K·M, 대략 뜨거운 별부터 차가운 별 순서). `spectral_type`에서 만든 가공 열 |
| `distance_group` | 거리 구간(가공 열): 1_under_70pc / 2_70_130pc / 3_130_230pc / 4_over_230pc |
| `hemisphere` | 하늘의 반구(가공 열): 적위가 0도 이상이면 north, 아니면 south |

## 수업용 가공
**2026-11-07에 학생이 분석하기 쉽게 다시 정리했습니다.**

- 열 이름은 영어 소문자와 밑줄(`_`)로 짧게 바꿨습니다(아래 대응표). 열 이름에 공백·괄호·단위가 없어서 `df["열이름"]`으로 그대로 쓸 수 있습니다.
- 분광형별로 150개씩(O형은 30개) 뽑은 표본이라 **개수 비교는 의미가 없고 평균 비교에만** 쓰세요. 맨눈으로 보이는 별만 모아서 실제로 밝은 별(거성 등)이 많이 들어 있습니다.
- `distance_pc × 3.262`로 광년 열을 만들어 볼 수 있습니다.
- `distance_group`, `hemisphere`로 "멀수록 어둡게 보이나", "북쪽 하늘과 남쪽 하늘이 다른가"를 살펴볼 수 있습니다. 맨눈으로 보이는 별만 모았으므로 먼 별은 원래 밝은 별이 많습니다.
- 빈칸(결측값): `distance_pc` 5개, `apparent_mag` 5개, `absolute_mag` 3개, `color_index` 8개, `luminosity` 5개, `spectral_type` 6개, `spectral_class` 6개, `distance_group` 5개.
- `df.dropna()`를 하면 빈칸이 하나라도 있는 행이 사라져 전체의 약 3%가 줄어듭니다.
- 있을 수 없는 값(음수 나이, 범위 밖 점수, -999 등)은 모두 빈칸으로 바꿨으므로 **현재 파일에는 결측치(빈칸) 외의 이상값이 없습니다.** 전처리는 `isnull().sum()` → `dropna()`/`fillna()`로 끝납니다.

원자료 값을 비운 칸(고정 난수42, 서로 다른 행): `apparent_mag` 5개, `distance_pc` 5개, `luminosity` 5개, `absolute_mag` 3개. 그 밖의 빈칸은 원자료에 원래 없던 값입니다(`spectral_type`·`spectral_class` 각 6개, `color_index` 8개).

열 이름 대응표(예전 → 새):

| 예전 열 이름 | 새 열 이름 |
|---|---|
| id | `star_id` |
| con | `constellation` |
| ra | `right_ascension_h` |
| dec | `declination_deg` |
| dist | `distance_pc` |
| mag | `apparent_mag` |
| absmag | `absolute_mag` |
| ci | `color_index` |
| lum | `luminosity` |
| spect | `spectral_type` |

## 분석 아이디어
학생들이 고를 수 있는 주제 예시입니다. 모두 이 파일로 계산해서 결과가 나오는 것을 확인했습니다(그룹마다 행이 충분하고 값이 서로 다릅니다). **그대로 베끼지 말고 우리 팀의 진로에 맞게 질문을 바꿔 쓰세요.** 결과가 "차이가 거의 없음"으로 나와도 괜찮습니다. 그것도 분석 결과이고, 왜 그런지 생각해 볼 수 있습니다. 이 질문들은 사이트의 [기획] 탭에서도 눌러서 시작할 수 있습니다.

| 질문 | 묶는 기준 | 계산할 열 | 통계 | 그래프 | 새 열 만들기 |
|---|---|---|---|---|---|
| 분광형(spectral_class)별 색지수(color_index) 평균은 어떻게 다를까? | `spectral_class` | `color_index` | 평균 | 막대 | — |
| 분광형(spectral_class)별 절대 등급(absolute_mag) 평균은 어떻게 다를까? | `spectral_class` | `absolute_mag` | 평균 | 막대 | — |
| 별까지의 거리 구간(distance_group)별 겉보기 등급(apparent_mag) 평균은 어떻게 다를까? | `distance_group` | `apparent_mag` | 평균 | 막대 | — |
| 북반구 하늘과 남반구 하늘(hemisphere)의 별 밝기(apparent_mag) 평균은 어떻게 다를까? | `hemisphere` | `apparent_mag` | 평균 | 막대 | — |
| 분광형(spectral_class)별 광도(luminosity)의 평균과 중앙값은 얼마나 다를까? | `spectral_class` | `luminosity` | 중앙값 | 막대 | — |
| 분광형(spectral_class)별 별까지의 거리(distance_pc × 3.262, 광년)는 평균 어떻게 다를까? | `spectral_class` | `distance_pc * 3.262` | 평균 | 막대 | `df["distance_ly"] = df["distance_pc"] * 3.262` |

이 데이터를 쓸 때 알아 둘 것:

- 분광형별로 150개씩(O형은 30개) 뽑은 표본이라 개수 비교는 의미가 없고, 평균을 비교해요.
- 광도(luminosity)는 극단값이 커서 평균과 중앙값이 크게 달라요.

## 공개 배포 조건
HYG v4.0 이후 버전은 Creative Commons Attribution-ShareAlike 4.0 International(CC BY-SA 4.0) http://creativecommons.org/licenses/by-sa/4.0/ 로 공개됩니다. astronomy.csv 가공본도 같은 조건(CC BY-SA 4.0)으로 배포합니다. 출처·가공 사실·원조건을 함께 표시하세요. 원자료에서 바꾼 내용은 이 안내의 "원자료 및 준비 기준"과 "수업용 가공"에 적었습니다. 제공자가 이 가공본을 보증하거나 추천하지 않습니다. licenses/HYG-LICENSE-NOTICE.txt 참고.
