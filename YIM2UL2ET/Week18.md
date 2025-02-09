## 기간
**25.01.20 ~ 25.01.26**

## PS 문제풀이
![Image](https://github.com/user-attachments/assets/90e749bb-50ad-4adf-8a88-5b7357384407)

사실 문제들을 풀었다기 보다는, 공부한 것들을 구현해보고 확인해 보았다는 것이 맞는 것 같다.
목요일까지는 정수론에 관한 문제를 풀었고, 그 이후로는 이분 매칭에 관하여 공부하였다.

뭔가 풀었던 것은 많지만, 문제풀이를 했다기 보다는, 공부를 했다는 느낌이 더 강했던 이번 한 주 문제풀이였다.

## [정수론(1) 내용 정리](https://yim2ul2et.github.io/posts/%EC%A0%95%EC%88%98%EB%A1%A01/)
블로그에 아래 내용들을 정리하였다.
- 합동식
- 모듈러 연산
- $O(\sqrt{N})$ 알고리즘
- 에라토스테네스의 체
- 유클리드 알고리즘

## 이분매칭 공부
이분매칭을 공부했다. 내용을 간단하게 정리하자면 아래와 같다.

#### 정의
이분 매칭은 노드가 두 그룹으로 나뉘어진 이분 그래프가 있을 때, 
각 그룹으로 나뉘어진 노드들을 인접한 간선으로 하나씩 쌍을 이루는 간선의 최대 개수를 구하는 알고리즘이다.

#### 의사 코드
```
bool dfs(node1) {
  for (node2 of connected to node1) {
    if (node2 is visited) continue    // This refers only to visits in recursive call.
    if (node2 is not matched or dfs(node of group1 matched with node2) is true) {
      matching node1 and node2
      return true
    }
  }
  return false
}

int matching() {
  answer = 0
  for (node1 of group1) {
    if (dfs(node1) is true) answer += 1
  }
  return answer
}
```

#### 참고
[SeungTaek - 이분 매칭](https://velog.io/@gmtmoney2357/%EC%9D%B4%EB%B6%84-%EB%A7%A4%EC%B9%ADBipartite-Matching)<br>
[안즈의 소소한 취미생활 - 이분 매칭](https://anz1217.tistory.com/50)

## 이번주 총평
이번 한 주는 열심히 했다고는 못하겠지만, 그래도 새로운 지식을 계속 배워서 만족하는 한 주였다.

## 다음주 목표
사실 다음주는 공부할게 딱히 정해져 있지는 않다. 
플래티넘 문제들을 훑어보니 세그트리를 슬슬 배워야겠다는 생각이 들어 PS를 하면서 세그트리를 공부해 볼 생각이다.

그 이후로는 정수론(1)을 블로그에 적었으니, 다음주는 정수론(2)을 정리할 예정이다.
- 선형 체 (Linear Seive) 테크닉
- 확장 유클리드 알고리즘
- 중국인의 나머지 정리
- 골드바흐의 추측
 
블로그에 적을 것들은 공부를 한지 좀 된 상태라 복습하면서 천천히 적어볼 예정이다.

## 특이사항
- 01/23 당직, 01/24 오프
