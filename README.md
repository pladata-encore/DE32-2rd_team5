## 채팅 프로그램 및 챗봇 기능 구현

### 배경
사내기술 유출 이슈로 인해 감사팀 메신저 감찰 필요

### 주요 기능
1. 대화 기능
- 채팅방 입장시 ID 설정 기능
- 입장시 환영 및 입장 메시지 출력 기능
- 퇴장시 퇴장 메시지 출력 기능
2. 알림 기능
- Airflow 성공 시 성공 알림 메시지 전송
- 특정 시간(칸반미팅 시간) 알림 메시지 전송
3. 챗봇 기능
- 영화 검색 기능 : @영화검색 <영화이름> 입력 시 검색어가 포함된 영화 정보 출력
- 메시지 검색 기능 : @검색 <검색명> 입력 시 검색어가 포함된 채팅 내용 출력
4. 데이터 저장
- Airflow를 활용하여 채팅 로그를 parquet파일로 저장

### team repository
https://github.com/mammamia5

### 기술스택
- Apache Kafka
- Apache Spark
- Apache Airflow
- Apache Zeppelin
- Textualize

### 설정 및 실행
**Airflow 환경설정**
```bash
$ cat ~/.zshrc

export AIRFLOW_HOME=~/pj2/airflow
export AIRFLOW__CORE__DAGS_FOLDER=~/pj2/airflow/dags
export AIRFLOW__CORE__LOAD_EXAMPLES=False
```

**Kafka chatting program 실행**
```bash
$ source .venv/bin/activate
$ python src/chat/name.py
```

### 구조
**dags**

![image](https://github.com/user-attachments/assets/9e83751e-7750-4ff0-96b2-fdc2a7532e40)

**chat**

![image](https://github.com/user-attachments/assets/a1ff8b06-730a-4c82-b0b4-da94a79a2e31)

****
### 결과 - 채팅(Textualize에 구현)
![image](https://github.com/user-attachments/assets/f60899e7-ac7f-4ad2-8c3c-5ed1a4cf892a)

### 결과 - 채팅 감사

**사용률이 높은 단어**

![image](https://github.com/user-attachments/assets/57d0d7b8-343f-463c-b00f-219cb4142175)

**사용률이 높은 표현**
```
+-------------+-----+
|         word|count|
+-------------+-----+
|         exit|   83|
|           아|   69|
|         저는|   55|
|퇴장했습니다.|   40|
|     채팅방을|   40|
|         다들|   28|
|       민주님|   24|
|           그|   24|
|           저|   23|
|         주제|   21|
+-------------+-----+
```
**이용율이 높은 시간대**
```
+-----+------+------+-----+----+----+----+----+----+
|9to10|10to11|11to12|12to1|1to2|2to3|3to4|4to5|5to6|
+-----+------+------+-----+----+----+----+----+----+
|   41|     0|     0|    0|   0| 199|  56| 877|1086|
+-----+------+------+-----+----+----+----+----+----+
```
**최다 채팅 유저**
```
+------+----------+
|sender|count_user|
+------+----------+
|김원준|       824|
|박민주|       642|
|김맹지|       598|
|정미은|       357|
|*공지*|         8|
+------+----------+
```
### 수정 - 영화검색 결과 예쁘게 꾸미기

![image](https://github.com/user-attachments/assets/217866b7-8eff-4e08-a684-18ca1e7de081)

