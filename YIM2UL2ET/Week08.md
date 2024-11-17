## 기간
**24.11.11 ~ 24.11.17**

## 풀었던 문제

### [BOJ 1099 - 알 수 없는 문장](https://www.acmicpc.net/problem/1099)
<details>
<summary>보기</summary> 

- 정보
    - Tier: GoldⅢ
    - Tag: DP

- 타임라인
    - Problem Open: 11/12 12:00?
    - Tag Open: 11/12 12:00?
    - Solve: 11/12 12:50

- 풀이
    - memo[i] = i번째 문자부터 시작하는 문장의 최솟값
    - 코드 참조

- 회고
    - 범위 제대로..
    - [더 나은 방식](https://www.acmicpc.net/source/84850016) -> 정렬하여 문자의 개수가 일치하는지 확인하는 방법
 
- 코드
  - ```cpp
    #include <iostream>
    #include <vector>
    
    #define MAX_COST 51
    
    using namespace std;
    
    int N;
    string target;
    vector <string> words;
    vector <int> minValue;
    
    int getCost(string &str1, string &str2) {
        if (str1.size() != str2.size()) return -1;
    
        // count alphabet EA
        vector <int> alpha1(26);
        vector <int> alpha2(26);
        for (int i = 0; i < int(str1.size()); i++) {
            alpha1[str1[i] - 'a']++;
            alpha2[str2[i] - 'a']++;
        }
    
        // count cost
        int result;
        if (alpha1 == alpha2) {
            result = 0;
            for (int i = 0; i < int(str1.size()); i++) {
                if (str1[i] != str2[i]) result++;
            }
        } else {
            result = -1;
        }
    
        return result;
    }
    
    int solve(int start) {
        if (start == int(target.size())) return 0;
    
        int &ret = minValue[start];
        if (ret == -1) {
            ret = MAX_COST;
    
            for (string &word : words) {
                string str = target.substr(start, word.size());
                int cost = getCost(str, word);
    
                if (cost == -1) continue;
                ret = min(ret, cost + solve(start + word.size()));
            }
        }
        return ret;
    }
    
    int main() {
        // fastIO
        ios_base::sync_with_stdio(false);
        cin.tie(NULL); cout.tie(NULL);
    
        // init && input;
        cin >> target >> N;
    
        words.resize(N);
        minValue.resize(int(target.size()), -1);
    
        for (string &str : words) {
            cin >> str;
        }
    
        // solve
        int ans = solve(0);
        cout << (ans == MAX_COST ? -1 : ans);
        return 0;
    }
    ```

</details>

### [BOJ 1029 - 그림 교환](https://www.acmicpc.net/problem/1029)
<details>
<summary>보기</summary> 

- 정보
    - Tier: GoldⅠ
    - Tag: dp_bit

- 타임라인
    - Problem Open: 11/13 12:00?
    - Tag Open: 11/13 12:20? (DP)
    - Solve: 11/13 22:19

- 풀이
    - 3차원 DP 사용
    - $cache[i][j][k] = \lbrace start = i, curCost = j, vst = k\rbrace$에서 최대 사람의 수
    - $vst$는 방문 체크 배열을 비트마스킹을 사용하는 방식으로 활용한 것 ($= vector \<bool\> vst$)

- 회고
    - 실 풀이시간 약 1시간 (자력솔)
    - 비트마스킹 정리하자 (2트)
 
- 코드
  - ```cpp
    #include <iostream>
    #include <vector>
    
    using namespace std;
    
    int N;
    vector <vector <int>> cost;
    vector <vector <vector <int>>> cache;
    
    int findMaxVal(int start, int curCost, int vst) {
        vst |= (1 << start);
        if (curCost == 10) return 1;
        
        int &ret = cache[start][curCost][vst];
        if (ret == -1) {
            ret = 1;
            for (int i = 0; i < N; i++) {
                if (start == i) continue;
                if ((vst & (1 << i)) || cost[start][i] < curCost) continue;
                
                ret = max(ret, findMaxVal(i, cost[start][i], vst) + 1);
            }
        }
        return ret;
    }
    
    int main() {
        // fastIO
        ios_base::sync_with_stdio(false);
        cin.tie(NULL); cout.tie(NULL);
    
        // init && input
        cin >> N;
        cost.resize(N, vector <int> (N));
        cache.resize(N, vector <vector <int>> (10, vector <int> (1 << N, -1)));
        
        char ch;
        for (auto &row : cost) {
            for (auto &el : row) {
                cin >> ch;
                el = int(ch - '0');
            }
        }
    
        // solve
        cout << findMaxVal(0, 0, 0);
        return 0;
    }
    ```

</details>

### [BOJ 2611 - 자동차 경주](https://www.acmicpc.net/problem/2611)
<details>
<summary>보기</summary> 

- 정보
    - Tier: GoldⅡ
    - Tag: dp, topological_sorting

- 타임라인
    - Problem Open: 11/13 22:20
    - Tag Open: 11/13 22:20 (DP)
    - Solve: 11/13 22:47

- 풀이
    - $cache[i] =  i$번 지점에서 출발하여 1번 지점으로 도착 시 얻을 수 있는 최대 코스트
    - 0번을 출발지점으로, 1번을 도착지점으로 잡아 구현
    - 재귀호출시 최댓값을 얻을 수 있는 경로까지 갱신해주어 최댓값을 얻을 수 있는 경로 (0 -> 1) 출력

- 회고
    - 최적해를 얻는 것 뿐만 아니라 최적해를 얻는 과정까지 출력하는 문제 연습하면 좋을 것 같다.
    - [위상정렬 풀이](https://www.acmicpc.net/source/74570248)
 
- 코드
  - ```cpp
    #include <iostream>
    #include <vector>
    
    using namespace std;
    
    int N, M;
    vector <vector <pair <int, int>>> graph;
    vector <int> cache;
    vector <int> path;
    
    int getMaxCost(int start) {
        int &ret = cache[start];
        if (ret == -1) {
            for (auto &p : graph[start]) {
                if (ret < getMaxCost(p.second) + p.first) {
                    ret = getMaxCost(p.second) + p.first;
                    path[start] = p.second;
                }
            }
        }
        return ret;
    }
    
    void outputPath() {
        vector <bool> vst(N + 1, false);
        int curV = 0;
        while (!vst[curV]) {
            vst[curV] = true;
            cout << (curV == 0 ? 1 : curV) << ' ';
            curV = path[curV];
        }
    }
    
    int main() {
        // fastIO
        ios_base::sync_with_stdio(false);
        cin.tie(NULL); cout.tie(NULL);
    
        // init && input
        cin >> N >> M;
    
        graph.resize(N + 1);
        cache.resize(N + 1, -1);
        path.resize(N + 1);
    
        int p, q, r;
        for (int i = 0; i < M; i++) {
            cin >> p >> q >> r;
            graph[p].push_back({r, q});
        }
    
        // solve && output
        cache[1] = 0;
        graph[0] = graph[1];    // start = 0, end = 1
    
        cout << getMaxCost(0) << '\n';
        outputPath();
        
        return 0;
    }
    ```

</details>

</details>

### [BOJ 13168 - 내일로 여행](https://www.acmicpc.net/problem/13168)
<details>
<summary>보기</summary> 

- 정보
    - Tier: GoldⅢ
    - Tag: hash_map, floyd_warshall, implemention

- 타임라인
    - Problem Open: 11/17 16:30?
    - Tag Open: --/-- --:--
    - Solve: 11/17 19:34

- 풀이
    - 해시맵, 플로이드 워셜 사용하여 구현

- 회고
    - 실 풀이 약 1시간 반?
    - 연습 안하니깐 구현 & 디버깅 능력이 확 떨어지네
 
- 코드
  - ```cpp
    #include <iostream>
    #include <unordered_set>
    #include <unordered_map>
    #include <vector>
    
    #define INF 1e9 * 2
    
    using namespace std;
    
    struct transport{
        string type;
        int start, end, cost;
    };
    
    int N, M, R, K;
    vector <int> path;
    vector <transport> graph;
    
    pair <long long, long long> getCost() {
        // 내일로 Tickets Init
        unordered_set <string> freeTicket{"Mugunghwa", "ITX-Cheongchun", "ITX-Saemaeul"};
        unordered_set <string> discountTicket{"S-Train", "V-Train"};
    
        // init cache
        vector <vector <long long>> dist1(N, vector <long long> (N, INF));    // 내일로 X
        vector <vector <long long>> dist2(N, vector <long long> (N, INF));    // 내일로 O
    
        for (int i = 0; i < N; i++) {
            dist1[i][i] = 0;
            dist2[i][i] = 0;
        }
    
        for (auto &e : graph) {
            dist1[e.start][e.end] = min(dist1[e.start][e.end], (long long)e.cost * 2);
    
            if (freeTicket.find(e.type) != freeTicket.end()) {
                dist2[e.start][e.end] = min(dist2[e.start][e.end], (long long)0);
            } else if (discountTicket.find(e.type) != discountTicket.end()) {
                dist2[e.start][e.end] = min(dist2[e.start][e.end], (long long)e.cost);
            } else {
                dist2[e.start][e.end] = min(dist2[e.start][e.end], (long long)e.cost * 2);
            }
        }
    
        // floyd
        for (int mid = 0; mid < N; mid++) {
            for (int start = 0; start < N; start++) {
                for (int end = 0; end < N; end++) {
                    dist1[start][end] = min(dist1[start][end], dist1[start][mid] + dist1[mid][end]);
                    dist2[start][end] = min(dist2[start][end], dist2[start][mid] + dist2[mid][end]);
                }
            }
        }
    
        // find totalCost
        long long result1 = 0, result2 = R * 2;
        for (int i = 1; i < M; i++) {
            result1 += dist1[path[i - 1]][path[i]];
            result2 += dist2[path[i - 1]][path[i]];
        }
        
        // return
        return {result1, result2};
    }
    
    void input() {
        // N, R input
        cin >> N >> R;
        
        // hash setting
        string str;
        unordered_map <string, int> stationHash;
        for (int i = 0; i < N; i++) {
            cin >> str;
            stationHash.insert({str, i});
        }
        
        // path input
        cin >> M;
        path.resize(M);
        for (auto &p : path) {
            cin >> str;
            p = stationHash[str];
        }
    
        // ticket input
        cin >> K;
        int cost;
        string type, start, end;
        for (int i = 0; i < K; i++) {
            cin >> type >> start >> end >> cost;
            graph.push_back({type, stationHash[start], stationHash[end], cost});
            graph.push_back({type, stationHash[end], stationHash[start], cost});
        }
    }
    
    int main() {
        // fastIO
        ios_base::sync_with_stdio(false);
        cin.tie(NULL); cout.tie(NULL);
    
        // init && input
        input();
    
        // solve
        auto ans = getCost();
        if (ans.first > ans.second) {
            cout << "Yes";
        } else {
            cout << "No";
        }
        
        return 0;
    }
    ```

</details>

## 공부한 내용
- 아무것도 한게 엄서요.. 흑흑.. (책 깔짝깔짝 읽기)

## 다음주 목표
- DP 마무리 + 정리글 올리기
- 실버스트릭 잇기

## 특이사항
- 시간이 너무 잘간다..
- 드디어 태블릿 인가받음
