## 기간
**24.10.21 ~ 24.10.27**

## 풀었던 문제

### [BOJ 3967 - 매직 스타](https://www.acmicpc.net/problem/3967)
<details>
<summary>보기</summary> 

- 정보
    - Tier: GoldⅤ
    - Tag: bruteforcing, backtracking, implementation

- 타임라인
    - Problem Open: 10/21 --:--?
    - Tag Open: 10/21 --:--?
    - Solve: 10/22 22:55

- 풀이
    - 코드로 대체

- 회고
    - 이렇게까지 오래 걸릴 문제가 아니었는데.. 구현에 문제가 있었는지 뭔가 자꾸 잘못되서 도중에 한번 코드 갈아엎음
    - 설계를 잘하자 + 구현력 키우기
 
- 코드
    - ```cpp
      #include <iostream>
      #include <vector>
      
      using namespace std;
      
      vector <bool> numIsIt(12);
      vector <bool> coordIsIt(12);
      
      vector <string> magicStar(5);
      
      vector <pair <int, int>> coord;
      
      vector <pair <int, int>> dpIdx{{0,1}, {3,4}, {0,3}, {1,3}, {3,5}, {0,4},
                                     {1,5}, {0,2}, {2,4}, {2,5}, {1,2}, {4,5}};
      vector <int> memo(6);
      
      bool check() {
          for (auto &el : memo) {
              if (el != 26) return false;
          }
          return true;
      }
      
      bool recursion(int coordIdx) {
          while (coordIdx < 12 && coordIsIt[coordIdx]) coordIdx++;
          if (coordIdx == 12) return check();
      
          for (int i = 0; i < 12; i++) {
              if (numIsIt[i]) continue;
              numIsIt[i] = true;
              memo[dpIdx[coordIdx].first] += i + 1; memo[dpIdx[coordIdx].second] += i + 1;
              magicStar[coord[coordIdx].first][coord[coordIdx].second] = char(i + 'A');
      
              if (recursion(coordIdx + 1)) return true;
              numIsIt[i] = false;
              memo[dpIdx[coordIdx].first] -= i + 1; memo[dpIdx[coordIdx].second] -= i + 1;
              magicStar[coord[coordIdx].first][coord[coordIdx].second] = 'x';
          }
      
          return false;
      }
      
      int main() {
          // fastIO
          ios_base::sync_with_stdio(false);
          cin.tie(NULL); cout.tie(NULL);
      
          // init && input
          for (auto &str : magicStar) {
              cin >> str;
          }
      
          for (int i = 0; i < 5; i++) {
              for (int j = 0; j < 9; j++) {
                  if (magicStar[i][j] == '.') continue;
                  coord.push_back({i,j});
      
                  if (magicStar[i][j] == 'x') continue;
                  auto p = dpIdx[coord.size() - 1];
                  memo[p.first] += int(magicStar[i][j] - 'A' + 1);
                  memo[p.second] += int(magicStar[i][j] - 'A' + 1);
      
                  numIsIt[int(magicStar[i][j] - 'A')] = true;
                  coordIsIt[coord.size() - 1] = true;
              }
          }
      
          // solve
          recursion(0);
      
          // output
          for (auto &str : magicStar) {
              cout << str << '\n';
          }
          return 0;
      }
      ```

</details>

### [BOJ 3019 - 테트리스](https://www.acmicpc.net/problem/3019)
<details>
<summary>보기</summary> 

- 정보
    - Tier: GoldⅤ
    - Tag: bruteforcing, implementation

- 타임라인
    - Problem Open: 10/22 22:56
    - Tag Open: 10/22 22:56
    - Solve: 10/22 23:24

- 풀이
    - 블럭의 바닥부분이 전부 필드와 맞닿아야 하므로 높이 중심으로 구현
    - 각 블럭이 놓을 수 있는 방식에 필요한 필드 높이를 2차원 배열로 하여 총 3차원 배열로 초기화하여 풀이
    

- 회고
    - for문 범위 확인하기 정도? 주의하기

- 코드
    - ```cpp
      #include <iostream>
      #include <vector>
      
      using namespace std; 
      
      int N, M;
      
      vector <int> fieldHeight;
      
      vector <vector <vector <int>>> blocks{ {},
          { {0}, {0, 0, 0, 0} },
          { {0, 0} },
          { {0, 0, -1}, {-1, 0} },
          { {-1, 0, 0}, {0, -1} },
          { {0, 0, 0}, {-1, 0}, {0, -1}, {-1, 0, -1} },
          { {0, 0, 0}, {-2, 0}, {0, -1, -1}, {0, 0} },
          { {0, 0, 0}, {0, 0}, {-1, -1, 0}, {0, -2} }
      };
      
      bool checkCorrectPut(int fieldLoc, vector <int> &type) {
          vector <int> newHeights{type[0] + fieldHeight[fieldLoc]};
          for (int i = 1; i < int(type.size()); i++) {
              newHeights.push_back(type[i] + fieldHeight[fieldLoc + i]);
              if (newHeights[i - 1] != newHeights[i]) return false;
          }
          return true;
      }
      
      int main() {
          // fastIO
          ios_base::sync_with_stdio(false);
          cin.tie(NULL); cout.tie(NULL);
      
          // init && input
          cin >> N >> M;
      
          auto targetBlock = blocks[M];
          fieldHeight.resize(N);
      
          for (int &el : fieldHeight) {
              cin >> el;
          }
      
          // solve
          int ans = 0;
          for (auto type : targetBlock) {
              for (int i = 0; i <= N - int(type.size()); i++) {
                  if (checkCorrectPut(i, type)) ans++;
              }
          }
          
          // output
          cout << ans;
          return 0;
      }
      ```

</details>

### [BOJ 12100 - 2048 (Easy)](https://www.acmicpc.net/problem/12100)
<details>
<summary>보기</summary> 

- 정보
    - Tier: GoldⅠ
    - Tag: bruteforcing, implementation, backtracking

- 타임라인
    - Problem Open: 10/23 12:00
    - Tag Open: 10/23 12:00
    - Solve: 10/23 22:12

- 풀이
    - 깡 시뮬레이션 구현 문제
    - 주의할점: 한번의 이동에서 합쳐진 블록은 또 합쳐질 수 없음 -> bool형 배열로 처리
  
- 회고
    - 실 풀이시간 약 100분
    - 설계시 주의해야 할 사항을 한번 더 확인하자. (요구 조건 확인)

- 코드
  - ```cpp
    #include <iostream>
    #include <vector>
    
    using namespace std;
    
    int N;
    const vector <pair <int, int>> offset{{0,-1}, {0,1}, {-1,0}, {1,0}};    // left, right, up, down 순
    
    int findMaxValue(vector <vector <int>> &board) {
        int result = 0;
    
        for (auto &row : board) {
            for (auto &el : row) {
                result = max(result, el);
            }
        }
        return result;
    }
    
    bool checkCorrectLoc(int r, int c) {
        return 0 <= r && r < N && 0 <= c && c < N;
    }
    
    void move(vector <vector <int>> &board, vector <vector <bool>> &isAdd, int curR, int curC, int direction) { // 완
        int setR = offset[direction].first;
        int setC = offset[direction].second;
    
        while (checkCorrectLoc(curR + setR, curC + setC)) {
            int nxtR = curR + setR;
            int nxtC = curC + setC;
            
            if (board[nxtR][nxtC] == 0) {
                swap(board[nxtR][nxtC], board[curR][curC]);
            } else {
                if (board[nxtR][nxtC] == board[curR][curC] && !isAdd[nxtR][nxtC]) {
                    isAdd[nxtR][nxtC] = true;
                    board[nxtR][nxtC] *= 2;
                    board[curR][curC] = 0;
                }
                break;
            }
    
            curR = nxtR;
            curC = nxtC;
        }
    }
    
    vector <vector <int>> tilt(vector <vector <int>> &board, int direction) {    // 완
        auto newBoard = board;
        vector <vector <bool>> isAdd(N, vector <bool> (N, false));
    
        if (direction == 0) {   // left
            for (int c = 0; c < N; c++) {
                for (int r = 0; r < N; r++) {
                    if (newBoard[r][c] == 0) continue;
                    move(newBoard, isAdd, r, c, direction);
                }
            }
        } else if (direction == 1) {    // right
            for (int c = N-1; c > -1; c--) {
                for (int r = N-1; r > -1; r--) {
                    if (newBoard[r][c] == 0) continue;
                    move(newBoard, isAdd, r, c, direction);
                }
            }
        } else if (direction == 2) {    // up
            for (int r = 0; r < N; r++) {
                for (int c = 0; c < N; c++) {
                    if (newBoard[r][c] == 0) continue;
                    move(newBoard, isAdd, r, c, direction);
                }
            }
        } else {    // down
            for (int r = N-1; r > -1; r--) {
                for (int c = N-1; c > -1; c--) {
                    if (newBoard[r][c] == 0) continue;
                    move(newBoard, isAdd, r, c, direction);
                }
            }
        }
    
        return newBoard;
    }
    
    int backtracking(vector <vector <int>> &board, int cnt) {   // 완
        if (cnt == 0) return findMaxValue(board);
    
        int ans = 0;
        for (int i = 0; i < 4; i++) {
            auto newBoard = tilt(board, i);
            ans = max(ans, backtracking(newBoard, cnt - 1));
        }
        return ans;
    }
    
    int main() {    // 완
        // fastIO
        ios_base::sync_with_stdio(false);
        cin.tie(NULL); cout.tie(NULL);
    
        // init && input
        cin >> N;
    
        vector <vector <int>> board(N, vector <int> (N));
        for (auto &row : board) {
            for (auto &el : row) {
                cin >> el;
            }
        }
    
        // solve
        cout << backtracking(board, 5);
        return 0;
    }
      ```

</details>

## 공부한 내용
- 종만북 Ch05 ~ Ch07 (알고리즘의 정당성 증명 방법, 브루트포스(복습), 분할정복(복습))

## 다음주 목표
- 분할정복 위주로 내실 쌓기
- 종만북 Ch08 (DP)

## 특이사항
- 구현력부족, 능지부족, 귀차니즘 삼위일체로 벽을 느끼고 있는중
- 템플릿에 코드 부분 추가
