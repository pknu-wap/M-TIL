## 기간
**24.01.27 ~ 25.02.02**

## PS 문제풀이
// 사진

이번주도 1일 1솔을 실천하였다.
절반정도는 세그먼트트리 구현 문제, 절반은 수학 문제를 풀이하였다.

이번주 문제를 풀면서 피보나치 수열의 성질이 의외로 많아 알아두면 좋을 것 같다는 생각이 들었다.<br>
**[피보나치 수열의 성질 - 나무위키](https://namu.wiki/w/%ED%94%BC%EB%B3%B4%EB%82%98%EC%B9%98%20%EC%88%98%EC%97%B4#s-5)**

나중에 따로 정리할 예정이다.

## 세그먼트 트리 공부
세그먼트 트리를 간단히 공부했다. 따로 정리하고 싶으나, 세그트리는 응용이 워낙 많아 나중에 함께 정리하려고 한다.
워낙 좋은 글들이 많아 아래 글을 참고하면 좋을 것 같다.

#### 정의
세그먼트 트리란 동적인 어떤 구간의 질의에 대하여 효율적으로 처리가 가능한 자료구조이다.
트리의 형식으로 되어 있으며, 각 노드에 대하여 [l, r]의 질의에 대하여 응답한다.

#### 코드
아래 코드는 누적 합에 대한 세그먼트 트리 구현이다.

```cpp
// acmicpc.net/problem/2042
#include <iostream>
#include <vector>

using namespace std;

typedef long long ll;

vector<ll> segTree;

ll sum(ll n, ll s, ll e, ll l, ll r) {
  if (e < l || s > r) return 0;
  if (l <= s && e <= r) return segTree[n];

  ll m = (s + e) / 2;
  return sum(n * 2, s, m, l, r) + sum(n * 2 + 1, m + 1, e, l, r);
}

void update(ll n, ll s, ll e, ll i, ll v) {
  if (i < s || i > e) return;

  if (s == e) {
    segTree[n] = v;
    return;
  }

  ll m = (s + e) / 2;
  update(n * 2, s, m, i, v);
  update(n * 2 + 1, m + 1, e, i, v);

  segTree[n] = segTree[n * 2] + segTree[n * 2 + 1];
}

int main() {
  ios_base::sync_with_stdio(false);
  cin.tie(NULL);
  cout.tie(NULL);

  int N, M, K;
  cin >> N >> M >> K;

  ll v;
  segTree.resize(N * 4);
  for (int i = 1; i <= N; i++) {
    cin >> v;
    update(1, 1, N, i, v);
  }

  ll c, p, q;
  for (int i = 0; i < M + K; i++) {
    cin >> c >> p >> q;
    if (c == 1) {
      update(1, 1, N, p, q);
    } else {
      cout << sum(1, 1, N, p, q) << '\n';
    }
  }

  return 0;
}
```

#### 참고
[안즈의 소소한 취미생활 - 세그먼트 트리](https://anz1217.tistory.com/33)

## 이번주 총평
이번주는 사실.. 휴일이 많이 겹쳐있으니 공부를 하려고 해도 잘 잡히지 않았다.. 평일 공부량에도 못미치는 것 같아 아쉬운 한주이다.
그래도 그동안 못봤던 애니메이션 등을 많이 봐서 좋았다.

## 다음주 목표
다음주는 휴가라 편히 쉬고 올 예정이다. (어차피 공부 안될 것을 알고있기에..)
CLRS로 최대 유량 그래프에 대해서 공부중이라 시간이 남으면 공부할 예정이다.

## 특이사항
- 01/29 당직
- 02/01 상병 조기진급
