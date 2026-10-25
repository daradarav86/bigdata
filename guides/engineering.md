# engineering.csv — 프로젝트용

관심 진로: 공학 전반(토목·건축·재료·화학·환경공학), 건설, 신소재

가공본 1,030행 × 9열. 이 파일은 분석·시각화 전 학생이 전처리하는 자료입니다.

## 원자료 및 준비 기준
Yeh, I-C. (1998). Concrete Compressive Strength. UCI. https://doi.org/10.24432/C5PK67 (Concrete_Data.xls)

https://archive.ics.uci.edu/dataset/165/concrete+compressive+strength

실험실에서 콘크리트 배합 1,030건의 재령(일)별 압축강도를 측정한 원자료 전체. 엑셀 파일을 CSV로 바꾸고 단위가 들어간 긴 원 열 이름을 그대로 유지(공백 두 칸·끝 공백 포함). 물-시멘트비 같은 파생 열은 미리 만들지 않음. 배합과 재령이 완전히 같은 중복 행 25개는 원자료 그대로 둠.

## 열 설명
| 열 | 뜻·단위 |
|---|---|
| `Cement (component 1)(kg in a m^3 mixture)` | 시멘트, 콘크리트 1m³당 kg |
| `Blast Furnace Slag (component 2)(kg in a m^3 mixture)` | 고로 슬래그(제철 부산물), kg/m³ |
| `Fly Ash (component 3)(kg in a m^3 mixture)` | 플라이애시(화력발전 부산물), kg/m³ |
| `Water  (component 4)(kg in a m^3 mixture)` | 물, kg/m³ |
| `Superplasticizer (component 5)(kg in a m^3 mixture)` | 고성능 감수제, kg/m³ |
| `Coarse Aggregate  (component 6)(kg in a m^3 mixture)` | 굵은 골재(자갈), kg/m³ |
| `Fine Aggregate (component 7)(kg in a m^3 mixture)` | 잔골재(모래), kg/m³ |
| `Age (day)` | 재령(타설 후 경과일), 1~365일 |
| `Concrete compressive strength(MPa, megapascals) ` | 압축강도, MPa |

## 수업용 가공
전처리 연습을 위해 원자료를 다음과 같이 바꿨습니다.
- 빈칸: 시멘트 5개, 물 5개, 압축강도 5개
- 있을 수 없던 값(→ 모두 빈칸으로 바꿈): `Age (day)` -1 3개, 압축강도 -999 3개

**현재 파일에는 결측치(빈칸) 외의 이상값이 없습니다.** 범위 밖 값은 모두 빈칸으로 바꿨으므로 전처리는 `isnull().sum()` → `dropna()`/`fillna()`만으로 끝납니다. 아래 빈칸 개수에 바꾼 값이 더해져 실제 빈칸은 더 많습니다.

원자료에는 결측이 없습니다. 배합·재령이 모두 같은 중복 행 25개는 원자료 그대로이며, 수업용 변경은 중복 행이 아닌 행에만 넣었습니다.

## 공개 배포 조건
CC BY 4.0 https://creativecommons.org/licenses/by/4.0/. 출처·가공 사실·원조건을 함께 표시하세요. 원자료에서 바꾼 내용은 이 안내의 "원자료 및 준비 기준"과 "수업용 가공"에 적었습니다. 제공자가 이 가공본을 보증하거나 추천하지 않습니다.
