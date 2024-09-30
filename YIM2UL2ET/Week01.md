## 기간
**24.09.23 ~ 24.09.29**

## 풀었던 문제

### [BOJ 30510 - 토마에 함수](https://www.acmicpc.net/problem/30510)
<details>
<summary>보기</summary> 

- 정보
    - Tier: Gold1
    - Tag: euler_phi

- 타임라인
    - Problem Open: 09/23 19:15
    - Tag Open: 09/23 19:15
    - Solve: 09/23 23:30

- 풀이
    - $1 + \sum_{i=1}^{\lfloor \frac{Q}{P} \rfloor} \varphi{(i)}$ 를 구한다.

- 회고
    - 오일러 피 함수를 제대로 구현할 수 있을 때 까지 공부하자
    - for문 구간 설정은 꼭 변수가 아니라 문장으로 해도 된단다..

</details>

### [BOJ 1800 - 인터넷 설치](https://www.acmicpc.net/problem/1800)
<details>
<summary>보기</summary>

- 정보
    - Tier: Gold1
    - Tag: dijkstra, parametric_search

- 타임라인
    - Problem Open: 09/24 18:17
    - Tag Open: 09/24 18:47
    - Solve: 09/24 20:08

- 풀이
    - 결정문제로 바꾸어 이분 탐색을 활용하여 해결
    - 결정함수 $f(x) = x$원 이하의 비용으로 1번 노드와 K번 노드를 연결시킬 수 있는가

- 회고
    - 참조: https://justicehui.github.io/usaco/2019/07/12/BOJ1800/
    - 함수의 입력 및 반환 값 제대로 정의하기

</details>

</details>

### [BOJ 17951 - 흩날리는 시험지 속에서 내 평점이 느껴진거야](https://www.acmicpc.net/problem/17951)
<details>
<summary>보기</summary>

- 정보
    - Tier: Gold3
    - Tag: parametric_search

- 타임라인
    - Problem Open: 09/24 21:00?
    - Tag Open: 09/24 21:00?
    - Solve: 09/24 21:54

- 풀이
    - 결정문제로 바꾸어 해결
    - 결정함수 $f(x) =$ k개 이상의 그룹으로 나누었을 때 $x$보다 큰 점수를 받을 수 있나?

- 회고
    - 매개 변수 탐색 블로그에 정리

</details>

### [BOJ 13397 - 구간 나누기 2](https://www.acmicpc.net/problem/13397)
<details>
<summary>보기</summary>

- 정보
    - Tier: Gold4
    - Tag: parametric_search

- 타임라인
    - Problem Open: 09/24 21:10?
    - Tag Open: 09/24 21:10?
    - Solve: 09/24 22:22

- 풀이
    - 결정문제로 바꾸어 해결
    - 결정함수 $f(x) =$ M개 이하의 배열로 구간 점수의 최댓값이 $x$ 이하이도록 만들 수 있는가?

- 회고
    - 위에 문제랑 판박이..

</details>

### [BOJ 1766 - 문제집](https://www.acmicpc.net/problem/1766)
<details>
<summary>보기</summary>

- 정보
    - Tier: Gold2
    - Tag: topological_sorting

- 타임라인
    - Problem Open: 09/25 18:47
    - Tag Open: --/-- --:--
    - Solve: 09/25 19:31

- 풀이
    - 우선순위 큐를 사용하여 위상정렬
    - 정렬 조건: 현재 풀 수 있는 문제 중에서 쉬운(순번이 작은) 문제
    - 현재 풀 수 있는 문제 = 현재 문제보다 먼저 풀어야 할 문제가 없는 문제

- 회고
    - C++에서 priorit_queue는 기본적으로 최대 힙이다.

</details>

### [BOJ 15317 - 동방 보수](https://www.acmicpc.net/problem/15317)
<details>
<summary>보기</summary>

- 정보
    - Tier: Gold2
    - Tag: parametric_search, greedy

- 타임라인
    - Problem Open: 09/25 21:40?
    - Tag Open: --/-- --:--
    - Solve: 09/25 22:35

- 풀이
    - 동아리방 예산과, 보수비용을 각각 오름차순, 내림차순 정렬 후 결정문제로 바꾸어 해결
    - 결정함수 $f(x) = x$개의 동아리가 동아리방을 가질 수 있는가
    - 이때 결정함수가 참일 조건은 $\sum_{i=1}^x fixcost[i] - \sum_{i=1}^x budget[i] \leqslant X$
    - 비용으로 주어지는 값 자체가 최대 10억정도로 크기 때문에 합으로 처리하지 않고 일일히 처리
      
- 회고
    - 이분 탐색 구간 설정시 문제 조건 잘 보고 정하기

</details>

### [BOJ 1865 - 웜홀](https://www.acmicpc.net/problem/1865)
<details>
<summary>보기</summary>

- 정보
    - Tier: Gold3
    - Tag: bellman_ford

- 타임라인
    - Problem Open: 09/26 12:00?
    - Tag Open: --/-- --:--
    - Solve: 09/26 12:59

- 풀이
    - 음의 가중치 간선이 있으므로 벨만포드 또는 플로이드 워셜을 사용하여 음의 사이클이 생기는지 확인
    - 이때 플로이드 워셜은 $O(V^3)$, 벨만포드는 $O(V\cdot E)$의 알고리즘을 가지므로, 시간 복잡도가 적은 벨만포드를 선택하는 것이 적절함.
      
- 회고
    - 플로이드 워셜과, 벨만포드 알고리즘을 복습하자.

</details> 

### [BOJ 20040 - 사이클 게임](https://www.acmicpc.net/problem/20040)
<details>
<summary>보기</summary>

- 정보
    - Tier: Gold4
    - Tag: union_find

- 타임라인
    - Problem Open: 09/26 21:40?
    - Tag Open: --/-- --:--
    - Solve: 09/26 22:52

- 풀이
    - 2 ~ m+1번째 각 줄에 노드를 두 개씩 입력받아 두 노드의 루트노드가 같으면 사이클이 생기는 것을 이용하여 해결하는 문제
      
- 회고
    - union_find를 사용하는 문제라는 것은 간파하였으나, 해당 알고리즘을 대략적으로만 이해한 나머지 구현 및 최적화를 제대로 하지 못한 것이 보였던 문제
    - 특히 parent[parent[u]] = parent[v]로 갱신해야 하는것을 최적화 한답시고 parent 배열 이름을 root로 바꾸었다가 root[u] = root[v]로 적어 심각한 논리적 오류가 돋보이는 코드를 제출하였음
    - union_find 복습하자.

</details>

### [BOJ 25916 - 싫은데요](https://www.acmicpc.net/problem/25916)
<details>
<summary>보기</summary>

- 정보
    - Tier: Silver1
    - Tag: two_pointer

- 타임라인
    - Problem Open: 09/27 12:35
    - Tag Open: --/-- --:--
    - Solve: 09/27 12:45

- 풀이
    - 누적합을 구한 후, 투 포인터를 사용하여 M보다 작은 최댓값을 갱신
    - 부여되는 값이 크므로 long long 자료형 사용
      
- 회고
    - 제출 전 검토하기 (자료형 확인, if문 부등호 제대로 확인)

</details>

### [BOJ 18187 - 평면 분할](https://www.acmicpc.net/problem/18187)
<details>
<summary>보기</summary>

- 정보
    - Tier: Silver2
    - Tag: geometry

- 타임라인
    - Problem Open: 09/28 22:40?
    - Tag Open: --/-- --:--
    - Solve: 09/28 22:52

- 풀이
    - 그림판으로 직접 해봄
    - 분할을 최대한 하려면 통과하는 선이 가장 많아야 하는 점을 사용
    - 2 2 3 3 4 5 5 6 7 7 8 9 9.. 로 분할 개수가 규칙적으로 늘어나서 while문 사용하여 간단히 해결
      
- 회고
    - 이게 왜 기하지?

</details>

## 참가한 오픈 콘테스트

### [INU 코드페스티벌 2024](https://www.acmicpc.net/contest/view/1363)
<details>
<summary>보기</summary>

| 문제 | A | B | C | D | E | F | G | H | I | J | K |
|---|---|---|---|---|---|---|---|---|---|---|---|
|결과| AC | WA | AC | AC | AC | WA | - | - | - | - | - | - |

- A번: [양파 실험](https://www.acmicpc.net/problem/32369)
    - 문제를 잘 읽고 구현만 잘 하면 됬던 문제
    - 문제 잘 못 읽고 구현 엉뚱하게 해서 시간 많이 날려먹음

- B번: [Rook](https://www.acmicpc.net/problem/32370)
    - 0,0에서 상하좌우 이동이 가능하고, 아군 폰 위치와, 적군 폰 위치가 주어지면 적 폰을 잡을 수 있는 최소 이동 횟수 구하는 문제
    - A번 처럼 조금만 생각하면 풀 수 있는 문제. 지능이 부족한건지 결국 WA 상태로 끝났는데 알고 보니 if문에 변수를 이상하게 썻음
 
- C번: [샷건](https://www.acmicpc.net/problem/32371)
    - string 입력받아서 상하좌우대각선 true false 여부 확인하고, 해당하는 key값 출력
    - 구현 문제인데 설계 생략하고 키보드 잡았다가 30분 훅감
 
- D번: [마법의 나침반](https://www.acmicpc.net/problem/32372)
    - bruteforce한 문제였다. 위치 하나하나 확인하면서 제대로 조건에 만족하는지만 함수 구현 하면 됬던 문제.
    - 유일하게 깔끔하게 풀었음.
 
- E번: [장난감 자물쇠](https://www.acmicpc.net/problem/32373)
    - 거리가 k인 숫자들만 바꿀 수 있는 배열에서 오름차순 정렬이 가능한지 물었던 문제
    - 생각 안하고 구현문제겠거니 하고 풀다가 틀려서 그제서야 설계 시작함
    - i번째키 % k != i % k 를 만족하는 i가 단 하나라도 있으면 NO, 아니면 YES
 
- F번: [선물 고르기](https://www.acmicpc.net/problem/32374)
    - dp인가 하고 보다가 parametric search로 풀이 시도
    - 대회 다 끝나고 보니 우선순위큐.. 감도 안와서 일단 냅둠

- 회고
    - 처음 30분정도 A~C번 문제를 풀 때 문제를 제대로 안보고, 설계도 제대로 안하다가 시간을 많이 날려먹었음. 반성할 것
    - F번 문제는 접근 잘못된거야 그렇다 치고 구현력이 부족했던 점과, 배열 범위 지정을 제대로 못한 점이 아쉬웠음. 
    - 구현의 핵심은 꼼꼼한 설계부터 나온다.
    - 범위 지정 !!!제발!!! 제대로 하기

</details>

### [2024 충남대학교 SW-IT Contest](https://www.acmicpc.net/contest/view/1379)
<details>
<summary>보기</summary>

| 문제 | A | B | C | D | E | F | G | H | I | J | K | L | M | N | O |
|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|
|결과| AC | - | - | - | - | AC | - | - | - | AC | - | - | - | - | -| - |

- A번: [햄버거 정렬](https://www.acmicpc.net/problem/32399)
    - 3글자 string 받아서 "(1)" 만드는 문제.
    - bruteforce하게 케이스 6개 정도로 나눠서 if else문으로 처리
  
- F번: [일이 커졌어](https://www.acmicpc.net/problem/32404)
    - 크기가 N인 배열에서 숫자 1~n을 배치하여 가장 큰 숫자로 만드는 배열 출력하는 문제
    - ans = 1에서 시작해서 v[i]를 더하거나 곱함. 이때 i가 홀수이면 곱하고, 짝수이면 더함. (i = 1 ~ N)
    - 곱하는 숫자 > 더하는 숫자, 곱하는 숫자는 뒤쪽이 큰 숫자로, 더하는 숫자는 앞쪽이 큰 숫자로 배치
    - 적당히 규칙 찾아서 for문으로 배치하여 출력함

- J번: [대전 도시철도 2호선](https://www.acmicpc.net/problem/32408)
    - 트리에서 1 ~ N번째 노드로 가는 노드 길목(1, N 포함)을 통과하는 두 노드 경우의 수를 찾는 문제 (이때 길목은 해당하는 두 노드에 들어갈 수 없음)
    - dfs로 길목에 해당하는 부분 체크 후, 해당 길목에서 갈라져 나온 서브트리들 각각의 노드 개수 체크하여 for문으로 마무리
    - 정답이 int형으로 하면 오버플로우 나서 long long형으로 해야했음. 정답의 크기 잘 체크하기.
 
- 회고
    - 좀 더 하고싶긴 했는데, 청소시간 + 점호시간 겹쳐서 좀 아쉬움.
    - 꿀팁: 문제는 인쇄해서 풀면 됨

</details>

### [월간 향유회 2024.09](https://www.acmicpc.net/contest/view/1366)
<details>
<summary>보기</summary>

| 문제 | A | B | C | D |
|---|---|---|---|---|
|결과| - | AC | - | - |

- B번: [Coloring 2: Electric Boogaloo](https://www.acmicpc.net/problem/32381)
    - $N \cdot N$칸에서 각 칸마다 앞뒷면으로 흰, 검은 타일이 존재하고, 행동으로 행을 뒤집거나 열을 뒤집을 수 있음. 이때 1~M번째 행동을 했을 때에 따른 검은타일의 개수가 주어지면 무슨 행동을 했는지 출력하는 문제
    - 초기상태 ($N \cdot N$이 전부 흰 타일일 때)부터 어떤 행동을 하는지에 따라 직접 그려보고 규칙성 추론
    - $R$ = row을 검은 타일로 뒤집은 횟수, $C$ = col을 검은 타일로 뒤집은 횟수 일때.. 검은 타일의 개수 = $(R + C) \cdot N - (R \cdot C)$
    - 4가지 행동 패턴으로 구분 후 for문으로 처리
    - 1시간 정도 소모해서 1트만에 깔끔하게 풀긴 했는데, 설계할 때 버벅거려서 조금 아쉬웠음.
 
- 회고
    - 청소시간 시간이 좀 부족해서 한 문제만 풀고 바로 RUN

</details>

## 공부한 내용
- [매개 변수 탐색 (parametric_search)](https://yim2ul2et.github.io/posts/%EC%9D%B4%EB%B6%84%ED%83%90%EC%83%89%EA%B3%BC-%EB%A7%A4%EA%B0%9C%EB%B3%80%EC%88%98%ED%83%90%EC%83%89/)
- 오일러 피 함수 (euler_phi)

## 다음주 목표
- 1Day 1Solve
- 플로이드 워셜, 벨만포드, 유니온 파인드 복습

## 특이사항
- 저와 취미가 같아서 좋았던 해군 병장님께서 9월 29일에 전역하십니다. 짧은 기간이었지만 같이 생활 했던 것이 행복했습니다.. 전역 정말 축하드립니다!!
