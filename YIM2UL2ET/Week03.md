## 기간
**24.10.07 ~ 24.10.13**

## 풀었던 문제

### [BOJ 1874 - 스택 수열](https://www.acmicpc.net/problem/1874)
<details>
<summary>보기</summary> 

- 정보
    - Tier: Silver Ⅱ
    - Tag: stack

- 타임라인
    - Problem Open: 10/07 20:30
    - Tag Open: 10/07 20:30
    - Solve: 10/07 20:49

- 풀이
    - 스택을 활용하여 푸는 간단한 문제
    ```cpp
    int k = 1;
    for (int i = 0; i < N; i++) {
        cin >> num;
        while (1) {
            if (!stk.empty() && stk.top() == num) {
                stk.pop();
                ans += '-';
                break;
            } else if (k <= num){
                stk.push(k++);
                ans += '+';
            } else {
                cout << "NO";
                return 0;
            }
        }
    }
    ```

- 회고
    - 설계하자

</details>

### [BOJ 4358 - 생태학](https://www.acmicpc.net/problem/4358)
<details>
<summary>보기</summary> 

- 정보
    - Tier: Silver Ⅱ
    - Tag: hash_map

- 타임라인
    - Problem Open: 10/08 19:26
    - Tag Open: --/-- --:--
    - Solve: 10/08 19:36

- 풀이
    - 1. 해시맵 사용하여 나무가 입력받은 횟수 갱신
    - 2. 이름순으로 정렬
    - 3. 해당 나무의 개수 / 총 입력 개수 출력
    - 입력시 getline, 출력시 cout << fixed 사용

- 회고
    - map 정렬시 vector로 변경 후 정렬 (map 컨테이너는 STL sort로 정렬 불가능함.)
    - ```vector <pair <string, int>> vec(mp.begin(), mp.end()); ```

</details>

### [BOJ 1976 - 여행가자](https://www.acmicpc.net/problem/1976)
<details>
<summary>보기</summary> 

- 정보
    - Tier: Gold Ⅳ
    - Tag: union_find

- 타임라인
    - Problem Open: --/-- --:--
    - Tag Open: --/-- --:--
    - Solve: 10/09 12:18

- 풀이
    - union find를 사용하여 여행 계획에 속한 M개의 노드의 루트노드가 전부 같으면 YES, 아니면 NO

- 회고
    - union find 복습

</details>

### [BOJ 17942 - 알고리즘 공부](https://www.acmicpc.net/problem/17942)
<details>
<summary>보기</summary> 

- 정보
    - Tier: Gold Ⅰ
    - Tag: priority_queue, greedy

- 타임라인
    - Problem Open: --/-- --:--
    - Tag Open: --/-- --:--
    - Solve: 10/10 14:34

- 풀이
    - 알고리즘을 공부하는 데에 드는 M개의 cost의 최솟값들을 우선순위 큐로 뽑아낸다.
    - 우선순위 큐에서 cost를 뽑을 때, 이미 공부한 알고리즘이면 스킵하고, 공부하지 않았다면 이 알고리즘을 공부했을 때 줄어드는 다른 알고리즘을 cost값을 계산하여 다시 집어넣음.
    - 해당 방식이 가능한 이유는 구하는 정답이 M개의 cost들 중 최댓값을 구하는 것이기 때문. (누적되는 값이 아니다.)

- 회고
    - 중복으로 큐에 집어 넣을 때 방문처리 안해서 한번 틀렸었음. (중복처리 반드시 하자)

</details>

### [BOJ 2307 - 도로검문](https://www.acmicpc.net/problem/2307)
<details>
<summary>보기</summary> 

- 정보
    - Tier: Gold Ⅰ
    - Tag: dijkstra

- 타임라인
    - Problem Open: --/-- --:--
    - Tag Open: --/-- --:--
    - Solve: 10/10 15:27

- 풀이
    - ```cpp
      int dijkstra(int u, int v) {
        vector <int> dist(N + 1, INF);
        priority_queue <pair <int, int>> pq;
    
        dist[1] = 0;
        pq.push({0, 1});
    
        while (!pq.empty()) {
            int cur_cost = -pq.top().first;
            int cur_node = pq.top().second;
            pq.pop();
    
            if (cur_cost > dist[cur_node]) continue;
    
            for (auto &e : graph[cur_node]) {
                int nxt_cost = e.second + dist[cur_node];
                int nxt_node = e.first;
                
                if ((nxt_node == u && cur_node == v) || (nxt_node == v && cur_node == u)) continue;
                
                if (nxt_cost < dist[nxt_node]) {
                    dist[nxt_node] = nxt_cost;
                    pq.push({-nxt_cost, nxt_node});
                    if (u == 0 && v == 0) check_edge.push_back({cur_node, nxt_node});
                }
            }
        }
    
        return dist[N];
      }
      ```
      
    - u와 v를 잇는 에지를 검문한다고 했을 때, 매개변수로 (u, v)를 넣어 다익스트라를 사용 시 해당 에지는 스킵하는 형태로 변형
    - 검문하는 에지가 없다면, 실제로는 없는 노드 (ex. 0)를 매개변수로 넣어 사용
    - (0, 0)을 매개변수로 넣는다면 최단 경로가 갱신된 에지들을 check_edge라는 vector에 push
    - 해당 다익스트라 함수를 사용하여 `check_edge에 저장된 에지들을 각각 검문했을 때 최단경로의 최댓값` - `검문이 없을 때 최단경로`가 정답 (물론 무한대의 경우도 체크하여 -1이 나올 경우도 대비)

- 회고
    - 모든 에지를 체크하지 않고, 원래 최단 경로에 활용된 에지만 체크하면 시간복잡도를 줄일 수 있다. (https://dmsvk01.tistory.com/98)
    - 위 테크닉을 생각하지 못하고 헤맸었던게 좀 아쉽다.

</details>

### [BOJ 16946 - 벽 부수고 이동하기 4](https://www.acmicpc.net/problem/16946)
<details>
<summary>보기</summary> 

- 정보
    - Tier: Gold Ⅱ
    - Tag: graph_traversal

- 타임라인
    - Problem Open: 10/12 22:00
    - Tag Open: --/-- --:--
    - Solve: 10/12 22:59

- 풀이
    - DFS로 풀이
    - 깡으로 탐색 돌려버리면 시간초과 나기 때문에 벽이 아닌 부분들(0)을 먼저 DFS 돌려서 지역화 (0 ~ K번 까지 locNum이라는 vector에 저장)
    - 각 지역의 크기는 memo라는 vector에 저장
    - 이후 벽들(1)을 하나씩 체크하여 (인접한 지역들의 크기들 + 1) % 10을 ans라는 vector에 저장 (이때 상하좌우 지역들이 중복을 확인하기 위하여 set 사용)

- 회고
    - input할때 int형으로 cin으로 받았다가 헤맸음. (값이 붙어있기 때문에 char형으로 받은 후 - '0' 처리)
    - 실제로는 ans에 mod10 처리 안하고, 출력시에 mod10 처리하여 출력

</details>

### [BOJ 2143 - 두 배열의 합](https://www.acmicpc.net/problem/2143)
<details>
<summary>보기</summary> 

- 정보
    - Tier: Gold Ⅲ
    - Tag: hash_set

- 타임라인
    - Problem Open: 10/13 18:00?
    - Tag Open: --/-- --:--
    - Solve: 10/13 18:17

- 풀이
    - A와 B의 누적합을 각각 저장한 후, 2중for문을 사용하여 각각의 subset의 누적합들을 subsetA_sums, subsetB_sums라는 해시맵에 저장
    - map.first == subset의 누적합, map.second == first가 나오는 경우의 수
    - 이후 for문을 사용하여 두 해시맵의 원소의 key값의 합이 $T$이면, 해당 원소의 value값을 서로 곱하여 long long형 변수인 answer에 더해나감.

- 회고
    - 정답의 크기를 조사하지 않아 오버플로우가 났었음. (long long형 사용해야 함)

</details>

### [BOJ 2252 - 줄 세우기](https://www.acmicpc.net/problem/2252)
<details>
<summary>보기</summary> 

- 정보
    - Tier: Gold Ⅲ
    - Tag: topological_sorting

- 타임라인
    - Problem Open: 10/13 18:20?
    - Tag Open: 10/13 19:45?
    - Solve: 10/13 19:03

- 풀이
    - 전형적인 위상정렬 문제이다.

- 회고
    - 근데 그 전형적인 위상정렬 문제인줄 모르고 해맸음. (다시 공부해야겠지?)

</details>

## 특이사항
- 10/08 ~ 10/11 휴가
- 책좀읽자
