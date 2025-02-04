# 문제
백준 - N과 M (3) (S3)
https://www.acmicpc.net/problem/15651


# 풀이

```Kotlin
fun main() {
    val br = System.`in`.bufferedReader()
    val (n, m) = br.readLine().split(" ").map { it.toInt() }

    // 같은 수를 여러번 골라도 되기 때문에 방문 여부를 검사할 필요가 없음
    val arr = Array(m) { 0 }
    val sb = StringBuilder()

    fun backTracking(len: Int) {
        if (len == m) {
            arr.forEach {
                sb.append("$it ")
            }
            sb.append("\n")
            return
        }

        // 마찬가지로 방문 여부를 검사할 필요가 없음
        for (i in 1 .. n) {
            arr[len] = i
            backTracking(len + 1)
        }
    }

    backTracking(0)
    println(sb)
}
```


# 해설
* 백트래킹 문제
* 같은 수를 여러 번 골라도 된다는 조건이 있으므로 방문 여부를 검사할 필요 `X`
* 기존 풀이 방식에서 `visited` 배열과 관련된 부분을 삭제