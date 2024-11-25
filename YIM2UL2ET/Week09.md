## 기간
**24.11.18 ~ 24.11.24**

## 풀었던 문제

### [BOJ 1670 - 정상 회담 2](https://www.acmicpc.net/problem/1670)
<details>
<summary>보기</summary> 

- 정보
    - Tier: GoldⅢ
    - Tag: DP

- 타임라인
    - Problem Open: --/-- --:--
    - Tag Open: --/-- --:--
    - Solve: 11/18 12:12

- 풀이
    - $DP[n] = \sum_{i = 0}^{n-2} DP[i] \cdot DP[n-i-2]$
    - 해당 점화식을 탑다운 형식으로 구현

- 회고
    - [카탈란 수](https://jjycjnmath.tistory.com/139)
 
- 코드
  - ```cpp
    #include <iostream>
    #include <vector>
    
    #define mod 987654321
    
    using namespace std;
    
    vector <long long> cache; // cache[i] = 집합의 크기가 i일 떄 악수 할 수 있는 경우의 수 % mod
    
    long long solve(int n) {
        auto &ret = cache[n];
        if (ret == -1) {
            ret = 0;
            for (int i = 0; i <= n - 2; i += 2) {
                ret += (solve(i) % mod) * (solve(n - i - 2) % mod);
                ret %= mod;
            }
        }
        return ret;
    }
    
    int main() {
        int n;
        cin >> n;
    
        cache.resize(n + 1, -1);
        cache[0] = 1;
        cout << solve(n);
        return 0;
    }
    ```

</details>

### [BOJ 2749 - 피보나치 수 3](https://www.acmicpc.net/problem/2749)
<details>
<summary>보기</summary> 

- 정보
    - Tier: GoldⅡ
    - Tag: DP

- 타임라인
    - Problem Open: 11/19 12:00
    - Tag Open: 11/19 12:00
    - Solve: 11/19 20:38

- 풀이
    - 분할정복을 활용한 행렬의 거듭제곱 기법을 사용하는 DP 연습 문제
    - 기본적인 피보나치 점화식인 $DP[i+2] = DP[i+1] + DP[i] (i \ge 0)$를 행렬로 변환
    - <img src="http://latex.codecogs.com/png.latex?\dpi{110}\bg_white 
          \begin{bmatrix} 
          0 & 1 \\ 1 & 1
          \end{bmatrix}
          \cdot
          \begin{bmatrix} 
          DP[i] \\ DP[i+1]
          \end{bmatrix}
          =
          \begin{bmatrix} 
          DP[i+1] \\ DP[i+2]
          \end{bmatrix}
          (i \ge 0)
          "/>

- 회고
    - 구현시간 약 1시간?
    - 기초적인 실수 조심 (n을 int형으로 받으려고 시도함)
 
- 코드
  - ```cpp
    #include <iostream>
    #include <vector>
    
    #define mod 1000000
    
    using namespace std;
    
    vector <vector <long long>> mulMatrix(vector <vector <long long>> &W1, vector <vector <long long>> &W2) {
        int rSize = W1.size(), cSize = W2.back().size();
        vector <vector <long long>> result(rSize, vector <long long>(cSize, 0));
        
        for (int c = 0; c < cSize; c++) {
            for (int r = 0; r < rSize; r++) {
                for (int k = 0; k < W2.size(); k++) {
                    auto &ret = result[r][c];
                    ret += ((W2[k][c] % mod) * (W1[r][k] % mod)) % mod;
                    ret %= mod;
                }
            }
        }
    
        return result;
    }
    
    vector <vector <long long>> powMatrix(long long n, vector <vector <long long>> &W) {
        if (n == 1) return W;
    
        vector <vector <long long>> newMatrix;
        if (n % 2 == 0) {
            newMatrix = powMatrix(n / 2, W);
            return mulMatrix(newMatrix, newMatrix);
        } else {
            newMatrix = powMatrix(n - 1, W);
            return mulMatrix(newMatrix, W);
        }
    }
    
    int main() {
        long long n;
        cin >> n;
    
        vector <vector <long long>> W{{0, 1}, {1, 1}};
        vector <vector <long long>> fibo{{0}, {1}};
        if (n >= 2) {
            W = powMatrix(n - 1, W);
            cout << mulMatrix(W, fibo)[1][0] % mod;
        } else {
            cout << n;
        }
        return 0;
    }
    ```

</details>

### [BOJ 1646 - 피이보나치 트리](https://www.acmicpc.net/problem/1646)
<details>
<summary>보기</summary> 

- 정보
    - Tier: GoldⅠ
    - Tag: DP

- 타임라인
    - Problem Open: 11/20 12:00
    - Tag Open: 11/20 12:00
    - Solve: 11/20 20:06

- 풀이
    - $memo[i] = memo[i - 1] + memo[i - 2] + 1 = i$레벨에서의 노드 수 $(i \ge 2)$
    - $i < 2$일 경우 $1$개의 노드만 존재하므로 $memo[0] = memo[1] = 1$
    - 함수 $order(Lv, root, target) =$ 루트노드가 $root$인 $Lv$레벨 피이보나치 트리에서 $target$노드까지 가는 방법
    - 1. $memo$ 점화식을 사용하여 50까지 초기화 시킴
      2. $start$노드와 $end$노드를 사용하여 $order(N, 1, start), order(N, 1, end)$ 시켜 최상단 노드에서 가는 방법을 찾음
      3. 2번의 두 string을 사용하여 최하위 공통 조상노드를 찾음
      4. $answer = (start$노드에서 해당 조상노드까지의 거리 $) \cdot$ 'U' $+ ($ 해당 조상노드에서 $end$노드까지 가는 방법 $)$

- 회고
    - [start노드에서 end노드까지 직접 가는 방식을 찾으려고 하다 실패한 코드](https://www.acmicpc.net/source/86659834)
    - 종교활동 참석하는데 해당 방법이 딱 생각나서 갔다온 후 바로 구현하여 AC (쾌감 미쳤다)
 
- 코드
  - ```cpp
    #include <iostream>
    #include <vector>
    
    typedef long long LL;
    
    using namespace std;
    
    int N;
    LL start, target;
    vector <LL> treeEA;
    
    void initTreeEA() {
        treeEA.resize(N + 1);
        treeEA[0] = treeEA[1] = 1;
        for (int i = 2; i <= N; i++) {
            treeEA[i] = treeEA[i - 1] + treeEA[i - 2] + 1;
        }
    }
    
    string order(int lv, LL cur, LL target) {
        if (cur == target) return "";
        
        if (cur + treeEA[lv - 2] < target) { // R
            return "R" + order(lv - 1, cur + treeEA[lv - 2] + 1, target);
        } else {    // L
            return "L" + order(lv - 2, cur + 1, target);
        }
    }
    
    int main() {
        cin >> N >> start >> target;
    
        initTreeEA();
        string rootToStart = order(N, 1, start);
        string rootToEnd = order(N, 1, target);
    
        int idx = 0;
        while (idx != int(rootToStart.size()) && idx != int(rootToEnd.size())) {
            if (rootToStart[idx] != rootToEnd[idx]) {
                break;
            } else {
                idx++;
            }
        }
    
        for (int i = 0; i < rootToStart.size() - idx; i++) {
            cout << 'U';
        }
        cout  << rootToEnd.substr(idx);
    
        return 0;
    }
    ```

</details>

### [BOJ 30023 - 전구 상태 바꾸기](https://www.acmicpc.net/problem/30023)
<details>
<summary>보기</summary> 

- 정보
    - Tier: GoldⅤ
    - Tag: Greedy

- 타임라인
    - Problem Open: 11/21 12:00
    - Tag Open: 11/21 12:00
    - Solve: 11/21 12:58

- 풀이
    - $mod$ 연산자를 사용하여 전구의 색을 변경
    - $setColor() = lamps$를 $idx$위치부터 끝까지 $color$색으로 바꾸는 데에 필요한 색 변경 횟수
    - 작동 방식: $lamps[idx]$을 최소 변경 횟수로 $color$으로 바꾼 후 $idx+1$번째부터 끝까지 $color$색으로 변경 $(0 \le idx \le N-3)$
    - 0번째 색을 바꾸는 방법은 0 ~ 2번째 색을 바꾸는 방법밖에 없으므로 해당 방식대로 바꾸고, 1번째 색도 이러한 방식으로 1 ~ 3번째 색(0 ~ 2번째 색 변경법은 이미 썻으므로 X)을 변경하고..
    - 이러한 방식으로 0 ~ N-3번째 색을 일괄적으로 같게 변경 후, N-3 ~ N-1번째 색이 같으면 변경 가능, 다르면 변경 불가능 하다는 뜻이다.
    - 만약 0번째부터 색을 바꾸지 않았다면 0번째 색이 바뀔 때 1 ~ 2번째 색, 그 색을 바꾸려고 할 때 그 이상의 위치의 색이 바뀌기 때문에 0번째부터 바꿀 때 보다 횟수가 크거나, 같을 수밖에 없다.

- 회고
    - 탐욕적 선택 속성 증명 연습
    - 증명이 너무 어렵네용..
 
- 코드
  - ```cpp
    #include <iostream>
    #include <vector>
    
    using namespace std;
    
    int N;
    
    int setColor(vector <int> &lamps, int idx, int color) {
        if (idx + 2 == N) {
            if (lamps[idx - 1] == lamps[idx] && lamps[idx] == lamps[idx + 1]) {
                return 0;
            } else {
                return -1;
            }
        }
    
        int setNum, result;
    
        setNum = (color + 3 - lamps[idx]) % 3;  // c = (lamp + x) % 3
        for (int i = 0; i < 3; i++) {
            lamps[idx + i] = (lamps[idx + i] + setNum) % 3;
        }
    
        result = setColor(lamps, idx + 1, color);
        for (int i = 0; i < 3; i++) {
            lamps[idx + i] = (lamps[idx + i] - setNum + 3) % 3;
        }
    
        return (result != -1 ? result + setNum : -1);
    }
    
    int main() {
        ios_base::sync_with_stdio(false);
        cin.tie(NULL); cout.tie(NULL);
    
        cin >> N;
        vector <int> lamps(N);
    
        string str;
        cin >> str;
        for (int i = 0; i < N; i++) {
            if (str[i] == 'R') {
                lamps[i] = 0;
            } else if (str[i] == 'G') {
                lamps[i] = 1;
            } else if (str[i] == 'B') {
                lamps[i] = 2;
            }
        }
    
        int ans = 1e9;
        for (int i = 0; i < 3; i++) {
            int res = setColor(lamps, 0, i);
            ans = min(ans, res != -1 ? res : ans);
        }
    
        cout << (ans != 1e9 ? ans : -1);
        return 0;
    }
    ```

</details>

### [BOJ 16467 - 병아리의 변신은 무죄](https://www.acmicpc.net/problem/16467)
<details>
<summary>보기</summary> 

- 정보
    - Tier: GoldⅠ
    - Tag: DP

- 타임라인
    - Problem Open: 11/21 22:15
    - Tag Open: 11/21 22:15
    - Solve: 11/22 08:03

- 풀이
    - $DP[i] = i$번째 날에 존재하는 병아리의 수 $= DP[i - 1] + DP[i - 1 - K]$
    - <img src="http://latex.codecogs.com/png.latex?\dpi{110}\bg_white 
          ex) 
          \begin{bmatrix} 
          0 & 1 & 0 & 0 & 0 & 0 & 0 & 0 & 0 & 0 & 0 \\ 
          0 & 0 & 1 & 0 & 0 & 0 & 0 & 0 & 0 & 0 & 0 \\ 
          0 & 0 & 0 & 1 & 0 & 0 & 0 & 0 & 0 & 0 & 0 \\ 
          0 & 0 & 0 & 0 & 1 & 0 & 0 & 0 & 0 & 0 & 0 \\ 
          0 & 0 & 0 & 0 & 0 & 1 & 0 & 0 & 0 & 0 & 0 \\ 
          0 & 0 & 0 & 0 & 0 & 0 & 1 & 0 & 0 & 0 & 0 \\ 
          0 & 0 & 0 & 0 & 0 & 0 & 0 & 1 & 0 & 0 & 0 \\ 
          0 & 0 & 0 & 0 & 0 & 0 & 0 & 0 & 1 & 0 & 0 \\ 
          0 & 0 & 0 & 0 & 0 & 0 & 0 & 0 & 0 & 1 & 0 \\ 
          0 & 0 & 0 & 0 & 0 & 0 & 0 & 0 & 0 & 0 & 1 \\ 
          0 & 0 & 0 & 0 & 0 & 0 & 0 & 0 & 1 & 0 & 1 \\ 
          \end{bmatrix}
          \cdot
          \begin{bmatrix} 
          DP[i] \\ DP[i+1] \\ DP[i+2] \\ DP[i+3] \\ DP[i+4] \\ DP[i+5] \\ DP[i+6] \\ DP[i+7] \\ DP[i+8] \\ DP[i+9] \\ DP[i+10] \end{bmatrix} 
          =
          \begin{bmatrix} 
          DP[i+1] \\ DP[i+2] \\ DP[i+3] \\ DP[i+4] \\ DP[i+5] \\ DP[i+6] \\ DP[i+7] \\ DP[i+8] \\ DP[i+9] \\ DP[i+10] \\ DP[i+11] \end{bmatrix}
          (K = 2, i \ge 0)
          "/>
     - 이를 일반화 하여 첫번째 행렬을 $W$, 두번째 행렬을 $V$라고 했을 때 $W^{N-10} \cdot V (N \ge 11)$를 하여 DP[N]을 구할 수 있음.
     - 물론 $W$는 $W[j][j+1] = 1 (0 \le j \le 10)$, 나머지를 $0$으로 설정 후 $W[10][10 - K]$에 1을 더하여 init

- 회고
    - 행렬의 거듭제곱을 활용한 DP 연습
    - 식을 잘 세워두고 구현하도록 (머릿속으로 생각하지 말고 적으면서 하기)
 
- 코드
  - ```cpp
    #include <iostream>
    #include <vector>
    
    #define MOD 100000007
    
    using namespace std;
    
    void initW(vector <vector <long long>> &W, int K) {
        W.resize(11, vector <long long> (11, 0));
        
        for (int i = 0; i < 10; i++) {
            W[i][i + 1] += 1;
        }
        
        W.back().back() += 1; 
        W.back()[10 - K] += 1;
    }
    
    void initV(vector <vector <long long>> &V, int K) { 
        V.resize(11, vector <long long> (1));
    
        V[0][0] = 1;
        for (int i = 1; i <= 10; i++) {
            if (i - K > 0) {
                V[i][0] = V[i - 1][0] + V[i - K - 1][0];
            } else {
                V[i][0] = V[i - 1][0];
            }
        }
    }
    
    vector <vector <long long>> mulMatrix(vector <vector <long long>> &W1, vector <vector <long long>> &W2) {
        int N = W1.size(), M = W2.back().size(), K = W2.size();
        vector <vector <long long>> result(N, vector <long long> (M));
    
        for (int i = 0; i < N; i++) {
            for (int j = 0; j < M; j++) {
                for (int k = 0; k < K; k++) {
                    result[i][j] += ((W1[i][k] % MOD) * (W2[k][j] % MOD)) % MOD;
                    result[i][j] %= MOD;
                }
            }
        }
        return result;
    }
    
    vector <vector <long long>> powMatrix(int n, vector <vector <long long>> &curMatrix) {
        if (n == 1) return curMatrix;
    
        if (n % 2 == 0) {
            auto newMatrix = powMatrix(n / 2, curMatrix);
            return mulMatrix(newMatrix, newMatrix);
        } else {
            auto newMatrix = powMatrix(n - 1, curMatrix);
            return mulMatrix(curMatrix, newMatrix);
        }
    }
    
    void solve() {
        // input && init
        int K, N;
        cin >> K >> N;
    
        vector <vector <long long>> W;
        vector <vector <long long>> V;
    
        initW(W, K);
        initV(V, K);
    
        if (N <= 10) {
            cout << V[N][0] << '\n';
        } else {
            W = powMatrix(N - 10, W);
            V = mulMatrix(W, V);
    
            cout << V.back()[0] << '\n';
        }
    }
    
    int main() {
        // fastIO
        ios_base::sync_with_stdio(false);
        cin.tie(NULL); cout.tie(NULL);
    
        // test case
        int tc;
        cin >> tc;
        for (int i = 0; i < tc; i++) {
            solve();
        }
        return 0;
    }
    ```

</details>

### [BOJ 12851 - 숨바꼭질 2](https://www.acmicpc.net/problem/12851)
<details>
<summary>보기</summary> 

- 정보
    - Tier: GoldⅣ
    - Tag: BFS

- 타임라인
    - Problem Open: 11/24 22:15
    - Tag Open: --/-- --:--
    - Solve: 11/24 22:39

- 풀이
    - 전형적인 BFS문제이지만, 2차원 배열이 아닌 1차원 배열에서의 BFS라는 점을 유의해야 함.

- 회고
    - BFS를 활용한 문제라는 것을 AC를 한 후에 깨달았다.
    - 쿼리에 추가: 그래프 탐색은 1차원 배열에서도 활용될 수 있다.
 
- 코드
  - ```cpp
    #include <iostream>
    #include <queue>
    #include <vector>
    
    #define limit 1e5
    
    using namespace std;
    
    int main() {
        int start, end;
        cin >> start >> end;
    
        vector <int> ea(limit + 1, 0);
        ea[start] = 1;
    
        vector <bool> vst(limit + 1, false);
    
        queue <int> nxtIdx;
        nxtIdx.push(start);
    
        int t = 0;
        while (ea[end] == 0) {
            queue <int> que;
            int s = nxtIdx.size();
    
            for (int i = 0; i < s; i++) {
                int nxt = nxtIdx.front();
                nxtIdx.pop();
    
                if (nxt + 1 <= limit && !vst[nxt + 1]) {
                    que.push(nxt + 1);
                    nxtIdx.push(nxt + 1);
                    ea[nxt + 1]++;
                }
                if (nxt - 1 >= 0 && !vst[nxt - 1]) {
                    que.push(nxt - 1);
                    nxtIdx.push(nxt - 1);
                    ea[nxt - 1]++;
                }
                if (nxt * 2 <= limit && !vst[nxt * 2]) {
                    que.push(nxt * 2);
                    nxtIdx.push(nxt * 2);
                    ea[nxt * 2]++;
                }
            }
    
            while (!que.empty()) {
                vst[que.front()] = true;
                que.pop();
            }
    
            t++;
        }
    
        cout << t << '\n' << ea[end];
        return 0;
    }
    ```

</details>

## 공부한 내용
- 종만북 Ch10 (탐욕법)
- LaTex 문법 공부

## 다음주 목표
- 휴가 전까지 골드스트릭 잇기
- 종만북 Ch11 (조합탐색)

## 특이사항
- 23일 생활관 단체 외출
- 그림 그리는 것이 너무나 재밌음.
