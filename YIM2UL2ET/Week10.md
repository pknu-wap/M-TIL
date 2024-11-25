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

## 공부한 내용
- 뭘했을까

## 다음주 목표
- 뭘해야할까

## 특이사항
- 12/01 ~ 12/09 휴가
