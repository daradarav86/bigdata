# engineering.csv — 프로젝트용

관심 진로: 공학 전반(토목·건축·재료·화학·환경공학), 건설, 신소재

가공본 1,005행 × 14열. 이 파일은 분석·시각화 전 학생이 전처리하는 자료입니다.

## 원자료 및 준비 기준
Yeh, I-C. (1998). Concrete Compressive Strength. UCI. https://doi.org/10.24432/C5PK67 (Concrete_Data.xls)

https://archive.ics.uci.edu/dataset/165/concrete+compressive+strength

실험실에서 콘크리트 배합 1,030건의 재령(일)별 압축강도를 측정한 원자료에서, 배합·재령·강도가 모두 같은 중복 행 25개를 뺀 1,005건입니다. 단위가 들어간 긴 원 열 이름(공백 두 칸·끝 공백 포함)은 짧은 이름으로 바꿨고, 재령을 4단계로 묶은 `age_stage` 열을 더했습니다. 물-시멘트비 같은 파생 열은 미리 만들지 않았습니다.

## 열 설명
| 열 | 뜻·단위 |
|---|---|
| `cement` | 시멘트, 콘크리트 1m³당 kg |
| `slag` | 고로 슬래그(제철 부산물), kg/m³ |
| `fly_ash` | 플라이애시(화력발전 부산물), kg/m³ |
| `water` | 물, kg/m³ |
| `superplasticizer` | 고성능 감수제, kg/m³ |
| `coarse_aggregate` | 굵은 골재(자갈), kg/m³ |
| `fine_aggregate` | 잔골재(모래), kg/m³ |
| `age_day` | 재령(타설 후 경과일), 1~365일 |
| `strength_mpa` | 압축강도, MPa |
| `age_stage` | 재령 구간(가공 열): stage1_1_7d(1~7일) / stage2_14_28d(14·28일) / stage3_56_100d(56~100일) / stage4_120d_plus(120일 이상). 번호 순서가 시간 순서 |
| `cement_level` | 시멘트 양 구간(가공 열): 1_low(250kg/m³ 미만) / 2_mid(250~349) / 3_high(350 이상) |
| `uses_slag` | 고로 슬래그를 넣었는지(가공 열) yes/no |
| `uses_fly_ash` | 플라이애시를 넣었는지(가공 열) yes/no |
| `uses_superplasticizer` | 고성능 감수제를 넣었는지(가공 열) yes/no |

## 수업용 가공
**2026-11-07에 학생이 분석하기 쉽게 다시 정리했습니다.**

- 열 이름은 영어 소문자와 밑줄(`_`)로 짧게 바꿨습니다(아래 대응표). 열 이름에 공백·괄호·단위가 없어서 `df["열이름"]`으로 그대로 쓸 수 있습니다.
- 원자료의 완전 중복 행 25개를 뺐습니다. 수업용으로 빈칸을 넣은 것은 중복이 아닌 행뿐입니다.
- `age_stage`를 더했습니다. 재령 1·120·360일은 시료가 2~6개뿐이라 `age_day`로 묶으면 그룹 크기가 들쭉날쭉합니다. 막대그래프는 `age_stage`가 읽기 좋고, 선그래프는 `age_day`를 쓰세요.
- `uses_slag`, `uses_fly_ash`, `uses_superplasticizer`는 그 재료의 양이 0보다 크면 yes, 0이면 no입니다. 양이 0인 것은 결측이 아니라 그 재료를 넣지 않았다는 뜻입니다.
- 빈칸(결측값): `cement` 5개, `water` 5개, `age_day` 3개, `strength_mpa` 8개, `age_stage` 3개, `cement_level` 5개.
- `df.dropna()`를 하면 빈칸이 하나라도 있는 행이 사라져 전체의 약 2%가 줄어듭니다.
- 있을 수 없는 값(음수 나이, 범위 밖 점수, -999 등)은 모두 빈칸으로 바꿨으므로 **현재 파일에는 결측치(빈칸) 외의 이상값이 없습니다.** 전처리는 `isnull().sum()` → `dropna()`/`fillna()`로 끝납니다.

원자료에는 결측이 없었고, 아래 빈칸은 모두 수업용으로 넣은 것입니다(원 값이 있을 수 없는 값이던 칸 포함: `age_day` -1, `strength_mpa` -999).

열 이름 대응표(예전 → 새):

| 예전 열 이름 | 새 열 이름 |
|---|---|
| Cement (component 1)(kg in a m^3 mixture) | `cement` |
| Blast Furnace Slag (component 2)(kg in a m^3 mixture) | `slag` |
| Fly Ash (component 3)(kg in a m^3 mixture) | `fly_ash` |
| Water  (component 4)(kg in a m^3 mixture) | `water` |
| Superplasticizer (component 5)(kg in a m^3 mixture) | `superplasticizer` |
| Coarse Aggregate  (component 6)(kg in a m^3 mixture) | `coarse_aggregate` |
| Fine Aggregate (component 7)(kg in a m^3 mixture) | `fine_aggregate` |
| Age (day) | `age_day` |
| Concrete compressive strength(MPa, megapascals)  | `strength_mpa` |

## 분석 아이디어
학생들이 고를 수 있는 주제 예시입니다. 모두 이 파일로 계산해서 결과가 나오는 것을 확인했습니다(그룹마다 행이 충분하고 값이 서로 다릅니다). **그대로 베끼지 말고 우리 팀의 진로에 맞게 질문을 바꿔 쓰세요.** 결과가 "차이가 거의 없음"으로 나와도 괜찮습니다. 그것도 분석 결과이고, 왜 그런지 생각해 볼 수 있습니다. 이 질문들은 사이트의 [기획] 탭에서도 눌러서 시작할 수 있습니다.

| 질문 | 묶는 기준 | 계산할 열 | 통계 | 그래프 | 새 열 만들기 |
|---|---|---|---|---|---|
| 재령 구간(age_stage)이 길수록 압축강도(strength_mpa) 평균이 높을까? | `age_stage` | `strength_mpa` | 평균 | 막대 | — |
| 플라이애시를 쓴 배합과 안 쓴 배합(uses_fly_ash)의 압축강도(strength_mpa) 평균은 어떻게 다를까? | `uses_fly_ash` | `strength_mpa` | 평균 | 막대 | — |
| 고성능 감수제 사용 여부(uses_superplasticizer)별 압축강도(strength_mpa) 평균은 어떻게 다를까? | `uses_superplasticizer` | `strength_mpa` | 평균 | 막대 | — |
| 시멘트 양(cement_level)이 많을수록 압축강도(strength_mpa)가 높을까? | `cement_level` | `strength_mpa` | 평균 | 막대 | — |
| 재령(age_day)에 따라 압축강도(strength_mpa) 평균은 어떻게 변할까? | `age_day` | `strength_mpa` | 평균 | 선 | — |
| 재령 구간(age_stage)별 물-시멘트비(water / cement)는 어떻게 다를까? | `age_stage` | `water / cement` | 평균 | 막대 | `df["wc_ratio"] = df["water"] / df["cement"]` |

이 데이터를 쓸 때 알아 둘 것:

- uses_fly_ash 등은 그 재료의 양이 0이면 no예요. 0은 결측이 아니라 "넣지 않았다"는 뜻이에요.
- 재령 1일·120일·360일은 시료가 2~6개뿐이라 막대는 age_stage가, 선그래프는 age_day가 어울려요.

## 공개 배포 조건
CC BY 4.0 https://creativecommons.org/licenses/by/4.0/. 출처·가공 사실·원조건을 함께 표시하세요. 원자료에서 바꾼 내용은 이 안내의 "원자료 및 준비 기준"과 "수업용 가공"에 적었습니다. 제공자가 이 가공본을 보증하거나 추천하지 않습니다.
