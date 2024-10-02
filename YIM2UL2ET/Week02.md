## 기간
**24.09.30 ~ 24.10.06**

## 풀었던 문제

### [BOJ 19621 - 회의실 배정 2](https://www.acmicpc.net/problem/19621)
<details>
<summary>보기</summary> 

- 정보
    - Tier: Silver Ⅱ
    - Tag: dynamic_programming, bruteforce

- 타임라인
    - Problem Open: 09/30 10:30
    - Tag Open: 09/30 10:30
    - Solve: 09/30 11:30

- 풀이
    - DP 연습하려고 DP로 풀이
    - K번째 회의가 K-1번째 회의와 K+1번째 회의랑만 겹친다는 것을 이용한다.
    - memo[i]: i번째 회의까지 보았을 때 제일 많이 들어가는 인원 수의 총합
    - memo[i] = max(memo[i - 1], memo[i - 2] + meetingPeople[i]);

- 회고
    - 문제와 조건을 잘 읽자.. (임의의 회의 K(1≤ K ≤ N)는 회의 K − 1과 회의 K + 1과는 회의 시간이 겹치고 다른 회의들과는 회의 시간이 겹치지 않는다. <- 이 조건 안읽어서 40분동안 삽질 겁나 하다가 깨달음)
    - 근데 겹치는 조건이 저렇게 있으면 시작시간, 끝나는 시간 왜 적어놓은거임..? 훼이크인가?? (실제로 풀이에 아무 쓸모가 없음;;)

</details>

### [BOJ 21992 - 학부 연구생 민상](https://www.acmicpc.net/problem/21922)
<details>
<summary>보기</summary> 

- 정보
    - Tier: Gold Ⅴ
    - Tag: implementation

- 타임라인
    - Problem Open: 10/01 18:10
    - Tag Open: --/-- --:--
    - Solve: 10/01 19:10

- 풀이
    - 단순한 구현문제
    - 설계시 이상 없는지 체크 확실하게 하면 간단하게 풀 수 있음.

- 회고
    - enum 공부
    - 너무 피곤하다

</details>

### [BOJ 21992 - 학부 연구생 민상](https://www.acmicpc.net/problem/21922)
<details>
<summary>보기</summary> 

- 정보
    - Tier: Platinum Ⅴ
    - Tag: greedy

- 타임라인
    - Problem Open: 10/01 22:00
    - Tag Open: --/-- --:--
    - Solve: 10/02 12:13

- 풀이
    - ans[0] = -2, $1 \le i \le N$ 로 정의
    - ans[i] = if (남은 수가 $k, k+1$ 형태의 두가지 종류의 수 밖에 없을 때) : $k + 1$을 넣음 / else : ans[i - 1] + 1 이 아닌 최솟값을 넣음.

- 회고
    - 컴퓨터에서 손 놓고 생각만 오래했던 문제 (실제론 3시간 정도만에 풀이가 생각남)

</details>

## 참가한 오픈 콘테스트

### []()
<details>
<summary>보기</summary>

| 문제 | A | B | C | D | E | F | G | H | I | J | K |
|---|---|---|---|---|---|---|---|---|---|---|---|
|결과| - | - | - | - | - | - | - | - | - | - | - | - |

- ?번:
    - 문제 정보와 풀이 및 회고 

- 회고
    - 노트

</details>

## 공부한 내용

## 다음주 목표
- 1Day 1Solve

## 특이사항
- 연등 휴일 연등 휴일 연등 휴일 휴일
