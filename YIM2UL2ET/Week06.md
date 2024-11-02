## 기간
**24.10.28 ~ 24.11.03**

## 풀었던 문제

### [BOJ 16974 - 레벨 햄버거](https://www.acmicpc.net/problem/16974)
<details>
<summary>보기</summary> 

- 정보
    - Tier: GoldⅤ
    - Tag: divide_and_conquer, DP

- 타임라인
    - Problem Open: 10/29 12:00?
    - Tag Open: 10/29 12:00?
    - Solve: 10/29 22:11

- 풀이
    - $layer[N] = N$레벨 버거의 레이어 $= layer[N - 1] \cdot 2 + 3$
    - $patty[N] = N$레벨 버거의 패티 개수 $= patty[N - 1] \cdot 2 + 1$
    - 메모이제이션한 두 배열을 바탕으로 분할정복으로 해결

- 회고
    - 머리도 안돌아가고, 코드도 개판으로 짜놔서.. 레퍼런스를 한번 보고 분석해야 할듯
 
- 코드
  - ```cpp
    #include <iostream>
    #include <vector>
    
    using namespace std;
    
    vector <long long> layer(51);
    vector <long long> patty(51);
    
    long long solve(int Lv, long long X) {  // Lv 햄버거에서 X장의 레이어를 먹었을 때 먹은 패티의 개수
        if (layer[Lv] <= X) {
            return patty[Lv];
        } else if (X <= 0) {
            return 0;
        } else {
            long long result = 0;
    
            result += solve(Lv - 1, X - 1);
            if (X - layer[Lv - 1] - 2 >= 0) result++;
            result += solve(Lv - 1, X - layer[Lv - 1] - 2);
    
            return result;
        }
    }
    
    int main() {
        // init && input
        int N;
        long long X;
        cin >> N >> X;
        
        layer[0] = 1; patty[0] = 1;
        for (int i = 1; i <= 50; i++) {
            layer[i] = layer[i - 1] * 2 + 3;
            patty[i] = patty[i - 1] * 2 + 1;
        }
        
        // solve
        cout << solve(N, X);
        return 0;
    }
    ```

</details>

### [BOJ 5904 - Moo 게임](https://www.acmicpc.net/problem/5904)
<details>
<summary>보기</summary> 

- 정보
    - Tier: GoldⅤ
    - Tag: divide_and_conquer

- 타임라인
    - Problem Open: 10/30 12:00?
    - Tag Open: 10/30 12:00?
    - Solve: 10/30 12:38

- 풀이
    - $memo[i] = i - 1$레벨의 수열 길이 = $memo[i - 1] \cdot 2 + i + 2$
    - 이를 사용하여 분할정복

- 회고
    - 생각은 되는데 구현이 안됨..
 
- 코드
  - ```cpp
    #include <iostream>
    #include <vector>
    
    using namespace std;
    
    vector <long long> memo;
    
    char recursive(int Lv, int n) {
        if (memo[Lv - 1] < n && n < memo[Lv - 1] + Lv + 3) {
            if (n == memo[Lv - 1] + 1) return 'm';
            else return 'o';
        }
    
        return recursive(Lv - 1, memo[Lv - 1] < n ? n - memo[Lv - 1] - Lv - 2 : n);
    }
    
    int main() {
        int i, n;
        cin >> n;
    
        memo.push_back(0);
        for (i = 1; memo[i - 1] <= 1e9; i++) {
            memo.push_back(memo[i - 1] * 2 + i + 2);
        }
    
        cout << recursive(i - 1, n);
        return 0;
    }
    ```

</details>

### [BOJ 21870 - 시철이가 사랑한 GCD](https://www.acmicpc.net/problem/21870)
<details>
<summary>보기</summary> 

- 정보
    - Tier: GoldⅤ
    - Tag: divide_and_conquer

- 타임라인
    - Problem Open: 10/31 12:00?
    - Tag Open: 10/31 12:00?
    - Solve: 11/01 12:22

- 풀이
    - 분할정복과 유클리드 호제법만 안다면 간단히 풀 수 있는 문제

- 회고
    - 40분동안 문제 자체를 이해하는데에 사용함 (능지처참)
    - 범위 지정을 어떻게 해야 할지 너무 헷깔림
    - 전에 헷깔렸던 [이분 탐색 범위 지정 방식](https://jun-codinghistory.tistory.com/154)을 정리한게 있길래 가져와봄
 
- 코드
  - ```cpp
    #include <iostream>
    #include <vector>
    
    using namespace std;
    
    vector <int> seq; 
    
    int gcd(int a, int b) {
        if (a < b) swap(a, b);
        while (b != 0) {
            int temp = a;
            a = b;
            b = temp % a;
        }
        return a;
    }
    
    int getSeqGcd(int left, int right) {
        int result = seq[left];
        for (int i = left + 1; i <= right; i++) {
            result = gcd(result, seq[i]);
        }
        return result;
    }
    
    int divide(int left, int right) {
        if (left == right) return seq[left];
        
        int mid = (right - left + 1) / 2 + left;
    
        int chsLeft = divide(left, mid - 1) + getSeqGcd(mid, right);
        int chsRight = divide(mid, right) + getSeqGcd(left, mid - 1);
        return max(chsLeft, chsRight);
    }
    
    int main() {
        // fastIO
        ios_base::sync_with_stdio(false);
        cin.tie(NULL); cout.tie(NULL);
    
        // init && input
        int N;
        cin >> N;
    
        seq.resize(N + 1);
        for (int i = 1; i <= N; i++) {
            cin >> seq[i];
        }
    
        // solve
        cout << divide(1, N);
        return 0;
    }
    ```

</details>

### [BOJ 13325 - 이진 트리](https://www.acmicpc.net/problem/13325)
<details>
<summary>보기</summary> 

- 정보
    - Tier: GoldⅢ
    - Tag: tree_dp

- 타임라인
    - Problem Open: 11/02 14:00?
    - Tag Open: --/-- --:--
    - Solve: 11/02 14:53

- 풀이
  - $memo[i] =$ 좌측 위 i번째 간선이 잇는 부모노드가 루트인 트리에서 루트노드->리프노드 로 가는 가중치의 최솟값
  - 해당 $memo[i]$는 자식노드가 루트가 되는 부분트리의 $memo[i \cdot 2 + 1]$와 $memo[i \cdot 2 + 2]$가 갱신되었다는 가정 하에 갱신되어야 함.
  - 코드 참조

- 회고
  - tree dp일줄은 전혀 생각 못했는데.. 지금 적으면서 보니 tree dp가 맞는 것 같다..
  - 2의 거듭제곱시 시프트 연산(<<)을 활용하면 편하고 빠르다!
  - 어떻게 설명해야 할지 모르겠네 ㄹㅇ
 
- 코드
  - ```cpp
    #include <iostream>
    #include <vector>
    
    using namespace std;
    
    int N;
    vector <int> cost;
    
    int divide(int lv, int n) {
        if (lv == N) return 0;
    
        int left = n, right = n + 1;
        int lValue = divide(lv + 1, (left << 1) + 1);
        int rValue = divide(lv + 1, (right << 1) + 1);
    
        if (cost[left] + lValue < cost[right] + rValue) {
            cost[left] = cost[right] + rValue - lValue;
        } else {
            cost[right] = cost[left] + lValue - rValue;
        }
        return cost[left] + lValue;
    }
    
    int main() {
        // fastIO
        ios_base::sync_with_stdio(false);
        cin.tie(NULL); cout.tie(NULL);
    
        // init && input
        cin >> N;
    
        cost.resize((1 << (N + 1)) - 1);
        for (int i = 1; i < int(cost.size()); i++) {
            cin >> cost[i];
        }
    
        // solve
        divide(0, 1);
    
        int ans = 0;
        for (auto &el : cost) {
            ans += el;
        }
    
        cout << ans;
        return 0;
    }
    ```

</details>

### [BOJ 11066 - 파일 합치기](https://www.acmicpc.net/problem/11066)
<details>
<summary>보기</summary> 

- 정보
    - Tier: GoldⅢ
    - Tag: DP

- 타임라인
    - Problem Open: 11/02 15:00?
    - Tag Open: 11/02 16:00?
    - Solve: 11/02 16:40

- 풀이
  - $memo[i][j] = i$부터 $j$까지 합쳤을 때 최소 비용
  - $memo[i][j] = memo[i][x] + memo[x+1][j] + \sum_{c=i}^j cost[c]$  $(i \le x \le j)$

- 회고
  - "연속이 되도록 파일을 합쳐나가고" <- 숨은 조건 찾기임?
  - 해당 조건이 있는줄 모르고 우선순위 큐로 구현하다가 이상해서 [질문게시판](https://www.acmicpc.net/board/view/32758) 보면서 1시간 날림;
  - 문제 잘 안읽은 내 잘못이긴 한데.. 이건 좀 너무하지 않나
 
- 코드
  - ```cpp
    #include <iostream>
    #include <vector>
    
    using namespace std;
    
    void problem() {
        // init && input;
        int N;
        cin >> N;
    
        vector <vector <int>> memo(N + 1, vector <int> (N + 1, 1e8)); // memo[i][j] = i부터 j까지 합쳤을 때 최소비용
        vector <int> sum(N + 1);
    
        int cost;
        for (int i = 1; i <= N; i++) {
            cin >> cost;
            sum[i] = sum[i - 1] + cost;
        }
    
        for (int i = 0; i <= N; i++) {
            memo[i][i] = 0;
        }
    
        // solve
        for (int c = 1; c < N; c++) {
            for (int i = 1; i + c <= N; i++) {
                for (int j = i; j < i + c; j++) {
                    memo[i][i + c] = min(memo[i][i + c], memo[i][j] + memo[j + 1][i + c] + sum[i + c] - sum[i - 1]);
                }
            }
        }
    
        cout << memo[1][N] << '\n';
    }
    
    int main() {
        // fastIO
        ios_base::sync_with_stdio(false);
        cin.tie(NULL); cout.tie(NULL);
    
        // TC
        int TC;
        cin >> TC;
        for (int i = 0; i < TC; i++) {
            problem();
        }
        return 0;
    }
    ```

</details>

### [BOJ 17471 - 게리맨더링](https://www.acmicpc.net/problem/17471)
<details>
<summary>보기</summary> 

- 정보
    - Tier: GoldⅢ
    - Tag: bruteforcing, graph_traversal

- 타임라인
    - Problem Open: 11/02 16:45?
    - Tag Open: --/-- --:--
    - Solve: 11/02 17:12

- 풀이
  - 백트래킹, dfs 사용하여 풀이

- 회고
  - 신중히 구현하기
  - 조건 빠진거 없나 체크 (ex. 같은 선거구끼리만 그래프를 탐색하였나)
 
- 코드
  - ```cpp
    #include <iostream>
    #include <vector>
    
    #define INF 1e8
    
    using namespace std;
    
    int N;
    vector <vector <int>> graph;
    vector <bool> isRedZone;
    vector <int> value;
    
    void dfs(int n, vector <bool> &isVst, bool isRed) {
        isVst[n] = true;
        for (auto &e : graph[n]) {
            if (isVst[e] || isRedZone[e] != isRed) continue;
            dfs(e, isVst, isRed);
        }
    }
    
    bool isPossible() {
        vector <bool> isVst(N + 1, false);
        bool vstBlue = false, vstRed = false;
    
        for (int i = 1; i <= N; i++) {
            if (isVst[i]) continue;
            if ((isRedZone[i] && vstRed) || (!isRedZone[i] && vstBlue)) return false;
            
            dfs(i, isVst, isRedZone[i]);
            if (isRedZone[i]) {
                vstRed = true;
            } else {
                vstBlue = true;
            }
        }
        return true;
    }
    
    int backtracking(int n, int redValue, int blueValue) {
        if (n == N + 1) {
            if (isPossible()) {
                return abs(redValue - blueValue);
            } else {
                return INF;
            }
        }
    
        isRedZone[n] = true;
        int r = backtracking(n + 1, redValue + value[n], blueValue);
        isRedZone[n] = false;
        int b = backtracking(n + 1, redValue, blueValue + value[n]);
        return min(r, b);
    }
    
    int main() {
        // fastIO
        ios_base::sync_with_stdio(false);
        cin.tie(NULL); cout.tie(NULL);
    
        // init && input
        cin >> N;
    
        graph.resize(N + 1);
        value.resize(N + 1);
        isRedZone.resize(N + 1);
    
        for (int i = 1; i <= N; i++) {
            cin >> value[i];
        }
    
        for (int i = 1; i <= N; i++) {
            int node, ea;
    
            cin >> ea;
            for (int j = 0; j < ea; j++) {
                cin >> node;
                graph[i].push_back(node);
            }
        }
    
        // solve
        int ans = backtracking(1, 0, 0);
        cout << (ans != INF ? ans : -1);
        return 0;
    }
    ```

</details>

## 공부한 내용
- 종만북 Ch08 (DP)
- 분할정복, DP 문제풀이 연습

## 다음주 목표
- 스트릭 잇기
- 종만북 Ch09 (DP 테크닉)

## 특이사항
- 너무피곤해용
