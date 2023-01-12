# 문제 후기
보기에 인풋 아웃풋이 어렵지 않고, 로직을 생각하기 쉬운문제라고 생각했지만, 막상 구현하려니 원하는대로 값이 안나왔다. 그렇게 생각지 못한 난항에 어려워 하다가 답을 찾아봤는데, 이 문제는 DFS알고리즘으로 풀이하는 문제라고 했다. DFS도 완전탐색의 일종이지만, 트리 구조를 생각하지 못한다면 풀지 못할 문제라는 생각이들었다.

## 나의 풀이

1. S배열을 스택처럼 사용하여 풀이를 진행한다.
2. 현재 Node가 방문한 적이 없다면, S에 추가하고 재귀함수를 이용해 DFS를 다시 호출한다.
3. 방문한 적이 있는 Node라면, pop을 하여, 조건에 맞게 출력한다.


```python
import sys

def dfs(x):
    if len(S) == M:
        print(*S)
        return

    for i in range(x, N + 1):
        S.append(i)
        dfs(i)
        S.pop()


if __name__ == '__main__':
    N, M = map(int, sys.stdin.readline().split())
    S = []
    dfs(1)
```