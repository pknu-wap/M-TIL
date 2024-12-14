## 기간
**24.12.09 ~ 24.12.15**

## 풀었던 문제

### [BOJ 15683 - 감시](https://www.acmicpc.net/problem/15683)
<details>
<summary>보기</summary> 

- 정보
    - Tier: GoldⅢ
    - Tag: 구현

- 타임라인
    - Problem Open: 12/10 18:30?
    - Tag Open: --/-- --:--
    - Solve: 12/10 20:11

- 풀이
    - 깡구현

- 회고
    - 함수명 잘짓기, 범위 지정시 한번 더 보기 (for문 사용시)
    - 구현은 설계다
 
- 코드
  - ```cpp
    #include <iostream>
    #include <vector>
    
    using namespace std;
    
    int N, M;
    
    vector <vector <vector <int>>> direction {
        {{1}, {2}, {3}, {4}}, 
        {{1, 3}, {2, 4}},
        {{1, 2}, {2, 3}, {3, 4}, {4, 1}}, 
        {{1, 2, 3}, {2, 3, 4}, {3, 4, 1}, {4, 1, 2}}, 
        {{1, 2, 3, 4}}
    };
    
    vector <vector <char>> fillingField(vector <vector <char>> field, int r, int c, vector <int> &vec) {
        for (auto &d : vec) {
            if (d == 1) {   // left
                for (int i = c; i >= 0; i--) {
                    if (field[r][i] == '0') {
                        field[r][i] = '#';
                    } else if (field[r][i] == '6') {
                        break;
                    } 
                }
            } else if (d == 2) {    // up
                for (int i = r; i >= 0; i--) {
                    if (field[i][c] == '0') {
                        field[i][c] = '#';
                    } else if (field[i][c] == '6') {
                        break;
                    } 
                }
            } else if (d == 3) {    // right
                for (int i = c; i < M; i++) {
                    if (field[r][i] == '0') {
                        field[r][i] = '#';
                    } else if (field[r][i] == '6') {
                        break;
                    } 
                }
            } else if (d == 4) {    // down
                for (int i = r; i < N; i++) {
                    if (field[i][c] == '0') {
                        field[i][c] = '#';
                    } else if (field[i][c] == '6') {
                        break;
                    } 
                }
            }
        }
        return field;
    }
    
    int checkField(vector <vector <char>> &field) {
        int result = 0;
        for (auto &row : field) {
            for (auto &ch : row) {
                if (ch == '0') result++;
            }
        }
        return result;
    }
    
    int dfs(vector <vector <char>> &field, int r, int c) {
        int result = 1e9;
    
        for (int k = r * M + c; k < N * M; k++) {
            int i = k / M, j = k % M;
            if ('1' > field[i][j] || field[i][j] > '5') continue;
            
            for (auto &v : direction[field[i][j] - '1']) {
                auto newField = fillingField(field, i, j, v);
                result = min(result, dfs(newField, i, j + 1));
            }
            return result;
        }
    
        return checkField(field);
    }
    
    int main() {
        ios_base::sync_with_stdio(false);
        cin.tie(NULL); cout.tie(NULL);
    
        cin >> N >> M;
        vector <vector <char>> field(N, vector <char> (M));
        for (auto &row : field) {
            for (auto &ch : row) {
                cin >> ch;
            }
        }
    
        cout << dfs(field, 0, 0);
        return 0;
    }
    ```

</details>

### [BOJ 1135 - 뉴스 전하기](https://www.acmicpc.net/problem/1135)
<details>
<summary>보기</summary> 

- 정보
    - Tier: GoldⅡ
    - Tag: tree_dp, greedy

- 타임라인
    - Problem Open: 12/10 22:15?
    - Tag Open: --/-- --:--
    - Solve: 12/10 22:46

- 풀이
    - 거꾸로 역행해서 리프노드부터 시작하여 올라가는 형식으로 풀이
    - $i$번 노드의 차수가 $0$이 되면 $parent[i]$번노드의 차수를 $-1$
    - 이때 전화는 중복으로 걸 수 없으므로 중복되지 않도록 큐와 해시맵을 적절히 사용

- 회고
    - 나중가서 해당 문제가 한번 더 나오면 이런 풀이가 생각날까..? -> 한번 더보자.
    - 코드 정리좀 해야할듯
 
- 코드
  - ```cpp
    #include <iostream>
    #include <queue>
    #include <unordered_set>
    #include <vector>
    
    using namespace std;
    
    int N;
    vector <int> parent;
    vector <int> degree;
    
    int main() {
        cin >> N;
    
        parent.resize(N);
        degree.resize(N);
    
        cin >> parent[0];
        for (int i = 1; i < N; i++) {
            cin >> parent[i];
            degree[parent[i]]++;
        }
    
        int ans = 0;
        unordered_set <int> isVst;
        while (degree[0] != 0) {
            unordered_set <int> uos;
            queue <int> que;
    
            for (int i = 1; i < N; i++) {
                if (degree[i] == 0 && isVst.find(i) == isVst.end() && uos.find(parent[i]) == uos.end() && degree[parent[i]] > 0) {
                    que.push(parent[i]);
                    uos.insert(parent[i]);
                    isVst.insert(i);
                }
            }
    
            while (!que.empty()) {
                degree[que.front()]--;
                que.pop();
            }
            
            ans++;
        }
    
        cout << ans;
        return 0;
    }
    ```

</details>

### [BOJ 2211 - 네트워크 복구](https://www.acmicpc.net/problem/2211)
<details>
<summary>보기</summary> 

- 정보
    - Tier: GoldⅡ
    - Tag: dijkstra

- 타임라인
    - Problem Open: --/-- -:--
    - Tag Open: --/-- --:--
    - Solve: 12/11 12:18

- 풀이
    - 다익스트라 후 우선순위 큐 사용하여 회선 복구 (정답 출력)

- 회고
    - 없
 
- 코드
  - ```cpp
	#include <iostream>
    #include <queue>
    #include <vector>
    
    using namespace std;
    
    vector <vector <pair <int, int>>> graph;
    vector <int> dist;
    vector <bool> isConnect;
    vector <pair <int, int>> ans;
    
    void dijkstra() {
        priority_queue <pair <int, int>> pq;
    
        dist[1] = 0;
        pq.push({0, 1});
    
        while (!pq.empty()) {
            int cnt = pq.size();
            while (cnt--) {
                int curDist = -pq.top().first;
                int curNode = pq.top().second;
                pq.pop();
    
                if (curDist > dist[curNode]) continue;
                for (auto &p : graph[curNode]) {
                    int nxtDist = p.first + curDist;
                    int nxtNode = p.second;
    
                    if (nxtDist < dist[nxtNode]) {
                        dist[nxtNode] = nxtDist;
                        pq.push({-nxtDist, nxtNode});
                    }
                }
            }
        }
    }
    
    void solve() {
        priority_queue <pair <int, int>> pq;
    
        isConnect[1] = true;
        pq.push({0, 1});
    
        while (!pq.empty()) {
            int curDist = pq.top().first;
            int curNode = pq.top().second;
            pq.pop();
            
            for (auto &p : graph[curNode]) {
                int nxtDist = p.first + curDist;
                int nxtNode = p.second;
                if (!isConnect[nxtNode] && dist[nxtNode] == nxtDist) {
                    isConnect[nxtNode] = true;
                    ans.push_back({curNode, nxtNode});
                    pq.push({nxtDist, nxtNode});
                }
            }
        }
    }
     
    int main() {
        // fastIO
        ios_base::sync_with_stdio(false);
        cin.tie(NULL); cout.tie(NULL);
    
        // init && input
        int N, M;
        cin >> N >> M;
    
        graph.resize(N + 1);
        dist.resize(N + 1, 1e9);
        isConnect.resize(N + 1, false);
    
        int u, v, w;
        for (int i = 0; i < M; i++) {
            cin >> u >> v >> w;
            graph[u].push_back({w, v});
            graph[v].push_back({w, u});
        }
    
        // solve
        dijkstra();
        solve();
        
        cout << ans.size() << '\n';
        for (auto &p : ans) {
            cout << p.first << ' ' << p.second << '\n';
        }
    
        return 0;
    }
    ```

</details>

### [BOJ 11444 - 피보나치 수 6](https://www.acmicpc.net/problem/11444)
<details>
<summary>보기</summary> 

- 정보
    - Tier: GoldⅡ
    - Tag: 분할정복

- 타임라인
    - Problem Open: --/-- -:--
    - Tag Open: --/-- --:--
    - Solve: 12/12 18:38

- 풀이
    - 분할정복을 사용하는 행렬의 거듭제곱으로 DP 풀이

- 회고
    - 연습
 
- 코드
  - ```cpp
    #include <iostream>
    #include <vector>
    
    #define MOD 1000000007
    
    using namespace std;
    
    vector <vector <long long>> mulMatrix(vector <vector <long long>> W1, vector <vector <long long>> W2) {
        int n = W1.size(), m = W2.back().size(), l = W1.back().size();
        vector <vector <long long>> result(n, vector <long long> (m));
    
        for (int i = 0; i < n; i++) {
            for (int j = 0; j < m; j++) {
                for (int k = 0; k < l; k++) {
                    result[i][j] += ((W1[i][k] % MOD) * (W2[k][j] % MOD)) % MOD;
                    result[i][j] %= MOD;
                }
            }
        }
        return result;
    }
    
    vector <vector <long long>> powMatrix(vector <vector <long long>> &W, long long n) {
        if (n == 1) {
            return W;
        } else if (n % 2 != 0) {
            return mulMatrix(powMatrix(W, n - 1), W);
        } else {
            auto newW = powMatrix(W, n / 2);
            return mulMatrix(newW, newW);
        }
    }
    
    int main() {
        long long n;
        vector <vector <long long>> fibo{{0}, {1}};
        vector <vector <long long>> W{{0, 1}, {1, 1}};
    
        cin >> n;
        if (n <= 1) {
            cout << n;
        } else {
            cout << mulMatrix(powMatrix(W, n-1), fibo).back().back();
        }
        
        return 0;
    }
    ```

</details>

### [BOJ 3197 - 백조의 호수](https://www.acmicpc.net/problem/3197)
<details>
<summary>보기</summary> 

- 정보
    - Tier: Platinum Ⅴ
    - Tag: bfs, union_find

- 타임라인
    - Problem Open: --/-- -:--
    - Tag Open: --/-- --:--
    - Solve: 12/13 12:48

- 풀이
    - 1. 필드를 입력받는다. 이떄 int형 배열로 변환하여 입력받고, 백조의 위치는 따로 저장해둔다.
	- 2. bfs를 활용하여 물의 집합을 양의 정수로 표현한다. 이때 field에는 int형 정수로 표현해주고, parent 배열을 집합의 수만큼 초기화한다.
	- 3. 물에 닿아있는 얼음들은 배열에 -2로, 닿지 않은 배열은 -1로 표시해주고, -2인 얼음의 좌표는 queue에 넣어준다.
	- 4. 백조의 위치에 해당하는 두 집합(숫자)의 부모가 같아질 때 까지 일련의 작업을 반복한다. 해당 작업을 한 횟수가 정답이 된다.
		- a. 현재 queue에 저장되어 있는 얼음의 좌표에서 상하좌우 방향으로 -1로 표시된 얼음들은 -2로 표시, queue에 넣는 작업을 한다.
		- b. 현재 작업중인 얼음은 field에 맞닿아있는 물의 집합의 숫자로 변경한다. 만약 두개 이상이라면 union find를 활용하여 부모를 합치는 작업을 진행한다.

- 회고
    - 플래 정도 되니깐 두개 이상의 알고리즘을 활용해야 하는 문제가 많은듯
	- 디버깅 연습을 하자.
 
- 코드
  - ```cpp
    #include <iostream>
    #include <queue>
    #include <vector>
    
    using namespace std;
    
    int N, M;
    vector <vector <int>> field;
    vector <int> parent;
    vector <pair <int, int>> offset{{0,1}, {0,-1}, {1,0}, {-1,0}};
    
    int getParent(int n) {
        if (parent[n] == n) return n;
        return parent[n] = getParent(parent[n]);
    }
    
    void unionParent(int a, int b) {
        a = getParent(a);
        b = getParent(b);
    
        if (a > b) swap(a, b);
        parent[a] = b;
    }
    
    bool isCorrectLoc(int r, int c) {
        return (r < N && r >= 0 && c < M && c >= 0);
    }
    
    void bfs(int r, int c, int n) {
        queue <pair <int, int>> que;
    
        field[r][c] = n;
        que.push({r, c});
        while(!que.empty()) {
            for (const auto &p : offset) {
                int nxtR = p.first + que.front().first;
                int nxtC = p.second + que.front().second;
                if (!isCorrectLoc(nxtR, nxtC)) continue;
                
                if (field[nxtR][nxtC] == 0) {
                    que.push({nxtR, nxtC});
                    field[nxtR][nxtC] = n;
                }
            }
            que.pop();
        }
    }
    
    bool isConnect(int r, int c) {
        for (const auto &p : offset) {
            int nxtR = p.first + r;
            int nxtC = p.second + c;
            if (!isCorrectLoc(nxtR, nxtC)) continue;
    
            if (field[nxtR][nxtC] > 0) {
                return true;
            }
        }
        return false;
    }
    
    int solve(const vector <pair <int, int>> &start) {
        int k = 1;
        vector <int> startSet;
        queue <pair <int, int>> que;
    
        // init field
        for (int i = 0; i < N; i++) {
            for (int j = 0; j < M; j++) {
                if (field[i][j] == 0) {
                    bfs(i, j, k++);
                }
            }
        }
    
        for (int i = 0; i < N; i++) {
            for (int j = 0; j < M; j++) {
                if (field[i][j] == -1 && isConnect(i, j)) {
                    field[i][j] = -2;
                    que.push({i, j});
                }
            }
        }
    
        // init parent vector
        parent.resize(k + 1);
        for (int i = 0; i <= k; i++) {
            parent[i] = i;
        }
    
        // init startSet
        for (const auto &p : start) {
            startSet.push_back(field[p.first][p.second]);
        }
    
        // find answer
        int result = 0;
        while (getParent(startSet.front()) != getParent(startSet.back())) {
            int s = que.size();
            for (int i = 0; i < s; i++) {
                int r = que.front().first;
                int c = que.front().second;
                que.pop();
    
                for (const auto &p : offset) {
                    int nxtR = r + p.first;
                    int nxtC = c + p.second;
                    if (!isCorrectLoc(nxtR, nxtC)) continue;
    
                    if (field[nxtR][nxtC] == -1) {
                        field[nxtR][nxtC] = -2;
                        que.push({nxtR, nxtC});
                    } else if (field[nxtR][nxtC] > 0 && field[r][c] < 0) {
                        field[r][c] = field[nxtR][nxtC];
                    } else if (field[nxtR][nxtC] > 0 && field[r][c] > 0) {
                        unionParent(field[r][c], field[nxtR][nxtC]);
                    }
                }
            }
            result++;
        }
    
        return result;
    }
    
    int main() {
        // fastIO
        ios_base::sync_with_stdio(false);
        cin.tie(NULL); cout.tie(NULL);
    
        // init && input
        cin >> N >> M;
        field.resize(N, vector <int> (M));
    
        char ch;
        vector <pair <int, int>> start;
        for (int i = 0; i < N; i++) {
            for (int j = 0; j < M; j++) {
                cin >> ch;
                if (ch == 'X') {
                    field[i][j] = -1;
                } else if (ch == 'L') {
                    start.push_back({i, j});
                }
            }
        }
    
        // solve && output
        cout << solve(start);
        return 0;
    }
    ```

</details>

### [BOJ 1516 - 게임 개발](https://www.acmicpc.net/problem/1516)
<details>
<summary>보기</summary> 

- 정보
    - Tier: GoldⅢ
    - Tag: topology_sort

- 타임라인
    - Problem Open: --/-- -:--
    - Tag Open: --/-- --:--
    - Solve: 12/14 14:07

- 풀이
    - "먼저 지어야 하는 건물" -> "나중에 지어야 하는 건물" 로 단방향 그래프 만들기
	- $dp[i] = i$번째 건물이 지어질 수 있는 최소 시간 = 이전 건물이 지어지는 최소 시간 ($dp[j]$) $+ i$번째 건물을 지을 때 필요한 시간 ($time[i]$)
	- 메모리 아끼기 위해 (-귀찮으니-) 초기 dp값은 i번째 건물을 지을 때 필요한 시간으로 초기화 (이전 건물이 지어지는 최소 시간을 더하면 됨)
	- 위상정렬 활용하여 차수가 0이 되는 건물의 dp값 설정 후 우선순위 큐에 삽입, 이때 우선순위 큐는 최소 시간 우선을 기준으로 설정.

- 회고
    - 위상정렬을 복습할 때..
 
- 코드
  - ```cpp
	#include <iostream>
    #include <queue>
    #include <vector>
    
    using namespace std;
    
    int main() {
        // fastIO
        ios_base::sync_with_stdio(false);
        cin.tie(NULL); cout.tie(NULL);
    
        // init && input
        int n;
        cin >> n;
    
        vector <int> dp(n + 1);
        vector <int> degree(n + 1);
        vector <vector <int>> graph(n + 1);
    
        int u;
        for (int i = 1; i <= n; i++) {
            cin >> dp[i] >> u;
            while (u != -1) {
                graph[u].push_back(i);
                degree[i]++;
                cin >> u;
            }
        }
    
        // solve
        priority_queue <pair <int, int>> pq;
        for (int i = 1; i <= n; i++) {
            if (degree[i] == 0) pq.push({-dp[i], i});
        }
    
        while (!pq.empty()) {
            int curDist = -pq.top().first;
            int curNode = pq.top().second;
            pq.pop();
    
            for (auto &nxt : graph[curNode]) {
                degree[nxt]--;
                if (degree[nxt] == 0) {
                    dp[nxt] += curDist;
                    pq.push({-dp[nxt], nxt});
                }
            }
        }
    
        // output
        for (int i = 1; i <= n; i++) {
            cout << dp[i] << '\n';
        }
        return 0;
    }
    ```

</details>

## 공부한 내용
- C++ 기초 플러스 7장 (함수) 복습: 개인 노션에 정리

## 다음주 목표
- 문제만 풀지 말고 공부한거 정리하기
- C++ 기초 플러스 8장 정리

## 특이사항
- 2층침대를 1층침대로 바꾸는 생활관 대공사 진행완. (생활관 좁아지니 개불편함)
- 15일 나홀로 주말외출
