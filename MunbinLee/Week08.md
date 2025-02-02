## 기간
**25.01.27 ~ 25.02.02**

---
# [9. Palindrome Number (Easy)](https://leetcode.com/problems/palindrome-number)

정수 `x`가 주어졌을 때, x가 회문인지 아닌지 그 여부를 반환하세요.  
추가 질문: 정수를 문자열로 변환하지 않고 해결할 수 있나요?

---
입력: `x` = 121  
출력: true  
설명: 121은 거꾸로 읽어도 121이므로 참 반환.

---
재귀로 푸는 게 깔끔해보여서 재귀 함수로 구현했다.  
isPalindrome(x)의 결과는 isPalindrome(x[1:-1])에 달려있기 때문이다.

```cpp
class Solution {
public:
    bool isPalindrome(int x, int size = -1) {
        // log10(0 이하)는 에러가 발생하기 때문에 미리 처리
        if (x == 0) {
            return true;
        }
        if (x < 0) {
            return false;
        }

        // 함수 최초 실행시 자릿수를 로그로 계산
        if (size == -1) {
            size = log10(x) + 1;
        }

        // 자릿수가 1 이하면 무조건 회문
        if (size <= 1) {
            return true;
        }

        int first = x / pow(10, size - 1);
        int last = x % 10;

        if (first != last) {
            return false;
        }

        // 숫자의 맨 앞과 맨 뒤 제거
        return isPalindrome(x % (int)pow(10, size - 1) / 10, size - 2);
    }
};
```

나머지는 사지방 연등시간이 끝나서 다음 시간에...