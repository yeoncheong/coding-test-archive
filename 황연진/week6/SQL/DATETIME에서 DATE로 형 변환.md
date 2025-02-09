# 문제
SQL 고득점 Kit - DATETIME에서 DATE로 형 변환 (LV.2)
https://school.programmers.co.kr/learn/courses/30/lessons/59414


# 풀이

```SQL
SELECT ANIMAL_ID, NAME, DATE_FORMAT(DATETIME, "%Y-%m-%d") AS 날짜
FROM ANIMAL_INS
ORDER BY ANIMAL_ID
```


# 해설
* 시각(시-분-초)을 제외한 날짜(년-월-일)만 : `DATE_FORMAT(DATETIME, "%Y-%m-%d") AS 날짜`
* 아이디 순으로 조회 : `ORDER BY ANIMAL_ID`