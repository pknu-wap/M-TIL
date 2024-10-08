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

## 특이사항
- 10/08 ~ 10/11 휴가
