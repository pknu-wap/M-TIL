## 기간
**24.09.30 ~ 24.10.06**

## 문제

### 1004 - 어린왕자 
- 기하
<details>
<summary> 코드 & 설명 </summary>
    <div>
    - 기하, 수학 문제 안푼지 오래되어서 도전해봤다. <br>
    - 처음에는 시작, 끝 점이 원 안에 있는지로 판별하려 했다. <br>
    - 그러나 한 원 안에 시작, 끝 점이 있을 가능성이 있어 조건문을 조금 수정했다.<br><br>
    - 입력으로 들어오는 원의 중앙으로부터, 시작점과 끝 점 둘 다 반지름 안에 있거나 밖에 있다면 count 해주지 않는다.<br>
    - 시작점이 원 안에 있고 끝점은 바깥에 있는 경우, 또는 그 반대의 경우 count를 증가시켜준다.<br>
    
``` c++
#include <iostream>
#include <cmath>

using namespace std;

int T, N, start_x, start_y, end_x, end_y;

bool checkInside(int c_x, int c_y, int r) {
    double start_dist = pow(start_x - c_x, 2) + pow(start_y - c_y, 2);
    double end_dist = pow(end_x - c_x, 2) + pow(end_y - c_y, 2);
    double sq_r = pow(r, 2);
    
    if(start_dist > sq_r && end_dist > sq_r) return false;
    else if(start_dist < sq_r && end_dist < sq_r) return false;
    
    return true;
}

int main()
{
    ios_base::sync_with_stdio(0);
    cin.tie(nullptr);
    cout.tie(nullptr);
  	cin >> T;
  	while(T--) {
	      int cnt = 0;
	    	cin >> start_x >> start_y >> end_x >> end_y;
		    cin >> N;

		    int c_x, c_y, radius;

		    for(int i = 0; i < N; i++) {
			      cin >> c_x >> c_y >> radius;
			      if(checkInside(c_x, c_y, radius)) cnt++;
		    }
		  cout << cnt << '\n';
	  }

	  return 0;
}
```
</div>
</details>

### 22858 - 원상 복구(small)
- 구현
<details>
<summary> 코드 & 설명 </summary>
    <div>
    - 구현 문제
    
``` c++
#include <iostream>
#include <vector>

using namespace std;

int main()
{
    int N, K;
    cin >> N >> K;
    
    vector<int> D(N);
    vector<int> S(N);
    vector<int> tmp(N);
    
    for(int i = 0; i < N; i++) {
        cin >> S[i];
    }
    for(int i = 0; i < N; i++) {
        cin >> D[i];
    }
    
    while(K--) {
        for(int i = 0; i < N; i++) {
            int prev_order = D[i] - 1;
            tmp[prev_order] = S[i];
        }
        for(int i = 0; i < N; i++) {
            S[i] = tmp[i];
        }
    }
    
    for(int i = 0; i < N; i++) {
        cout << tmp[i] << " ";
    }

    return 0;
}

// D_i 번째 카드를 i 번째로 가져오는 작업.
```
</div>
</details>


### 16236 - 아기상어
- BFS
- 시뮬레이션

<details>
<summary> 코드 & 설명 </summary>
    <div>
    - 상어가 출발해서 물고기 하나를 먹으면, 그 상태에서 다시 BFS를 돌려준다.	<br>
    - N ≤ 20이라 여러번 BFS를 실행하는게 가능하다.<br>
    - 거의다 풀었는데, 마지막에서 어디에서 막혔는지 모르겠어서 답안지랑 비교를 했는데, bool형으로 먹었는지 안먹었는지 확인하는거랑, 멈추는 조건, 그리고 나는 visited를 매번 초기화했는데 답안지에서는 while 안에 선언해서 좀 더 실행횟수를 아꼈다. 물론 이런 부분만이 있는것은 아닐 것이다. <br>
    
``` c++
#include <iostream>
#include <queue>
 
using namespace std;
int n;
int map[22][22];
int dx[] = {0, -1, 1, 0}; 
int dy[] = {-1, 0, 0, 1};
int bx, by;
int result = 0; 
int count = 0; 
int sz = 2; 
bool stop = false; 
bool eat = false;
void bfs(int a, int b, bool visit[][22], int shSize){
    queue<pair<pair<int, int>, int>> q;
    q.push(make_pair(make_pair(a, b), 0));
    visit[b][a] = true;
    int temp;
    while(!q.empty()){
        int x = q.front().first.first; 
        int y = q.front().first.second; 
        int cnt = q.front().second;
     
        if(map[y][x] > 0 && map[y][x] <shSize && temp == cnt){
            if((by > y) || (by == y && bx > x)){
                by = y; 
                bx = x;
                continue;
            }
        }
        q.pop();
        for (int i = 0; i < 4; i++){
            int nx = x + dx[i]; 
            int ny = y + dy[i];
 
            if(nx>=0 && nx <n && ny>=0 && ny <n && !visit[ny][nx]){
                if(map[ny][nx] <= shSize){
                    if(map[ny][nx] > 0 && map[ny][nx] < shSize && !eat){ 
                        eat = true; 
                        bx = nx;
                        by = ny;
                        temp = cnt + 1; 
                        result += temp;
                    }else{ 
                        q.push(make_pair(make_pair(nx, ny), cnt + 1));
                        visit[ny][nx] = true;  
                    }                      
                }
            }
        }
    }
}
int main(){
    cin >> n;
    for (int i = 0; i < n; i++){
        for (int j = 0; j < n;j++){
            cin >> map[i][j];
            if(map[i][j] == 9){
                by = i; 
                bx = j;
                map[i][j] = 0;
            }
        }
    }
 
    while(!stop){
        bool visit[22][22] = {0};
        bfs(bx, by, visit, sz); 
        if(eat){
            eat = false; 
            count += 1;
            map[by][bx] = 0;
            if(count == sz){
                sz += 1;
                count = 0; 
            }
        }else{ 
            stop = true; 
        }
    }
    cout << result << '\n';
    return 0;
}

```
</div>
</details>

## 공부한 내용
[<프롬프트 엔지니어링>-반병현](https://blog.naver.com/pluto0303/223603245206) <br>
[<AI 사피엔스>](https://blog.naver.com/pluto0303/223608684266)

## 이번주 목표 성공
- 알고리즘 3/5 (실패)
- <프롬프트 엔지니어링> 독서록 작성완료
- 3km 뜀걸음 3회 (15:07) 및 풋살, 축구 대체,,성공,,^^~
- 독일어 공부 1chapter 끝냄

## 다음주 목표
- <도파민네이션> 다 읽기
- 알고리즘 5문제
- 독일어 0.5chapter 하기

## 특이사항
- 10/11 전투휴무
