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

## 공부한 내용
- 종만북 Ch08 (DP)
- 분할정복, 동적계획법 문제풀이 연습

## 다음주 목표
- 스트릭 잇기
- 종만북 Ch09

## 특이사항
- 너무피곤해용
