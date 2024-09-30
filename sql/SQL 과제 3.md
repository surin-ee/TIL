# 연습문제
## 1번. type 2가 없는 포켓몬의 수 쿼리 작성

~~~
- 조건 : type 2가 없는
- type 2가 어떻게 생겼지? type 2d의 정의는 무엇이지?
- type 2 : NULL ; 0이랑 다르고 **랑도 다름 => 값이 없는 상태
- 연산자 IS NULL/ IS NOT NULL
- type2 = NULL은 안되나? 안됨 NULL은 다른 값과 직접 비교할 수 없음. NULL = NULL 거짓이 아니라 알 수 없
- 어떤 테이블? poketmon
- 어떤 집계? 포켓몬의 수 ==> COUNT
~~~
```sql
SELECT 
  COUNT(id) AS cnt
FROM basic.pokemon
WHERE
 type2 IS NULL
 OR type1 ='Fire'
```
- WHERE 절에서 여러 조건을 연결하고 싶은 경우 => AND 조건을 사용
- OR 조건 => () OR ()

## 2번. type 2 없는 포켓몬 type1과 그 수를 알려주는 쿼리 작성 (type 1 포켓몬 수가 큰 순으로 정렬)
~~~
테이블 : poketmon
조건 : type 2가 없는 포켓몬
정렬 : type 2가 없는 포켓몬
컬럼 : type 1
집계 : 포켓몬 수 => COUNT
정렬 : type1의 포켓몬 수가 큰 순으로 정렬 => ORDER BY. 
~~~
```sql
SELECT
 type1,
 COUNT(id) AS poketmon_cnt
FROM basic. poketmon
WHERE
 type2 IS NULL
GROUP BY
 type1
ORDER BY
 poketmon_cnt DESC
```
- 큰 것부터 작은 것으로 => 내림차순(DESC)=> ORDER BY 포켓몬 수  DESC

- 집계함수는 GROUP BY와 같이 다님. 집계하는 기준(컬럼)이 없으면 COUNT만 쓸 수 있으나, 집계하는 기준이 있다면 그 기준 컬럼을 GROUP BY에 써줘야 함

## 3번. type2 상관없이 type1의 포켓몬 수 알 수 있는 쿼리 작성

```sql
SELECT
 type1,
 COUNT(id) AS poketmon_cnt,
 COUNT(DISTINCT id) AS poketmon_cnt2
FROM basic.poketmon
GROUP BY
 type1
```
- DISTINCT ; 고유한(uique) 값만 보고 싶을 떄 사용
 - COUNT(id)=COUNT(DISTINCT id); id 설계 시 중복이 없게 설계함 그래서 두 개의 결과가 동일