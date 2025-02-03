# 문제
백준 - N과 M (1) (S3)
https://www.acmicpc.net/problem/15649


# 풀이

```Kotlin
// 성공 - 256ms
import java.lang.StringBuilder

fun main() {
    val br = System.`in`.bufferedReader()
    val (n, m) = br.readLine().split(" ").map { it.toInt() }

    // 선택한 숫자를 담을 배열
    val arr = Array(m) { 0 }
    // 방문 여부 저장 배열
    val visited = BooleanArray(n + 1) { false }

    // 한번에 출력하기 위해 선택한 숫자를 쌓을 StringBuilder
    val sb = StringBuilder()

    fun backTracking(len: Int) {
        // 문제에서 요구하는 수열 길이와 쌓인 숫자의 길이가 같다면
        if (len == m) {
            // for문 돌면서 배열에 저장된 숫자를 StringBuilder에 저장
            arr.forEach {
                sb.append("$it ")
            }
            sb.append("\n")
            // 함수 탈출
            return
        }

        // 1부터 n까지 for문 돌면서
        for (i in 1 .. n) {
            // 방문하지 않은 숫자가 있으면 방문
            if (!visited[i]) {
                visited[i] = true
                // arr 배열에 수열 쌓기
                arr[len] = i
                // 다음 숫자 선택을 위해 재귀함수 호출
                backTracking(len + 1)
                // 함수에서 나오면 나중에 다시 사용하기 위해 숫자를 선택하지 않은 상태로 변경
                visited[i] = false
            }
        }
    }

    backTracking(0)
    println(sb)
}
```

```kotlin
// 성공 - 212ms
fun main() {
    val br = System.`in`.bufferedReader()
    val (n, m) = br.readLine().split(" ").map { it.toInt() }

    val arr = Array(n + 1) { i -> i }
    val visited = BooleanArray(n + 1) { false }

    val sb = StringBuilder()

    fun backTracking(len: Int, str: String) {
        if (len == m) {
            /* 여기만 StringBuilder 추가 */
            sb.append(str)
            sb.append("\n")
            return
        }

        for (i in 1 .. n) {
            if (!visited[i]) {
                visited[i] = true

                if (len == 0) {
                    backTracking(1, arr[i].toString())
                } else {
                    backTracking(len + 1, "$str ${arr[i]}")
                }

                visited[i] = false
            }
        }
    }

    backTracking(0, "")
    println(sb)
}
```


# 해설
* 백트래킹(`BackTracking`)?
  해를 찾는 도중 해가 절대 될 수 없다고 판단되면, 되돌아가서 해를 다시 찾아가는 기법
    * `DFS`와 백트래킹의 차이
      `DFS`는 가능한 모든 경로를 탐색하는데, 때로는 불필요한 경로까지 모두 탐색하며 경우의 수를 최적으로 줄이지 못할 수 있다.
      그러나 백트래킹은 해를 찾는 도중 막히면 더 이상 깊이 들어가지 않고 이전 단계로 돌아가서 다른 해를 찾아 탐색한다.

* 중복을 허용하지 않는 수열이므로 `visited` 배열을 사용하여 방문여부 체크
* `len`을 함수의 인수로 추가하여 현재까지 선택한 수열의 길이를 체크
  현재까지 선택한 수열의 길이와 문제에서 제공하는 수열의 길이가 같아지면 값을 담은 배열을 출력
* 방문하지 않은 노드들을 `for문`으로 검사하며 숫자를 이어붙여 재귀적으로 노드 탐

* `print()` 함수를 반복하여 사용하는 것보다 `StringBuilder`로 값을 쌓은 후 한번에 출력하는 것이 시간이 훨씬 더 절약된다.
    * 이 때, `StringBuilder`를 사용하기 위해서 `import`할 필요는 없다.