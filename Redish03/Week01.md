## 기간
**24.09.23 ~ 24.09.29**

## 문제

### 7579 - 앱
- DP, 배낭 문제
<details>
<summary> 코드 & 설명 </summary>
    <div>
    - 배낭 문제를 조금만 응용한 문제.
    
``` c++
    #include <iostream>
    #include <algorithm>
    
    using namespace std;
    
    int N, M;
    long long dp[101][10001];
    int byte[101];
    int cost[101];
    
    int main()
    {
        cin >> N >> M;
        
        for(int i = 1; i <= N; i++) {
            cin >> byte[i];
        }
        for(int i = 1; i <= N; i++) {
            cin >> cost[i];
        }
        
        long long ans = 98765321987;
        for(int i = 1; i <= N; i++) {
            for(int j = 0; j <= 10001; j++) { // 모든 비용들의 합으로 바꿔도 괜찮음.
                if(j >= cost[i]){
                    dp[i][j] = max(dp[i - 1][j], dp[i - 1][j-cost[i]] + byte[i]);     
                    if(dp[i][j] >= M) {
                        ans = min(ans, (long long)j);
                    }
                }
                else dp[i][j] = dp[i - 1][j];
            }
        }
        
        cout << ans;
        
        return 0;
    }
    
```
</div>
</details>

### 14852 - 타일 채우기 3

- DP
<details>
<summary> 코드 & 설명 </summary>
    <div>
    - 점화식이 아래와 같이 나온다.
    - $DP(N) = 2 * DP(N - 1) + 3 * DP(N - 2) + 2 * SUM(N - 3)$
    - for문을 이중으로 돌리면 시간 복잡도가 O(N^2)가 되므로, O(N)으로 만들기 위해 2차원 배열 또는 1차원 배열 두 개를 이용한다.
    
``` c++
#include<iostream>

using namespace std;

long long dp[1000001];
long long sum[1000001];

long long DP(int x) {
    dp[0] = 0;
    dp[1] = 2;
    dp[2] = 7;
    sum[0] = 0;
    sum[1] = 2;
    sum[2] = 9;
    
    for(int i = 3; i <= x; i++) {
        dp[i] = (2 * dp[i - 1] + 3 * dp[i - 2] + 2 * sum[i - 3] + 2) % 1000000007;
        sum[i] = (dp[i] + sum[i - 1]) % 1000000007;
    }
    
    return dp[x];
}

int main()
{
    int N;
    cin >> N;
    cout << DP(N);
    return 0;
}

```
        
</div>

</details>

## 공부한 내용
- <개발자의 글쓰기> 책 완독
- 배낭 알고리즘 다시 공부함


## 다음주 목표
- 3km 뜀걸음 4일
- 알고리즘 5문제
- <도파민네이션> 읽기
- <프롬프트 엔지니어링> 블로그 쓰기

## 특이사항
- 
