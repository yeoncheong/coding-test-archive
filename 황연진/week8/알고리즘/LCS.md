# 문제
백준 - LCS (G5)
https://www.acmicpc.net/problem/9251


# 풀이

```Kotlin
import kotlin.math.*

fun main() {
    val br = System.`in`.bufferedReader()
    val a = br.readLine()
    val b = br.readLine()
    // a[0..i-1]과 b[0..j-1]까지 봤을 때의 최장 공통 부분 수열의 길이
    val dp = Array(a.length + 1) { IntArray(b.length + 1) { 0 } }

    for (i in 1 .. a.length) {
        for (j in 1 .. b.length) {
            // 비교해서 글자가 같으면
            if (a[i - 1] == b[j - 1]) {
                // 해당 글자도 최장 문자열에 포함되므로 직전값 + 1
                dp[i][j] = dp[i - 1][j - 1] + 1
            } else {
                // 글자가 다르면 글자 하나 버렸을 때의 최장 LCS값 가져오기
                dp[i][j] = max(dp[i - 1][j], dp[i][j - 1])
            }
        }
    }

    println(dp[a.length][b.length])
}
```


# 해설
* `LCS` (`Longest Common Sequence`)
* `이중 for문`을 돌면서 같은 글자를 만나면 해당 글자도 최장 수열에 포함되므로 직전 `dp`값에서 `+1`
* 글자가 다르면 수열에 포함되지 않으므로 글자 하나 버리고 둘 중 어떤 것이 더 긴지 `max`로 비교
    * 이 때 직전값은 `for문` 돌면서 앞에서부터 `dp`값이 채워지므로 구해져있음