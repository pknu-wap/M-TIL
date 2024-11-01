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

## 공부한 내용
- 종만북 Ch08 (DP)
- 분할정복, 동적계획법 문제풀이 연습

## 다음주 목표
- 스트릭 잇기
- 종만북 Ch09

## 특이사항
- 너무피곤해용
