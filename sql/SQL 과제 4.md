## 3-4. 오류를 디버깅하는 방법
**대표적인 오류 카테고리 : Syntax Error(문법 오류)**
~~~
1) SELECT
 
  col => 이 부분이 비어있기에 생기는 오류

 FROM

2) 집계함수 COUNT 인자 수가 일치하지 않아서 생기는 오류

3) GROUP BY에 적절한 칼럼을 명시하지 않았을 경우 발생하는 오류

4) 입력이 끝날 것으로 예상되었는데 SELECT 키워드가 입력되어 생기는 오류( 하나의 쿼리엔 하나의 SELECT)
-> SELECT 근처 확인, 쿼리 끝나는 부분에 ; 붙이고 실행할 부분만 드래그 앤 드랍해서 실행하기

5) LIMIT 오류
~~~

## 4-2. 데이터 타입과 데이터 변환

>**데이터 타입**

- 숫자
- 문자
- 시간, 날짜
- 부울

>**중요한 이유**

- 보이는 것과 저장된 것의 차이가 존재 => 내 생각과 다른 경우 데이터의 타입을 서로 변경해줘야 함

>**자료 타입 변경하기**

- 자료 타입을 변경하는 함수 : CAST_
```
SELECT
  CAST (1 AS STRING) #숫자 1을 문자 1로 변경
```

- 더 안전하게 데이터 타입 변경하기 : SAFE_CAST_**
~~~
: SAFE_가 붙은 함수는 변환이 실패할 경우, NULL로 반환.
~~~


>**수학함수**

암기 X 필요할 때 찾아쓰기

~~~
나누기를 하는 경우,

X/Y 대신 SAFE_dIVIDE 함수 사용 : SAFE_DIDVIDE(X,Y)
~~~
---

## 4-3. 문자열 함수

>**CONCAT함수 : 문자열 붙이기**

 ```sql
SELECT
    CONCAT("안녕","하세요","!") AS result
 ```
- CONCAT의 인자로 문자열이나 숫자를 넣을 때는 데이터를 직접 넣은 것-> FROM이 없어도 실행 
- CONCAT (컬럼1, 컬럼2)



>**SPLIT함수: 문자열 분리하기**

 ```sql
SELECT
    SPLIT("가,나,다,라",",") AS result
 ```
 - 쉽표 기준으로 나눠달라는 의미
 - SPLIT(문자열 원본, 나눌 기준이 되는 문자)


 >**REPLACE 함수 : 특정 단어 수정(치환)하기**

 ```sql
SELECT
    REPLACE("안녕하세요","안녕","실천") AS result
 ```
- 결과 : 실천하세요
- REPLACE (문자열 원본, 찾을 단어, 바꿀 단어)

 >**TRIM 함수 : 문자열 자르기**

  ```sql
 SELECT
    TRIM("안녕하세요","하세요")
 ```
 - 결과 : 안녕
 - TRIM(문자열 원본, 자를 단어)


>**UPPER 함수 : 대문자로 변경**

  ```sql
SELECT
    UPPER("abc") AS result
 ``````
- 결과 ABC

# 4-4.날짜 및 시간 데이터 이해하기(1)

>**핵심**
~~~
1) 날짜 및 시간 데이터 타입 파악하기 : DATE, DATETIME, TIMESTAMP
2) 날짜 및 데이터 관련 알면 좋은 내용 : UTC, Millisecond
3) 날짜 및 시간 데이터 타입 변환하기
4) 시간 함수(두 시간 차이, 특정 부분 추출하기)
~~~

 **시간 데이터 다루기**

- DATE : DATE만 표시하는 데이터 (2023-12-31)
- DATETIME : DATE와 TIME까지 표시하는 데이터 (2023-12-31 14:00:00) / TIME ZONE정보 없음
- TIME : 날짜없이 시간만 (14:00:00)

>**타임존**

GMT:Greenwich Mean Time(한국시간 GMT + 9)

- 영국의 그리니치 천문대(경도 0도) 를 기준으로 지역에 따른 시간의 차이를 조정하기 위해 생긴 시간의 구분선

- 영국 근처에서 자주 활용


>**UTC : Universal Time Coordinated**

- 국제적인 표준 시간
- 타임존이 존재한다 - 특정 지역의 표준 시간대
- 한국시간 + 9

>**TIMESTAMP**
 - UTC부터 경과한 시간을 나타내는 값.
- TIMEZONE정보 있음
- 2023-12-31 14:00:00 UTC

>**millisecond(ms)**
- 시간의 단위, 천분의 1초(1,000ms = 1초)
- 빠른 반응이 필요한 분야에서 사용 (초보다 더 정확)
- millisecond > timestamp > datetime으로 변경

>**microsecond**
- 1/1,000ms

 ```sql
SELECT 
  TIMESTAMP_MILLIS(1704176819711) AS milli_to_timestamp_value,
  TIMESTAMP_MICROS(1704176819811000) AS micro_to_timestamp_value,
   DATETIME(tIMESTAMP_MICROS(1704176819711000), 'Asia/Seoul') AS datetime_value;
 `````

- 변환시 타임존('Asia/Seoul')이 존재하는지 확인

>**TIMESTAMP와 DATETIME비교**
~~~
TIMESTAMP
- 타임존이 UTC라고 나옴
- 시간 차이가 한국시간 -9시간임

DATETIME
- 타임존이 T가 나옴(TIME)
- 한국 Zone 사용시 한국 시간과 동일
