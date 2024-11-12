## 기간
**24.11.04 ~ 24.11.10**

## 풀었던 문제

### [BOJ 24395 - 명진이의 신년계획](https://www.acmicpc.net/problem/24395)
<details>
<summary>보기</summary> 

- 정보
    - Tier: GoldⅢ
    - Tag: DP

- 타임라인
    - Problem Open: 11/05 22:00
    - Tag Open: 11/05 22:00 (DP)
    - Solve: 11/05 23:03

- 풀이
    - 알약의 개수에 따라 가질 수 있는 최댓값 경우의 수는 2500가지, 학생의 수는 최대 10만명이므로 비둘기집 원리에 의해 중복되는 것이 반드시 존재
    - 따라서 먼저 처방 알약의 종류에 따른 최댓값을 먼저 만든 후, 이에 따른 위험도를 대응 후 정렬
    - $memo[i][j][k] =$ $i$번째 질병까지 보았을 때 빨간 약 $j$개와, 파란 약 $k$개를 받는 최대 위험도 (코드 참조)
    - 실제 풀이는 2차원 배열로 curMemo와 nxtMemo를 사용하여 배열 복사를 활용하여 진행

- 회고
    - 풀이는 금방 생각났으나 구현에 버벅임.
    - 조건도 확실히 봐가며 풀이하자.
 
- 코드
  - ```cpp
    #include <iostream>
    #include <vector>
    #include <algorithm>
    
    using namespace std;
    
    struct disease { int blueM, redM, risk; };
    struct student { int num, blueM, redM, risk; };
    
    int N, M;
    vector <student> studentVec;
    vector <disease> diseaseVec;
    vector <vector <int>> memo;
    
    void findMaxRisk() {
        memo.resize(51, vector <int> (51, -1));
        memo[0][0] = 0;
    
        for (int i = 0; i < M; i++) {
            auto nxtMemo = memo;
            auto &curD = diseaseVec[i];
            
            for (int r = curD.redM; r <= 50; r++) {
                for (int b = curD.blueM; b <= 50; b++) {
                    if (memo[r - curD.redM][b - curD.blueM] == -1) {
                        nxtMemo[r][b] = memo[r][b];
                    } else {
                        nxtMemo[r][b] = max(memo[r][b], memo[r - curD.redM][b - curD.blueM] + curD.risk);
                    }
                }
            }
    
            memo = nxtMemo;
        }
    }
    
    void getStudentsRisk() {
        for (auto &p : studentVec) {
            p.risk = (memo[p.redM][p.blueM] == -1 ? 0 : memo[p.redM][p.blueM]);
        }
    }
    
    int main() {
        // fastIO
        ios_base::sync_with_stdio(false);
        cin.tie(NULL); cout.tie(NULL);
    
        // init && input
        cin >> N >> M;
    
        studentVec.resize(N);
        diseaseVec.resize(M);
    
        for (int i = 0; i < M; i++) {
            cin >> diseaseVec[i].redM >> diseaseVec[i].blueM >> diseaseVec[i].risk;
        }
    
        for (int i = 1; i <= N; i++) {
            cin >> studentVec[i - 1].redM >> studentVec[i - 1].blueM;
            studentVec[i - 1].num = i;
        }
    
        // solve
        findMaxRisk();
        getStudentsRisk();
    
        sort(studentVec.begin(), studentVec.end(), [](student &p1, student &p2) -> bool {
            if (p1.risk == p2.risk) return p1.num < p2.num;
            return p1.risk < p2.risk;
        });
    
        // output
        for (auto &p : studentVec) {
            cout << p.num << ' ' << p.risk << '\n';
        }
        return 0;
    }
    ```

</details>

### [BOJ 1691 - 석판](https://www.acmicpc.net/problem/1691)
<details>
<summary>보기</summary> 

- 정보
    - Tier: GoldⅠ
    - Tag: DP

- 타임라인
    - Problem Open: 11/08 11:44
    - Tag Open: 11/08 11:44 (DP)
    - Solve: 11/08 12:12

- 풀이
    - $memo[i][j] =$ 사각형의 길이가 $i$, 높이가 $j$일때 최소 손실값
    - 코드 참조

- 회고
    - 태그 알고 하니 그냥 바로 풀리는 문제..
    - DP인거 모르고 했어도 바로 풀렸을까..?
 
- 코드
  - ```cpp
    #include <iostream>
    #include <vector>
    
    using namespace std;
    
    struct square { int w, h; };
    
    int W, H, N;
    vector <square> vec;
    vector <vector <int>> memo;
    
    int cutSq (int w, int h) {
        if (memo[w][h] != -1) return memo[w][h];
    
        memo[w][h] = (w != 0 && h != 0 ? w * h : 0);
        for (auto &sq : vec) {
            if (sq.w > w || sq.h > h) continue;
            memo[w][h] = min(memo[w][h], min(cutSq(w - sq.w, sq.h) + cutSq(w, h - sq.h), cutSq(sq.w, h - sq.h) + cutSq(w - sq.w, h)));
        }
        return memo[w][h];
    }
    
    int main() {
        // fastIO
        ios_base::sync_with_stdio(false);
        cin.tie(NULL); cout.tie(NULL);
        
        // init && input
        cin >> W >> H >> N;
    
        memo.resize(W + 1, vector <int> (H + 1, -1));
        vec.resize(N);
    
        for (auto &sq : vec) {
            cin >> sq.w >> sq.h;
        }
    
        // solve
        cout << cutSq(W, H);
        return 0;
    }
    ```

</details>

## 공부한 내용
- 종만북 Ch08, 09 (동적계획법, 동적계획법 테크닉)
- 컴퓨터구조 및 설계 ~Ch1.6

## 다음주 목표
- 공부한거 블로그에 적기
- 실버스트릭

## 특이사항
- 휴가가고싶어요
