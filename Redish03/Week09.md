## 기간
**24.11.18 ~ 24.11.24**

## 문제

### 18110 - solved.ac
- 수학
<details>
<summary> 코드 & 설명 </summary>
    <div>
    - 평균구하는 문제.
    - floor 함수로 반올림 만들기를 알았다.
    - floor은 내림 함수인데, 함수의 인자로 들어가는 수에 0.5를 더해서 넣으면 반올림이 가능하다.
    
``` c++
#include <iostream>
#include <vector>
#include <algorithm>
#include <cmath>

using namespace std;

int main()
{
    int N; cin >> N;
    vector<int> v;
    if(N == 0) {
        cout << 0;
        return 0;
    }
    
    for(int i = 0; i < N; i++) {
        int a;
        cin >> a;
        v.push_back(a);
    }
    
    sort(v.begin(), v.end());
    
    int cut_person = floor((float)N * 0.15 + 0.5);
    int avg = 0;
    
    for(int i = 0; i < N - cut_person; i++) 
    {
        if(i < cut_person) {
            continue;
        }
        
        avg += v[i];
    }
    
    avg = floor((float)avg / (N - 2 * cut_person) + 0.5);
    cout << avg;
    
    return 0;
}
```
</div>
</details>

## 이번주 목표
- <오직 두사람> 절반 읽기
- 알고리즘 5문제
- 

## 공부한 내용


## 다음주 목표
- 3km 뜀걸음 4일
- 알고리즘 5문제
- <오직 두사람> 절반 읽기

## 특이사항
- 금요일 부대 개방 행사
- 토요일 부모님 면회
- 휴가 갔다왔읍니다..
