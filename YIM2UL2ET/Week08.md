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

## 공부한 내용
- 종만북 Ch08, 09 (동적계획법, 동적계획법 테크닉)
- 컴퓨터구조 및 설계 ~Ch1.6

## 다음주 목표
- 공부한거 블로그에 적기
- 실버스트릭

## 특이사항
- 휴가가고싶어요
