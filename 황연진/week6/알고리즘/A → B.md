# 문제
백준 - A → B (S2)
https://www.acmicpc.net/problem/16953


# 풀이

```Kotlin
fun main() {
    val br = System.`in`.bufferedReader()
    var (a, b) = br.readLine().split(" ").map { it.toInt() }

    var count = 0

    while (a != b) {
        // b가 a보다 작아지면 더 이상 나눠지지 않으므로 -1 출력
        if (a > b) {
            print(-1)
            return
        }

        if (b % 10 == 1) { // 끝에 1을 붙인다는 것은 10으로 나눴을 때 나머지가 1이라는 것
            b /= 10
        } else if (b % 2 == 0) { // 2로 나눠진다면
            b /= 2
        } else { // 그 외의 조건은 무조건 안 나눠지는 것이므로 -1 출력
            println(-1)
            return
        }
        count++
    }

    // 연산 최솟값에 +1
    print(count + 1)
}
```

```kotlin
// 실패 - IDE에서 돌리면 올바른 답 나옴
// 범위가 큰 건 배열로 안된다고 함.. 런타임에러 (NZEC)

import java.util.*

fun main() {
    val br = System.`in`.bufferedReader()
    val (a, b) = br.readLine().split(" ").map { it.toLong() }

    val graph = Array(b.toInt() + 1) { 0L }

    fun BFS(x: Long) {
        val queue: Queue<Long> = LinkedList()
        queue.add(x)

        while (queue.isNotEmpty()) {
            val cur = queue.poll()

            if (cur == b) break

            for (i in 0 until 2) {
                when (i) {
                    0 -> { // 곱하기 2
                        if (cur * 2 < graph.size && graph[cur.toInt() * 2] == 0L) {
                            queue.offer(cur * 2)
                            graph[cur.toInt() * 2] = graph[cur.toInt()] + 1
                        }
                    }
                    1 -> { // 곱하기 10 플러스 1
                        if (cur * 10 + 1 < graph.size && graph[cur.toInt() * 10 + 1] == 0L) {
                            queue.offer(cur * 10 + 1)
                            graph[cur.toInt() * 10 + 1] = graph[cur.toInt()] + 1
                        }
                    }
                }
            }
        }
    }

    BFS(a)
    if (graph[b.toInt()] == 0L) {
        println("-1")
    } else {
        println(graph[b.toInt()] + 1)
    }
}
```


# 해설
* 기본적으로 그리디 문제이나, `BFS`, `DP`로도 풀 수 있다.
* 조건이 `x2`거나 `x10+1`
    * `10`으로 나눴을 때 나머지가 `1`인 경우
    * `2`로 나눴을 때 나머지가 `0`인 경우
    * 두 경우가 반복되다가 `a`와 `b` 값이 동일해지면 `최솟값 + 1` 하여 출력
    * 만약 두 경우에 해당되지 않을 경우 조건이 일치하지 않으므로 `-1` 출력	