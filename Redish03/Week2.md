## 기간
**24.09.30 ~ 24.10.06**

## 문제

### 1004 - 어린왕자 
- 기하
<details>
<summary> 코드 & 설명 </summary>
    <div>
    - 기하, 수학 문제 안푼지 오래되어서 도전해봤다.
    - 처음에는 시작, 끝 점이 원 안에 있는지로 판별하려 했다.
    - 그러나 한 원 안에 시작, 끝 점이 있을 가능성이 있어 조건문을 조금 수정했다.

    - 입력으로 들어오는 원의 중앙으로부터, 시작점과 끝 점 둘 다 반지름 안에 있거나 밖에 있다면 count 해주지 않는다.
    - 시작점이 원 안에 있고 끝점은 바깥에 있는 경우, 또는 그 반대의 경우 count를 증가시켜준다.
    
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


## 공부한 내용


## 다음주 목표


## 특이사항
- 새로운 통신장비가 들어와서...장비 40개 상하차 엄청나게 햇습니다..3명이서...
