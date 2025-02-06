# 문제
SQL 고득점 Kit - 이름에 el이 들어가는 동물 찾기 (LV.2)
https://school.programmers.co.kr/learn/courses/30/lessons/59047


# 풀이

```SQL
SELECT ANIMAL_ID, NAME
FROM ANIMAL_INS
WHERE NAME LIKE '%EL%'
    AND ANIMAL_TYPE = 'DOG'
ORDER BY NAME
```


# 해설
* 이름에 "EL"이 들어가는 개 :
  `WHERE NAME LIKE '%EL%'
  AND ANIMAL_TYPE = 'DOG'`
* 이름 순으로 조회 : `ORDER BY NAME`