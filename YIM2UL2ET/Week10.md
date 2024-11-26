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

## 공부한 내용
- 뭘했을까

## 다음주 목표
- 뭘해야할까

## 특이사항
- 12/01 ~ 12/09 휴가
