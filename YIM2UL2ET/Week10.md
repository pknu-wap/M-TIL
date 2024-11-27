## 기간
**24.11.25 ~ 24.12.01**

## 풀었던 문제

### [BOJ 3678 - 카탄의 개척자](https://www.acmicpc.net/problem/3678)
<details>
<summary>보기</summary> 

- 정보
    - Tier: GoldⅠ
    - Tag: implementation

- 타임라인
    - Problem Open: 11/24 22:40
    - Tag Open: 11/25 07:20
    - Solve: --/-- --:--

- 풀이
    - 깡으로 해보는중

- 회고
    - 시뮬레이션 / 구현인 점 짐작은 하고 있었지만, 직접 태그를 확인해보고는 경악했다.
    - 시간이 오래 걸릴 것 같아 이번주 까지 푸는걸 목표로 잡고 임시적으로 유기
 
- 코드
  - ```cpp
    코드
    ```

</details>

### [BOJ 2698 - 인접한 비트의 개수](https://www.acmicpc.net/problem/2698)
<details>
<summary>보기</summary> 

- 정보
    - Tier: GoldⅣ
    - Tag: DP

- 타임라인
    - Problem Open: 11/25 22:10
    - Tag Open: 11/25 22:30
    - Solve: 11/25 23:01

- 풀이
    - $DP[i][N][K] =$ 첫 비트가 $i$이고, 크기가 $N$, 인접 비트의 개수가 $K$인 수열의 개수 $i \in \lbrace0, 1\rbrace$
    - <img src="http://latex.codecogs.com/png.latex?\dpi{110}\bg_white 
          \begin{cases}
          DP[i][N][K] = DP[i-1][N-1][K] + DP[i][N-1][K-1] & i=1 \\
          DP[i][N][K] = DP[i][N-1][K] + DP[i+1][N-1][K] & i=0
          \end{cases}
          "/>
    - 기저사례: $DP[0][1][0] = DP[1][1][0] = 1$

- 회고
    - 점화식 구현에서 애를 먹었다. 최적화 문제가 아닌 새로운 유형의 DP 문제로 잘 연구해서 쿼리에 추가하기
    - [바텀업 방식 코드](https://www.acmicpc.net/source/79130749)
 
- 코드
  - ```cpp
    #include <iostream>
    #include <vector>
    
    using namespace std;
    
    vector <vector <int>> bit0DP(101, vector <int> (101, -1));
    vector <vector <int>> bit1DP(101, vector <int> (101, -1));
    
    int get0BitDP(int N, int K);
    int get1BitDP(int N, int K);
    
    int get0BitDP(int N, int K) {
        if (N <= K) return 0;
    
        if (bit0DP[N][K] == -1) {
            bit0DP[N][K] = get0BitDP(N - 1, K) + get1BitDP(N - 1, K);
        }
        return bit0DP[N][K];
    }
    
    int get1BitDP(int N, int K) {
        if (N <= K) return 0;
    
        if (bit1DP[N][K] == -1) {
            bit1DP[N][K] = get0BitDP(N - 1, K) + get1BitDP(N - 1, K - 1);
        }
        return bit1DP[N][K];
    }
    int main() {
        ios_base::sync_with_stdio(false);
        cin.tie(NULL); cout.tie(NULL);
    
        int tc;
        cin >> tc;
    
        bit0DP[1][0] = 1;
        bit1DP[1][0] = 1;
    
        int N, K;
        while (tc--) {
            cin >> N >> K;
            cout << get0BitDP(N, K) + get1BitDP(N, K) << '\n';
        }
        return 0;
    }
    ```

</details>

### [BOJ 15319 - 동혁이의 생일선물](https://www.acmicpc.net/problem/15319)
<details>
<summary>보기</summary> 

- 정보
    - Tier: GoldⅣ
    - Tag: Divide_and_Conquer

- 타임라인
    - Problem Open: 11/26 22:00
    - Tag Open: --/-- --:--
    - Solve: 11/26 23:28

- 풀이
    - $n^m + n^{m-1} + n^{m-2} + \dots + 1 < n^{m+1} (n \ge 2)$
    - 이를 숙지하여 오름차순 나열하여 관찰
    - $i = max(j | 2^j - 1 < k) + 1$라고 할 때 아래와 같음
    - <img src="http://latex.codecogs.com/png.latex?\dpi{110}\bg_white 
          f(x, k) = 
          \begin{cases}
          x^{i-1} + f(x, k-2^{i-1}) & k > 0 \\
          0 & k \le 0
          \end{cases}
          "/>
    - 이를 재귀함수로 구현

- 회고
    - 나는 여전히 멍청하다는 것을 깨닫게 해준 문제
    - 구현 식을 세우고, 이를 어떻게 구현할 것인지 까지 확실히 해두기
    - [mod 연산의 특징](https://developer-mac.tistory.com/84) 제대로 숙지 (제발..)
    - [깔끔한 풀이](https://www.acmicpc.net/source/78800490): 오름차순 나열했을 때 $k$를 2진수로 하여 i번째 비트가 켜져있으면 $ans = ans + n^i$
 
- 코드
  - ```cpp
    #include <iostream>

    #define MOD 1000000007
    
    using namespace std;
    
    long long pow(int n, int i) {
        long long result = 1;
        while(i--) {
            result = ((result % MOD) * (n % MOD)) % MOD;
        }
        return result;
    }
    
    long long getNum(int x, int k) {
        if (k <= 0) return 0;
    
        long long i = 1;
        while ((1 << i) - 1 < k) {
            i++;
        }
    
        return (pow(x, i-1) + getNum(x, k - (1 << (i-1)))) % MOD;
    }
    
    int main() {
        long long n, x, k, ans;;
        ans = 0;
    
        cin >> n;
        while (n--) {
            cin >> x >> k;
            ans += getNum(x, k);
            ans %= MOD;
        }
    
        cout << ans;
        return 0;
    }
    ```

</details>

### [BOJ 16211 - 백채원](https://www.acmicpc.net/problem/16211)
<details>
<summary>보기</summary> 

- 정보
    - Tier: GoldⅡ
    - Tag: Dijkstra

- 타임라인
    - Problem Open: 11/27 12:00
    - Tag Open: --/-- --:--
    - Solve: 11/27 21:37

- 풀이
    - 다익스트라에서 출발점을 여러 부분으로 하여 변형하여 풀이 (코드 참조)

- 회고
    - 실풀이 대략 80분
    - 열심히 연습하자.
 
- 코드
  - ```cpp
    #include <iostream>
    #include <algorithm>
    #include <vector>
    #include <queue>
    
    #define INF 1e9 * 2 + 1
    
    using namespace std;
    typedef long long ll;
    
    int N, M, K;
    vector <vector <pair <int, int>>> graph;
    vector <ll> runawayDist;
    vector <ll> chaserDist;
    
    void dijkstra(vector <ll> &dist) {
        priority_queue <pair <ll, int>> pq;
        for (int i = 0; i < int(dist.size()); i++) {
            if (dist[i] == 0) {
                pq.push({0, i});
            }
        }
    
        while(!pq.empty()) {
            int s = pq.size();
    
            for (int i = 0; i < s; i++) {
                int curNode = pq.top().second;
                ll curDist = -pq.top().first;
                pq.pop();
    
                for (auto &nxt : graph[curNode]) {
                    int nxtNode = nxt.second;
                    ll nxtDist = curDist + nxt.first;
                    if (nxtDist < dist[nxtNode]) {
                        dist[nxtNode] = nxtDist;
                        pq.push({-nxtDist, nxtNode});
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
        cin >> N >> M >> K;
    
        graph.resize(N + 1);
        runawayDist.resize(N + 1, INF);
        chaserDist.resize(N + 1, INF);
    
        int u, v, w;
        for (int i = 0; i < M; i++) {
            cin >> u >> v >> w;
            graph[u].push_back({w, v});
            graph[v].push_back({w, u});
        }
    
        int p;
        runawayDist[1] = 0;
        for (int i = 0; i < K; i++) {
            cin >> p;
            chaserDist[p] = 0;
        }
    
        // solve
        dijkstra(runawayDist);
        dijkstra(chaserDist);
    
        vector <int> ans;
        for (int i = 2; i <= N; i++) {
            if (runawayDist[i] < chaserDist[i]) {
                ans.push_back(i);
            }
        }
    
        // output
        if (ans.size() == 0) cout << 0;
    
        sort(ans.begin(), ans.end());
        for (auto &n : ans) {
            cout << n << ' ';
        }
    
        return 0;
    }
    ```

</details>

### [BOJ 22115 - 창영이와 커피](https://www.acmicpc.net/problem/22115)
<details>
<summary>보기</summary> 

- 정보
    - Tier: GoldⅡ
    - Tag: DP

- 타임라인
    - Problem Open: 11/27 22:10
    - Tag Open: --/-- --:--
    - Solve: 11/27 22:23

- 풀이
    - 0-1 냅색문제를 알고있다면 쉽게 풀리는 문제

- 회고
    - 익숙한 맛 (영양가는 X)
 
- 코드
  - ```cpp
    #include <iostream>
    #include <vector>
    
    using namespace std;
    
    int main() {
        // fastIO
        ios_base::sync_with_stdio(false);
        cin.tie(NULL); cout.tie(NULL);
    
        // init && input
        int N, K;
        cin >> N >> K;
    
        vector <vector <int>> dp(N + 1, vector <int> (K + 1, 1e9));
        vector <int> coffee(N + 1);
    
        for (int i = 1; i <= N; i++) {
            cin >> coffee[i];
        }
    
        // solve
        dp[0][0] = 0;
        for (int i = 1; i <= N; i++) {
            for (int j = 0; j <= K; j++) {
                if (coffee[i] <= j) {
                    dp[i][j] = min(dp[i - 1][j], dp[i - 1][j - coffee[i]] + 1);
                } else {
                    dp[i][j] = dp[i - 1][j];
                }
            }
        }
    
        // output
        cout << (dp[N][K] != 1e9 ? dp[N][K] : -1);
        return 0;
    }
    ```

</details>

### [BOJ 1062 - 가르침](https://www.acmicpc.net/problem/1062)
<details>
<summary>보기</summary> 

- 정보
    - Tier: GoldⅣ
    - Tag: Backtracking

- 타임라인
    - Problem Open: 11/27 23:30?
    - Tag Open: --/-- --:--
    - Solve: 11/27 07:36

- 풀이
    - 비트마스킹 활용한 백트래킹
    - $i$번째 알파벳을 가르친 여부를 $i$번째 비트에 저장
    - $and$ 연산으로 알파벳을 완성할 수 있는지 여부 확인하여 이에 대한 $max$값을 찾기
    - $K \le 4$일때는 무슨 수를 사용하더라도 알파벳 완성이 안된다는 것 주의

- 회고
    - 설계 잘하자
 
- 코드
  - ```cpp
    #include <iostream>
    #include <vector>
    
    using namespace std;
    
    int N, K;
    vector <int> words;
    
    int backtracking(int bits, int idx, int n) {
        int res = 0;
        if (n <= 0 || idx == 27) {
            for (int i = 0; i < N; i++) {
                if ((bits & words[i]) == words[i]) res++;
            }
        } else {
            for (int i = idx; i <= 26; i++) {
                if (bits & (1 << i)) continue;
                int newBits = (bits | (1 << i));
                res = max(res, backtracking(newBits, i + 1, n - 1));
            }
        }
        return res;
    }
    
    int main() {
        ios_base::sync_with_stdio(false);
        cin.tie(NULL); cout.tie(NULL);
    
        cin >> N >> K;
        words.resize(N, 0);
    
        string str;
        for (int i = 0; i < N; i++) {
            cin >> str;
            for (auto &ch : str) {
                words[i] |= (1 << (ch - 'a'));
            }
        }
        
        if (K < 5) {
            cout << 0;
        } else {
            cout << backtracking(532741, 0, K - 5);
        }
        return 0;
    }
    ```

</details>

## 공부한 내용
- 뭘했을까

## 다음주 목표
- 뭘해야할까

## 특이사항
- 12/01 ~ 12/09 휴가
