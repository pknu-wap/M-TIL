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

### [BOJ 1071 - 소트](https://www.acmicpc.net/problem/1071)
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

### [STPC 2024 Autumn Open Contest](https://www.acmicpc.net/contest/view/1361)
<details>
<summary>보기</summary>

| 문제 | A | B | C | D | E | F | G | H | I | J |
|---|---|---|---|---|---|---|---|---|---|---|
|결과| AC | AC | AC | AC | AC | - | WA | - | - | - | - |

- A번: 바코드 닉네임
    - string 입력받아서 l을 L로, I를 i로 바꿔서 출력하는 문제
 
- B번: Max-Queen
    - 체스판에 여러개의 퀸을 두었을 때, 서로 잡을 수 있는 경우의 수 / 2
    - n * m 체스판 크기가 주어지므로, 정답은 ((꼭짓점 퀸의 수 * 3) + (테두리 퀸의 수 * 5) + (나머지 퀸의 수 * 8)) / 2
 
- C번: MEX vs OR
    - $n = \lbrace m | m \in \mathbb{Z}, l \le m \le r \rbrace$와 $x$를 OR연산 시켜서 나온 값중 음이 아닌 정수 중 가장 작은 값을 출력하는 문제
    - 비트연산을 활용한 구현

- D번: $x$와 $x+1$의 차이
     - $x$를 입력받아 임의의 $n \in \mathbb{Z}^+$에 대하여 $x \div n \neq (x + 1) \div n$인 n을 찾는 문제
     - $x+1$의 약수를 찾으면 된다.
 
- E번: ABB to BA (Easy)
     - string을 입력받아, 문자열에 "ABB"가 있으면 "BA"로 바꾸어, "ABB"가 없을 때 까지 반복한 다음 출력하는 문제
     - 구현으로 처리 (F번이 Hard였는데 제한이 너무 크게 늘어 해결하지 못함)
 
- G번: 수열과 개구리
     - 기다리는 시간 $a_i$와 움직이는 거리 $b_i$ ($i \in \mathbb{Z}_{n-1}$)를 입력받은 후, 수열 바깥으로 가는 최소 시간 구하기
     - DP인듯 한데.. 왜 안되는건지 모르겠음. 내가 모르는 잘못된 설계가 있나봄. 1시간반 정도 날림
 
- 회고:
     - D번 풀이시 자료형 확인 (int형을 써야할 것과 long long형을 써야할 것 확인)
     - 안되면 우선 놓고, 다른 문제부터 일단 읽어보기 (G번같은 경우, 효율적인 시간 사용)

</details>

## 공부한 내용

## 다음주 목표
- 종만북 읽기
- 골랜디 시작
- 다음주 휴가때 푹 쉬고 오기

## 특이사항
- 연등 휴일 연등 휴일 연등 휴일 휴일
