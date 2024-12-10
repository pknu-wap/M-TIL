## 기간
**24.12.09 ~ 24.12.15**

## 풀었던 문제

### [BOJ 15683 - 감시](https://www.acmicpc.net/problem/15683)
<details>
<summary>보기</summary> 

- 정보
    - Tier: GoldⅢ
    - Tag: 구현

- 타임라인
    - Problem Open: 12/10 18:30?
    - Tag Open: --/-- --:--
    - Solve: 12/10 20:11

- 풀이
    - 깡구현

- 회고
    - 함수명 잘짓기, 범위 지정시 한번 더 보기 (for문 사용시)
    - 구현은 설계다
 
- 코드
  - ```cpp
    #include <iostream>
    #include <vector>
    
    using namespace std;
    
    int N, M;
    
    vector <vector <vector <int>>> direction {
        {{1}, {2}, {3}, {4}}, 
        {{1, 3}, {2, 4}},
        {{1, 2}, {2, 3}, {3, 4}, {4, 1}}, 
        {{1, 2, 3}, {2, 3, 4}, {3, 4, 1}, {4, 1, 2}}, 
        {{1, 2, 3, 4}}
    };
    
    vector <vector <char>> fillingField(vector <vector <char>> field, int r, int c, vector <int> &vec) {
        for (auto &d : vec) {
            if (d == 1) {   // left
                for (int i = c; i >= 0; i--) {
                    if (field[r][i] == '0') {
                        field[r][i] = '#';
                    } else if (field[r][i] == '6') {
                        break;
                    } 
                }
            } else if (d == 2) {    // up
                for (int i = r; i >= 0; i--) {
                    if (field[i][c] == '0') {
                        field[i][c] = '#';
                    } else if (field[i][c] == '6') {
                        break;
                    } 
                }
            } else if (d == 3) {    // right
                for (int i = c; i < M; i++) {
                    if (field[r][i] == '0') {
                        field[r][i] = '#';
                    } else if (field[r][i] == '6') {
                        break;
                    } 
                }
            } else if (d == 4) {    // down
                for (int i = r; i < N; i++) {
                    if (field[i][c] == '0') {
                        field[i][c] = '#';
                    } else if (field[i][c] == '6') {
                        break;
                    } 
                }
            }
        }
        return field;
    }
    
    int checkField(vector <vector <char>> &field) {
        int result = 0;
        for (auto &row : field) {
            for (auto &ch : row) {
                if (ch == '0') result++;
            }
        }
        return result;
    }
    
    int dfs(vector <vector <char>> &field, int r, int c) {
        int result = 1e9;
    
        for (int k = r * M + c; k < N * M; k++) {
            int i = k / M, j = k % M;
            if ('1' > field[i][j] || field[i][j] > '5') continue;
            
            for (auto &v : direction[field[i][j] - '1']) {
                auto newField = fillingField(field, i, j, v);
                result = min(result, dfs(newField, i, j + 1));
            }
            return result;
        }
    
        return checkField(field);
    }
    
    int main() {
        ios_base::sync_with_stdio(false);
        cin.tie(NULL); cout.tie(NULL);
    
        cin >> N >> M;
        vector <vector <char>> field(N, vector <char> (M));
        for (auto &row : field) {
            for (auto &ch : row) {
                cin >> ch;
            }
        }
    
        cout << dfs(field, 0, 0);
        return 0;
    }
    ```

</details>

### [BOJ 1135 - 뉴스 전하기](https://www.acmicpc.net/problem/1135)
<details>
<summary>보기</summary> 

- 정보
    - Tier: GoldⅡ
    - Tag: tree_dp, greedy

- 타임라인
    - Problem Open: 12/10 22:15?
    - Tag Open: --/-- --:--
    - Solve: 12/10 22:46

- 풀이
    - 거꾸로 역행해서 리프노드부터 시작하여 올라가는 형식으로 풀이
    - $i$번 노드의 차수가 $0$이 되면 $parent[i]$번노드의 차수를 $-1$
    - 이때 전화는 중복으로 걸 수 없으므로 중복되지 않도록 큐와 해시맵을 적절히 사용

- 회고
    - 나중가서 해당 문제가 한번 더 나오면 이런 풀이가 생각날까..? -> 한번 더보자.
    - 코드 정리좀 해야할듯
 
- 코드
  - ```cpp
    #include <iostream>
    #include <queue>
    #include <unordered_set>
    #include <vector>
    
    using namespace std;
    
    int N;
    vector <int> parent;
    vector <int> degree;
    
    int main() {
        cin >> N;
    
        parent.resize(N);
        degree.resize(N);
    
        cin >> parent[0];
        for (int i = 1; i < N; i++) {
            cin >> parent[i];
            degree[parent[i]]++;
        }
    
        int ans = 0;
        unordered_set <int> isVst;
        while (degree[0] != 0) {
            unordered_set <int> uos;
            queue <int> que;
    
            for (int i = 1; i < N; i++) {
                if (degree[i] == 0 && isVst.find(i) == isVst.end() && uos.find(parent[i]) == uos.end() && degree[parent[i]] > 0) {
                    que.push(parent[i]);
                    uos.insert(parent[i]);
                    isVst.insert(i);
                }
            }
    
            while (!que.empty()) {
                degree[que.front()]--;
                que.pop();
            }
            
            ans++;
        }
    
        cout << ans;
        return 0;
    }
    ```

</details>

## 공부한 내용
- 공부한 내용 노트

## 다음주 목표
- 문제만 풀지 말고 공부한거 정리하기

## 특이사항
- 2층침대를 1층침대로 바꾸는 생활관 대공사 진행중
