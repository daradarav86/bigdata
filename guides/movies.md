# movies.csv — 프로젝트용

관심 진로: 미디어, 영화, 문화콘텐츠, 마케팅, 추천 서비스

가공본 9,742행 × 5열. 이 파일은 분석·시각화 전 학생이 전처리하는 자료입니다.

## 원자료 및 준비 기준
GroupLens. MovieLens latest-small (generated 2018-09-26). Harper & Konstan (2015), https://doi.org/10.1145/2827872

https://files.grouplens.org/datasets/movielens/ml-latest-small-README.html

원 영화 9,742편 모두 유지. 교사는 평점 평균·개수만 미리 병합해 다중 파일 병합 부담을 줄임. 평가 없는 영화/미등록 장르/연도 없는 제목 유지.

## 열 설명
| 열 | 뜻·단위 |
|---|---|
| `movieId` | 영화 ID |
| `title` | 연도가 괄호로 포함될 수 있는 제목 |
| `genres` | 전체 장르 목록, | 구분, 미등록 표시 존재 |
| `rating_mean` | 0.5~5점 평균, 평가 없으면 결측 |
| `rating_count` | 평가 수, 평가 없는 영화는 결측 |

## 공개 배포 조건
MovieLens 자체 이용조건; 비상업적 사용, 출처 표시, 동일 조건 재배포, 보증·추천 암시 금지. 출처·가공 사실·원조건을 함께 표시하세요. 데이터의 오류를 인위적으로 추가하지 않았습니다.
