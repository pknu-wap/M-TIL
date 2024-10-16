## 기간
**24.10.14 ~ 24.10.20**

## 풀었던 문제

### [BOJ 2342 - Dance Dance Revolution](https://www.acmicpc.net/problem/2342)
<details>
<summary>보기</summary> 

- 정보
    - Tier: GoldⅢ
    - Tag: dynamic_programming

- 타임라인
    - Problem Open: 10/14 13:00? 
    - Tag Open: --/-- --:--
    - Solve: 10/14 19:17

- 풀이
    - 동작을 11개의 번호로 나눠서 DP로 풀이 (ex. {0,0} -> 0번째 동작, {0,1} -> 1번째 동작...) + ({left, right}에서 left <= right)
    - $memo[i][j]$: i번째 동작에서 j번 동작을 취했을 때 힘의 최솟값 (j $\in$ 입력받은 발판위치가 무조건 들어가도록 하는 값)
    - $cost[i][j]$: i번 위치에서 j번 위치로 이동시 드는 힘의 값
    - $memo[i][j] = min{\sum_{k=0}^{11} memo[i - 1][k] + cost[k][j]}$

- 회고
    - 실 풀이시간 약 50분 (구현에 30분정도..)
    - 아.. DP 너무 어렵..

</details>

### [BOJ 16724 - 피리 부는 사나이](https://www.acmicpc.net/problem/16724)
<details>
<summary>보기</summary> 

- 정보
    - Tier: GoldⅢ
    - Tag: union_find

- 타임라인
    - Problem Open: 10/14 13:00? 
    - Tag Open: --/-- --:--
    - Solve: 10/14 19:43

- 풀이
    - 맵을 구역별로 나눈 2차원 배열 locNum을 생성하여 탐색과 갱신을 반복
    - 탐색시 사이클이 생기면 새로운 구역, 다른 구역에 도달하면 기존 구역에 포함된 것.
    - 새로 나온 구역의 개수 = 정답

- 회고
    - 실 풀이시간 약 30분 (구현에 20분정도..)

</details>

### [BOJ 20303 - 할로윈의 양아치](https://www.acmicpc.net/problem/20303)
<details>
<summary>보기</summary> 

- 정보
    - Tier: GoldⅢ
    - Tag: union_find, knapsack

- 타임라인
    - Problem Open: 10/14 13:00? 
    - Tag Open: --/-- --:--
    - Solve: 10/14 22:42

- 풀이
    - union find 사용 후 knapsack 문제로 풀이

- 회고
    - 실 풀이시간 약 70분? (구현에 60분정도..)
    - 자꾸 MLE나서 DP문젠가 싶었는데 union_find 함수 이상하게 짜놓음.. 정확히 이해하고 코드를 짜도록 하자
    - ```cpp
      void connect(int u, int v) {
        u = findParent(u);
        v = findParent(v);
        if (u < v) parent[v] = u;
        else parent[u] = v;
      }

</details>

### [BOJ 2623 - 음악프로그램](https://www.acmicpc.net/problem/2623)
<details>
<summary>보기</summary> 

- 정보
    - Tier: GoldⅢ
    - Tag: topological_sorting

- 타임라인
    - Problem Open: 10/14 23:00 
    - Tag Open: --/-- --:--
    - Solve: 10/14 23:14

- 풀이
    - 위상정렬을 활용하여 풀이
    - 보조 PD가 담당한 가수들을 입력받을 때, 중복된 에지 체크하지 않도록 주의하며 에지와 차수를 갱신함.
    - 0이 나올 조건을 제외함 = 사이클이 나오는 것 (특히 양방향 에지)
    - 주의점: 담당 가수의 수가 2명 미만일 경우도 있음.

- 회고
    - 사이클 여부를 체크하지 않아 WA가 났었음.
    - 알고리즘을 사용하기 위해 조건이 충족되었는지 확인하는 습관 가지기

</details>

### [BOJ 17404 - RGB거리 2](https://www.acmicpc.net/problem/17404)
<details>
<summary>보기</summary> 

- 정보
    - Tier: GoldⅣ
    - Tag: dynamic_programming

- 타임라인
    - Problem Open: 10/15 11:50 
    - Tag Open: --/-- --:--
    - Solve: 10/14 12:44

- 풀이
    - $dp[i][j]$ = 첫 시작 색이 $j/3$번째이고, 현재 색이 $j%3%일때 최소 누적 합
    - 정답 : $dp[N-1][k] (k \in \lbrace 1, 2, 3, 5, 6, 7\rbrace)$ -> $0, 4, 8$번째 제외

- 회고
    - DP 어려워용

</details>

### [BOJ 10942 - 팰린드롬?](https://www.acmicpc.net/problem/10942)
<details>
<summary>보기</summary> 

- 정보
    - Tier: GoldⅣ
    - Tag: dynamic_programming

- 타임라인
    - Problem Open: 10/15 18:40
    - Tag Open: --/-- --:--
    - Solve: 10/15 18:54

- 풀이
    - 팰린드롬이 되는 경우의 수를 다 조사하여 2차원 배열에 저장 (memo[i][j] = i~j가 팰린드롬인가)
    - ```cpp
      void update(int start, int end) {
        while (nums[start] == nums[end]) {
            memo[start][end] = true;
            start--; end++;
            if (start < 0 || end >= N) break;
        }
      }

- 회고
    - EASY~

</details>

### [BOJ 1647 - 도시 분할 계획](https://www.acmicpc.net/problem/1647)
<details>
<summary>보기</summary> 

- 정보
    - Tier: GoldⅣ
    - Tag: MST

- 타임라인
    - Problem Open: 10/15 18:55
    - Tag Open: 10/15 19:47
    - Solve: 10/15 20:03

- 풀이
    - 크루스칼 알고리즘을 사용하여 풀이
    - ans = MST 가중치 - MST 가중치 안의 최대값

- 회고
    - MST를 배웠다. (맛있다)

</details>

### [BOJ 1197 - 최소 스패닝 트리](https://www.acmicpc.net/problem/1197)
<details>
<summary>보기</summary> 

- 정보
    - Tier: GoldⅣ
    - Tag: MST

- 타임라인
    - Problem Open: 10/15 22:00
    - Tag Open: --/-- --:--
    - Solve: 10/15 23:06

- 풀이
    - 전형적인 MST 찾는 문제 (크루스칼로 풀이)

- 회고
    - 약 10분만에 구현이 끝났으나, 정렬 함수를 이상하게 짜는 바람에 50분을 날려버림
    - **정렬 함수 구현시 <= 또는 >= 절때 사용 금지**

</details>

### [BOJ 15681 - 트리와 쿼리](https://www.acmicpc.net/problem/15681)
<details>
<summary>보기</summary> 

- 정보
    - Tier: GoldⅤ
    - Tag: dp_tree

- 타임라인
    - Problem Open: 10/15 23:10
    - Tag Open: --/-- --:--
    - Solve: 10/15 23:18

- 풀이
    - DFS로 쿼리 수 찾아서 memo에 저장하여 바로 출력할 수 있게 풀이

- 회고
    - EASY~(2)

</details>

### [BOJ 7579 - 앱](https://www.acmicpc.net/problem/7579)
<details>
<summary>보기</summary> 

- 정보
    - Tier: GoldⅢ
    - Tag: knapsack

- 타임라인
    - Problem Open: 10/16 18:00
    - Tag Open: --/-- --:--
    - Solve: 10/16 18:35

- 풀이
    - 냅색문제로 2차원 $memo$ 만든 후, $ans = min \lbrace K | K \in memo[i][j] \le M \rbrace $를 출력

- 회고
    - 구현에 좀 버벅임

</details>

### [BOJ 1922 - 네트워크 연결](https://www.acmicpc.net/problem/1922)
<details>
<summary>보기</summary> 

- 정보
    - Tier: GoldⅣ
    - Tag: MST

- 타임라인
    - Problem Open: 10/16 18:36
    - Tag Open: --/-- --:--
    - Solve: 10/16 18:51

- 풀이
    - 크루스칼로 풀이

- 회고
    - MST, 크루스칼 복습

</details>

### [BOJ 2583 - 영역 구하기](https://www.acmicpc.net/problem/2583)
<details>
<summary>보기</summary> 

- 정보
    - Tier: SilverⅠ
    - Tag: graph_traversal

- 타임라인
    - Problem Open: 10/16 19:20??
    - Tag Open: --/-- --:--
    - Solve: 10/16 19:40

- 풀이
    - DFS로 풀이

- 회고
    - 구현에 조금 버벅임

</details>

### [BOJ 1806 - 부분합](https://www.acmicpc.net/problem/1806)
<details>
<summary>보기</summary> 

- 정보
    - Tier: GoldⅣ
    - Tag: two_pointer

- 타임라인
    - Problem Open: 10/16 19:00??
    - Tag Open: --/-- --:--
    - Solve: 10/16 19:48

- 풀이
    - 누적합과 투포인터를 활용하는 아주 쉬운 문제
    - ```cpp
      while (right <= N) {
        if (sum[right] - sum[left] >= M) {
            ans = min(ans, right - left);
            left++;
        } else {
            right++;
        }
      }

      cout << (ans == INF ? 0 : ans);

- 회고
    - 실 풀이시간 약 20분

</details>

## 공부한 내용
- 책읽고 블로그에 남겨

## 다음주 목표
- 뭐하징..

## 특이사항
- 10/14 ~ 10/18 진지공사기간
- 10/16 [solved.ac](https://solved.ac/profile/yim2ul2et) Platinum5 + Class5 + 500AC !!
