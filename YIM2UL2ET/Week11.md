## 기간
**24.12.02 ~ 24.12.08**

## 풀었던 문제

### [BOJ 1613 - 역사](https://www.acmicpc.net/problem/1613)
<details>
<summary>보기</summary> 

- 정보
    - Tier: GoldⅢ
    - Tag: 플로이드 워셜
 
- 코드
  - ```cpp
    #include <iostream>
    #include <vector>
    
    using namespace std;
    
    int N, K, S;
    vector <vector <bool>> dp;  // dp[i][j] = i가 가보다 먼저 발생했는지 여부
    
    void floyd() {
        for (int m = 1; m <= N; m++) {
            for (int s = 1; s <= N; s++) {
                for (int e = 1; e <= N; e++) {
                    if (dp[s][m] && dp[m][e]) {
                        dp[s][e] = true;
                    }
                }
            }
        }
    }
    
    int main() {
        // fastIO
        ios_base::sync_with_stdio(false);
        cin.tie(NULL); cout.tie(NULL);
    
        // init && input
        cin >> N >> K;
    
        dp.resize(N + 1, vector <bool> (N + 1, false));
        for (int i = 1; i <= N; i++) {
            dp[i][i] = true;
        }
    
        int u, v;
        for (int i = 0; i < K; i++) {
            cin >> u >> v;
            dp[u][v] = true;
        }
    
        // solve
        floyd();
    
        cin >> S;
        for (int i = 0; i < S; i++) {
            cin >> u >> v;
            if (dp[u][v] && !dp[v][u]) {
                cout << -1 << '\n';
            } else if (!dp[u][v] && dp[v][u]) {
                cout << 1 << '\n';
            } else {
                cout << 0 << '\n';
            }
        }
        return 0;
    }
    ```

</details>

### [BOJ 2240 - 자두나무](https://www.acmicpc.net/problem/2240)
<details>
<summary>보기</summary> 

- 정보
    - Tier: GoldⅤ
    - Tag: DP
 
- 코드
  - ```cpp
    #include <iostream>
    #include <vector>
    
    using namespace std;
    
    int T, W;
    vector <pair <int, int>> drop;
    vector <vector <pair <int, int>>> dp;
    
    int getMaxV(int curL, int t, int w) {
        if (t > T) return 0;
        
        int &let = (!curL ? dp[t][w].first : dp[t][w].second);
        int add = (!curL ? drop[t].first : drop[t].second);
        if (let == -1) {
            let = getMaxV(curL, t + 1, w) + add;
            if (w > 0) {
                let = max(let, getMaxV((curL + 1) % 2, t + 1, w - 1) + add);
            }
        }
        return let;
    }
    
    int main() {
        cin >> T >> W;
        drop.resize(T + 1);
        dp.resize(T + 1, vector <pair <int, int>> (W + 1, {-1, -1}));
    
        int n;
        for (int i = 1; i <= T; i++) {
            cin >> n;
            if (n == 1) {
                drop[i].first++;
            } else {
                drop[i].second++;
            }
        }
    
        cout << getMaxV(0, 0, W);
        return 0;
    }
    ```

</details>

### [BOJ 2281 - 데스노트](https://www.acmicpc.net/problem/2281)
<details>
<summary>보기</summary> 

- 정보
    - Tier: GoldⅢ
    - Tag: DP
 
- 코드
  - ```cpp
    #include <iostream>
    #include <vector>
    
    using namespace std;
    
    int N, M;
    vector <int> nameLen;
    vector <vector <int>> dp;
    
    int solve(int i, int j) {
        if (i == N) return 0;
    
        int &let = dp[i][j];
        if (let == -1) {
            if (nameLen[i] + 1 <= j) {
                let = min(solve(i + 1, M - nameLen[i]) + (j * j), solve(i + 1, j - (nameLen[i] + 1)));
            } else {
                let = solve(i + 1, M - nameLen[i]) + (j * j);
            }
        }
        return let;
    }
    
    int main() {
        cin >> N >> M;
    
        nameLen.resize(N);
        dp.resize(N, vector <int> (M + 1, -1));
    
        for (auto &n : nameLen) {
            cin >> n;
        }
    
        cout << solve(1, M - nameLen.front());
        return 0;
    }
    ```

</details>

### [BOJ 17485 - 진우의 달 여행 (Large)](https://www.acmicpc.net/problem/17485)
<details>
<summary>보기</summary> 

- 정보
    - Tier: GoldⅤ
    - Tag: DP
 
- 코드
  - ```cpp
    #include <iostream>
    #include <vector>
    
    using namespace std;
    
    int N, M;
    vector <vector <int>> cost;
    vector <vector <vector <int>>> dp;  // dp[i][j][k] = i행 j열에서 직전방향이 k였을 때 최소 값
    
    int solve(int i, int j, int k) {
        if (i > N) {
            return 0;
        } else if (j == -1 || j == M) {
            return 1e9;
        }
    
        int &let = dp[i][j][k];
        if (let == -1) {
            let = cost[i][j];
            if (k == 0) {
                let += min(solve(i + 1, j, 1), solve(i + 1, j + 1, 2));
            } else if (k == 1) {
                let += min(solve(i + 1, j - 1, 0), solve(i + 1, j + 1, 2));
            } else if (k == 2) {
                let += min(solve(i + 1, j - 1, 0), solve(i + 1, j, 1));
            }
        }
        return let;
    }
    
    int main() {
        cin >> N >> M;
    
        cost.resize(N + 1, vector <int> (M));
        dp.resize(N + 1, vector <vector <int>> (M, vector <int> (3, -1)));
    
        for (int i = 1; i <= N; i++) {
            for (int j = 0; j < M; j++) {
                cin >> cost[i][j];
            }
        }
    
        int ans = 1e9;
        for (int i = 0; i < M; i++) {
            for (int j = 0; j <= 2; j++) {
                ans = min(ans, solve(1, i, j));
            }
        }
    
        cout << ans;
        return 0;
    }
    ```

</details>

## 공부한 내용
- 없음

## 다음주 목표
- 종만북 3부 완독
- C++ 공부

## 특이사항
- 12/01 ~ 12/09 휴가
- 이번주 문제들은 타임라인, 풀이 및 회고 생략
