## 기간
**24.11.04 ~ 24.11.10**

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

## 공부한 내용
- 공부해라

## 다음주 목표
- 블로그 글 올리기
- 실버스트릭

## 특이사항
- 시간이 너무 잘간다..