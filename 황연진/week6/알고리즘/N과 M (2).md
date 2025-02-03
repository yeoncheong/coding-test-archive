# 문제
백준 - N과 M (2) (S3)
https://www.acmicpc.net/problem/15650


# 풀이

```Kotlin
fun main() {
    val br = System.`in`.bufferedReader()
    val (n, m) = br.readLine().split(" ").map { it.toInt() }

    // 저장 배열은 수열 길이와 동일하게
    val arr = Array(m) { 0 }
    // 방문 배열은 사용할 수 있는 숫자와 동일해야 하므로 n + 1
    val visited = BooleanArray(n + 1) { false }

    // StringBuilder를 사용하는 것이 시간을 훨씬 단축할 수 있음
    val sb = StringBuilder()

    fun backTracking(idx: Int, len: Int) {
        if (len == m) {
            arr.forEach {
                sb.append("$it ")
            }
            sb.append("\n")
            return
        }

        // 다음 재귀함수에서 i보다 작은 값이 들어가지 않도록 idx(전 함수의 i값)부터 for문 시작
        for (i in idx .. n) {
            if (!visited[i]) {
                visited[i] = true
                arr[len] = i
                backTracking(i, len + 1)
                visited[i] = false
            }
        }
    }

    backTracking(1, 0)
    println(sb)
}
```


# 해설
* 백트래킹 문제
* 이전 `N과 M (1)` 문제에서 풀었던 두 가지 방식을 결합하여 풀었음
* 오름차순 정렬이 조건이므로 함수 내에서 `for문`을 돌 때 원래 값보다 작은 값이 있으면 안됨
  `idx` 인수를 만들어서 현재 `i`값을 다음 함수에 넘겨줌
  다음 함수에서 `for문`을 돌 때 `i`보다 작은 값이 들어가지 않도록 함