## 기간
**24.09.23 ~ 24.09.29**

## 문제

### 7579 - 앱
![image.png](https://prod-files-secure.s3.us-west-2.amazonaws.com/b0078df0-8e0f-42b1-9c37-cd13fc42e65c/ea1cb2f0-52ca-4190-9190-2e90abae6388/image.png)

- DP, 배낭 문제
- 코드 & 설명
    - 배낭 문제를 조금만 응용한 문제.
    
    ``` c++
    #include <iostream>
    #include <algorithm>
    
    using namespace std;
    
    int N, M;
    long long dp[101][10001];
    int byte[101];
    int cost[101];
    
    int main()
    {
        cin >> N >> M;
        
        for(int i = 1; i <= N; i++) {
            cin >> byte[i];
        }
        for(int i = 1; i <= N; i++) {
            cin >> cost[i];
        }
        
        long long ans = 98765321987;
        for(int i = 1; i <= N; i++) {
            for(int j = 0; j <= 10001; j++) { // 모든 비용들의 합으로 바꿔도 괜찮음.
                if(j >= cost[i]){
                    dp[i][j] = max(dp[i - 1][j], dp[i - 1][j-cost[i]] + byte[i]);     
                    if(dp[i][j] >= M) {
                        ans = min(ans, (long long)j);
                    }
                }
                else dp[i][j] = dp[i - 1][j];
            }
        }
        
        cout << ans;
        
        return 0;
    }
    
    ```

## 공부한 내용
- <개발자의 글쓰기> 책 완독
- 배낭 알고리즘 다시 공부함


## 다음주 목표
- 3km 4일
- 알고리즘 5문제
- 

## 특이사항
- 
