# 문제
백준 - N과 M (4) (S3)
https://www.acmicpc.net/problem/15652


# 풀이

```Kotlin
fun main() {
    val br = System.`in`.bufferedReader()
    val (n, m) = br.readLine().split(" ").map { it.toInt() }

    val arr = Array(m) { 0 }
    val sb = StringBuilder()

    fun backTracking(idx: Int, len: Int) {
        if (len == m) {
            arr.forEach {
                sb.append("$it ")
            }
            sb.append("\n")
            return
        }

        /* 중복은 가능하되 오름차순은 허용하지 않으므로
        직전 수를 idx로 전달받아 idx부터 for문 돌기 */
        for (i in idx .. n) {
            arr[len] = i
            backTracking(i, len + 1)
        }
    }

    backTracking(1, 0)
    println(sb)
}
```


# 해설
* 백트래킹 문제
* 같은 수를 여러 번 골라도 된다는 조건이 있으므로 방문 여부를 검사할 필요 `X`
* 기존 풀이 방식에서 `visited` 배열과 관련된 부분을 삭제
* 비내림차순 정렬이 조건이므로 함수 내에서 `for문`을 돌 때 원래 값보다 작은 값이 있으면 안됨
  `idx` 인수를 만들어서 현재 `i`값을 다음 함수에 넘겨줌
  다음 함수에서 `for문`을 돌 때 `i`보다 작은 값이 들어가지 않도록 함