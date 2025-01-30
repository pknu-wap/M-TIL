## 기간
**25.01.20 ~ 25.01.26**

---

[프로그래머스 코드 챌린지](https://career.programmers.co.kr/competitions/4079) 에 신청하였다.

오랜만에 알고리즘 문제를 푸는 것이라 어떤 문제들을 풀까 고민하다  
외부 IDE가 필요없는 저지 사이트 중 가장 유명한 리트코드에서 풀기로 했다.  
일단은 Easy와 Medium 문제들만 풀면서 재활훈련을...

---
# [1. Two Sum (Easy)](https://leetcode.com/problems/two-sum)

정수 배열 `nums`와 정수 `target`이 주어질 때, 더해서 `target`이 되는 `nums`의 두  정수의 인덱스를 반환하세요.

각 입력에는 하나의 해답이 존재하며, 동일한 요소를 두 번 사용할 수 없습니다.

답은 어떤 순서로든 반환할 수 있습니다.

---
입력: `nums` = [2,7,11,15], `target` = 9  
출력: [0,1]  
설명: nums[0] + nums[1] == target 이므로, [0, 1] 반환.

---
nums.length <= 10^4 이므로, $O(N^2)$ 풀이가 가능.  
for문을 2번 돌려서 모든 경우의 수를 탐색하면 된다.

---
이진탐색을 활용하여 $O(NlogN)$ 풀이도 가능.  
정렬 한번 때린 후, 각 정수에 대하여 보수를 (`target`이 9이고 현재 정수가 2라면 7을) 이진탐색으로 찾는다.

---
각 정수와 그 인덱스를 map으로 저장하면 $O(N)$ 으로 풀 수 있다.  
위 두 풀이와는 다르게 메모리가 $O(N)$이다.

```cpp
class Solution {
public:
    vector<int> twoSum(vector<int>& nums, int target) {
        // 정수의 인덱스 저장용
        unordered_map<int, int> positions;

        for (int position = 0; position < nums.size(); position++) {
            // 보수 (원하는 값))
            int complement = target - nums[position];

            // 보수가 저장되어 있다면 그대로 답을 반환한다.
            if (positions.contains(complement)) {
                return {positions[complement], position};
            }

            // map에 정수의 인덱스를 저장한다.
            positions[nums[position]] = position;
        }

        return {};
    }
};
```

---
# [3. Longest Substring Without Repeating Characters (Medium)](https://leetcode.com/problems/longest-substring-without-repeating-characters)

주어진 문자열 `s`에서 반복되는 문자가 없는 가장 긴 부분 문자열의 길이를 구하세요.

---
**예제**  
입력: s = "abcabcbb"  
출력: 3  
설명: 가장 긴 부분 문자열은 "abc"이므로, 3 반환.

---
투 포인터와 슬라이딩 윈도우를 사용하여 $O(N)$으로 풀 수 있다.  
윈도우는 반복되는 문자가 없는 상태를 유지한 상태로 움직인다.
```cpp
class Solution {
public:
    int lengthOfLongestSubstring(string s) {
        // 중복체크용, 윈도우에 포함된 문자들
        unordered_set<char> usedCharacters;

        // 윈도우는 닫힌 구간 [slow, fast]
        int slow = 0;
        int fast = 0;
        int maxLength = 0;

        while (fast < s.size()) {
            // 중복이 발생할 경우, 중복이 해소될 때까지 slow 포인터를 민다.
            while (usedCharacters.contains(s[fast])) {
                usedCharacters.erase(s[slow]);
                slow++;
            }

            usedCharacters.emplace(s[fast]);
            maxLength = max(maxLength, fast - slow + 1);
            fast++;
        }

        return maxLength;
    }
};
```

---
# [4. Median of Two Sorted Arrays (Hard)](https://leetcode.com/problems/median-of-two-sorted-arrays/)

두 정렬된 배열 `nums1`과 `nums2`가 주어졌을 때, 두 배열의 중앙값을 반환하세요.

시간 복잡도는 $O(log(m+n))$이어야 합니다.

---
**예제**  
입력: nums1 = [1,3], nums2 = [2]  
출력: 2.00000  
설명: 합친 배열 = [1,2,3], 중앙값은 2.

---
$O(log(M+N))$으로 풀라는데 너무 어렵다.  
1번부터 순서대로 풀다가 이 문제에서 Hard의 벽을 느끼고 Medium까지만 풀게됐다.  

일단 두 배열을 머지소트에서 배열 합치듯이 합치면 $O(M+N)$ 인데 이걸로는 택도 없다.

---
일단 각 배열이 정렬되어 있고 시간 복잡도가 로그니까 이진탐색을 써야겠지...?  

처음에 상상했던 건 nums1에서 이진탐색을 돌려 각 값에 대하여 nums2가 어떤 지점에 있는지 이진탐색으로 파악하는 것이었다.  

근데 이렇게 풀면 시간복잡도가 로그가 아니라 로그제곱이 된다.  

그러면, 특정 배열에 대하여 이진탐색을 돌리지 말고 숫자에 대하여 이진탐색을 돌리면 어떨까?  

이러면 시간복잡도가 $O(log(M+N))$에서 $O(log(max - min))$ 으로 바뀌는데

M+N의 최댓값은 2000이고 max-min의 최댓값은 2000000이다.  

인정협회에서 인정 안 해줄 것 같다...  
