# students_lesson.csv — 학생의 학습·생활과 성적

관심 진로: 교육, 상담, 심리, 사회복지

한 행의 의미: 포르투갈 두 학교의 포르투갈어 과목 학생 기록 1건. 가공본 649행 × 11열.

## 원자료 및 공개 조건
Cortez, P. (2008). Student Performance. UCI. https://doi.org/10.24432/C5TG7T

원자료 설명: https://archive.ics.uci.edu/dataset/320/student+performance

이용조건: CC BY 4.0. 출처·원 라이선스 링크·가공 사실을 함께 표시하고 원 제공자의 공식 추천 자료로 소개하지 않습니다.

## 교사가 가공한 내용
포르투갈어 과목 649건만 사용. 수학 파일과 결합하지 않음. 11열 선택. 원점수·순서척도 유지. record_id는 가공용 행 번호.

결측치 수: {"record_id": 0, "age": 0, "study_level": 0, "travel_level": 0, "activities": 0, "internet": 0, "higher_education": 0, "freetime": 0, "health": 0, "absences": 0, "final_score": 0}. CSV 빈칸은 pandas에서 NaN으로 읽습니다. 열 평균 계산은 결측을 제외하므로 분석에 사용한 수를 함께 확인합니다. 원자료 숫자를 임의로 만들거나 수정하지 않았습니다.

## 열 안내
| 열 | 의미와 단위 |
|---|---|
| `record_id` | 가공용 행 번호; 실제 학번 아님 |
| `age` | 나이, 세 |
| `study_level` | 주당 공부 시간 구간: 1=<2시간, 2=2~5시간, 3=5~10시간, 4=>10시간. 실제 시간 아님 |
| `travel_level` | 통학 시간 구간: 1=<15분, 2=15~30분, 3=30분~1시간, 4=>1시간 |
| `activities` | 교과 외 활동 참여 yes/no |
| `internet` | 집 인터넷 이용 가능 yes/no |
| `higher_education` | 고등교육 진학 희망 yes/no |
| `freetime` | 방과 후 자유시간 자기보고 1~5, 높을수록 많음 |
| `health` | 건강 자기보고 1~5, 높을수록 좋음; 진단 결과 아님 |
| `absences` | 원자료 학교 결석 횟수, 한국 출결의 일수와 동일하다고 가정하지 않음 |
| `final_score` | 마지막 학기 성적, 0~20점; 0도 유효 값 |

## 탐구 질문 선택
1. 공부 시간 구간에 따라 평균 성적이 다른가?
2. 교과 외 활동 참여 여부에 따라 평균 성적이 다른가?
3. 인터넷 이용 가능 여부별 학생 수와 평균 성적은 어떤가?

위 질문 중 하나를 고르거나 같은 열을 사용해 질문을 바꾸세요. 기본 과제는 질문 1개, 표 1개, 그래프 1개, 수치를 포함한 해석 2문장, 한계 1문장입니다.

## 첫 분석 예시
```python
import pandas as pd
df = pd.read_csv('data/students_lesson.csv')
display(df.head())
result = df.groupby("study_level")["final_score"].mean()
display(result)
result.plot(kind='bar', xlabel='Study-time category', ylabel='Mean score (0-20)', rot=45)
```

이 경로는 압축을 푼 폴더에서 실행하는 예시입니다. Colab에서는 첨부 노트북의 파일 업로드 셀 또는 GitHub Raw 주소 셀을 사용하세요.

## 결론 작성 틀
“분석 대상은 ___이고 사용한 기준은 ___이다. ___의 값은 ___로, ___와 비교하면 ___ 차이가 있었다. 다만 ___ 때문에 이 결과를 모든 대상에게 일반화하기 어렵다.”

## 해석할 때 주의
한국 고등학생의 대표 표본이 아니며 생활습관의 인과 효과나 심리 상태를 판정할 수 없다. 공부 시간 구간의 평균을 실제 시간 평균으로 해석하지 않는다. 수면·스트레스 데이터는 포함되지 않는다.
