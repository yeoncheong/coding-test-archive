# 문제
백준 - OX 퀴즈 (B2)
https://www.acmicpc.net/problem/8958


# 풀이

```Kotlin
// 84ms
fun main() {
    val br = System.`in`.bufferedReader()
    val num = br.readLine().toInt()

    repeat (num) {
        val str = br.readLine().toString()
        var score = 0
        var result = 0

        // 받는 문자열의 길이만큼 for문 돌면서
        for (i in 0 until str.length) {
            // O 나오면 score + 1, 최종 점수에 score 더하기
            if (str[i] == 'O') {
                score++
                result += score
            } else {
                // X 나오면 score을 0으로 만들어서 초기화
                score = 0
            }
        }

        /*
        for (i in str) {
            if (i == 'O') {
                score++
                result += score
            } else {
                score = 0
            }
        }
        */

        println(result)
    }
}
```

```kotlin
// 88ms
fun main() {
    val br = System.`in`.bufferedReader()
    val num = br.readLine().toInt()

    repeat (num) {
        val str = br.readLine().toString()
        var score = 0
        var result = 0

        str.forEach {
            if (it == 'O') {
                score++
                result += score
            } else {
                score = 0
            }
        }
        println(result)
    }
}
```


# 해설
* 구현, 문자열 문제
* `O`는 기본적으로 `1점`, 연속되면 `+1점`씩 중첩되는 점수를 더함
* `score` 변수를 두어서 `O`이 반복되면 `score`에 `1`점씩 쌓으면 중첩 점수를 만듦
* `X`를 만나면 `score`를 `0`으로 초기화하여 중첩 점수를 없앰