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

## 공부한 내용
- 뭘 했을까

## 다음주 목표
- 뭘 해야할까

## 특이사항
- 23일 단체외출
- 요즘 그림그리는게 너무 재밌네요
