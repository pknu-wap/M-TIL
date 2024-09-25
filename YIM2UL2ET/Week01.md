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

### [BOJ 1766 - 문제집](https://www.acmicpc.net/problem/1766)
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

## 공부한 내용

- [매개 변수 탐색 (parametric_search)](https://yim2ul2et.github.io/posts/%EC%9D%B4%EB%B6%84%ED%83%90%EC%83%89%EA%B3%BC-%EB%A7%A4%EA%B0%9C%EB%B3%80%EC%88%98%ED%83%90%EC%83%89/)
- 오일러 피 함수 (euler_phi)

## 다음주 목표
- 1Day 1Solve
- 종만북 읽기

## 특이사항
- 없음
