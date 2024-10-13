## 기간
**24.10.07 ~ 24.10.13**

## 문제

### 14888 - 연산자 끼워넣기 
- 백트래킹
<details>
<summary> 코드 & 설명 </summary>
    <div>
    - 설설계계를 잘하자자자자악
    
``` c++
#include <iostream>

#define MAX 1000000001

using namespace std;
int N;
int arr[11];
int idx[4];
int m = MAX;
int M = -MAX;

void func(int result, int count)
{
    if(count == N)
    {
        if(m > result) m = result;
        if(M < result) M = result;
        return;
    }

    for (int i = 0; i < 4; i++)
    {
        if(idx[i] == 0) continue;
        idx[i]--;

        if(i == 0)
        {
            func(result + arr[count], count + 1);
        }
        else if(i == 1)
        {
            func(result - arr[count], count + 1);
        }
        else if(i == 2)
        {
            func(result * arr[count], count + 1);
        }
        else
        {
            func(result / arr[count], count + 1);
        }
        idx[i]++;
    }
}

int main()
{
    cin >> N;

    for (int i = 0; i < N; i++)
    {
        cin >> arr[i];
    }
    for (int i = 0; i < 4; i++)
    {
        cin >> idx[i];
    }

    func(arr[0], 1);

    cout << M << '\n' << m << '\n';
}
```
</div>
</details>

## 공부한 내용


## 이번주 목표 성공
- 알고리즘 1문제..응애
- 독일어 공부 1chapter 끝냄

## 다음주 목표
- 도파민네이션 다 읽기
- 독일어 Chapter 8 절반하기

## 특이사항
- 훈련 준비랑 일을 혼자 해서 바쁘고 피곤한...한주였슴. 운동도 못해서 상당히 쉽지 않았었다. 쉬는날인데 급한일로
- 훈련 준비로 인해 바쁠 예정..
- 근무 폭탄 맞아서 잠도 못잘 예정..
- 살려줘
