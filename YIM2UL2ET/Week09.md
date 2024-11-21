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
    - [참조](https://driip.me/00556a4c-0782-4c5b-a86a-8e27e5f4ac1b)

- 회고
    - 구현시간 약 1시간?
    - 기초적인 실수 조심 (n을 int형으로 받으려고 시도함)
    - 이거 왜 LaTex 행렬이 안되지?
 
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
    - 함수 $order(Lv, root, target) = $ 루트노드가 root인 Lv레벨 피이보나치 트리에서 target노드까지 가는 방법
    - 1. $memo$ 점화식을 사용하여 50까지 초기화 시킴
      2. start노드와 end노드를 사용하여 $order(N, 1, start), order(N, 1, end)$ 시켜 최상단 노드에서 가는 방법을 찾음
      3. 2번의 두 string을 사용하여 최하위 공통 조상노드를 찾음
      4. answer = (start노드에서 해당 조상노드까지의 거리) * 'U' + (해당 조상노드에서 end노드까지 가는 방법)

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

## 공부한 내용
- 뭘 했을까

## 다음주 목표
- 뭘 해야할까

## 특이사항
- 23일 단체외출
- 요즘 그림그리는게 너무 재밌네요
