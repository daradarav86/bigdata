# computer.csv — 프로젝트용

관심 진로: 컴퓨터공학, 소프트웨어 개발, 인공지능, 정보보안, IT 산업

가공본 2,005행 × 14열. 이 파일은 분석·시각화 전 학생이 전처리하는 자료입니다.

## 원자료 및 준비 기준
Stack Overflow Annual Developer Survey 2025 (results.csv, 응답 49,191건). Retrieved 2026-10-24.

https://survey.stackoverflow.co/ · https://github.com/StackExchange/Survey/tree/main/packages/archive/2025

원 172열 중 14열을 원 열 이름 그대로 선택. 응답 2,000건을 고정 난수42로 무작위 추출해 ResponseId 순으로 정렬. 무응답 빈칸, 여러 답을 `;`로 이어 쓴 열, 연봉의 극단값을 모두 유지. 응답 값을 번역·재분류하지 않음.

## 열 설명
| 열 | 뜻·단위 |
|---|---|
| `ResponseId` | 원자료 응답 번호 |
| `MainBranch` | 응답자 유형(직업 개발자, 학생, 취미 등) |
| `Age` | 나이 구간 문자열 |
| `EdLevel` | 최종 학력 |
| `YearsCode` | 교육 포함 코딩 경력, 년 |
| `WorkExp` | 직업 경력, 년 |
| `DevType` | 직무(백엔드, 데이터 과학자, 학생 등) |
| `OrgSize` | 회사 규모 구간 |
| `RemoteWork` | 근무 형태(원격·혼합·출근) |
| `Country` | 거주 국가 |
| `ConvertedCompYearly` | 연간 총보수, 미국 달러로 환산. 극단값 존재 |
| `LanguageHaveWorkedWith` | 지난 1년간 사용한 언어 목록, `;` 구분 |
| `AISelect` | 개발에 AI 도구 사용 여부·빈도 |
| `JobSat` | 직무 만족도 0~10 |

## 수업용 가공
전처리 연습을 위해 원자료를 다음과 같이 바꿨습니다.
- 빈칸: `Age` 6개
- 있을 수 없는 값: `YearsCode` -1 5개, `JobSat` 99 5개(만족도 범위 0~10 밖)
- 중복 행: 응답 5개를 한 번 더 넣음(같은 `ResponseId`가 두 번 나옴)

그 밖의 빈칸은 원자료의 무응답입니다. 표본 2,000건 기준 원자료 빈칸 수: `EdLevel` 32, `YearsCode` 265, `WorkExp` 255, `DevType` 226, `OrgSize` 603, `RemoteWork` 619, `Country` 577, `ConvertedCompYearly` 1,036, `LanguageHaveWorkedWith` 714, `AISelect` 633, `JobSat` 920.

## 공개 배포 조건
Survey data licensed under ODbL 1.0 https://opendatacommons.org/licenses/odbl/1-0/, contents under DbCL 1.0 https://opendatacommons.org/licenses/dbcl/1-0/. computer.csv 가공본도 ODbL 1.0으로 배포합니다(동일조건). 출처·가공 사실·원조건을 함께 표시하세요. 원자료에서 바꾼 내용은 이 안내의 "원자료 및 준비 기준"과 "수업용 가공"에 적었습니다. 제공자가 이 가공본을 보증하거나 추천하지 않습니다.
