# 문제 후기
문제를 해석하고 나서 로직을 생각하기까지 시간이 오래 걸렸다. 그리고, 스스로 생각해낸 로직을 구현하는데, 망설임이 있었다. 완전탐색, 백트래킹을 이해했다 생각했는데, 관련문제를 푸는데에는 아직 부족함이 많다.

## 나의 풀이

1. 퀸은 대각선과 직선방향으로 이동이 가능하다.
2. 한 열, 한 행의 두개의 퀸이 존재할 수 없다.
3. 퀸끼리는 대각선 방향에 위치할 수 없다.
4. 따라서, 퀸을 놓는 경우의 수 를 확인하여 위의 조건에 걸리지 않는 경우의 수를 체크한다.

```java
import java.util.Scanner;

public class Main {
    static int N, ans;
    static int[] col;

    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);

        N = sc.nextInt();
        col = new int[N+1];
        rec_func(1);
        System.out.println(ans);
    }

    static void rec_func(int row) {
        if (row == N + 1) {
            ans++;
        } else {
            for (int c = 1; c <= N; c++) {
                boolean possible = true;
                for (int i = 1; i <= row - 1; i++) {
                    if(attackable(row, c, i, col[i])) {
                        possible = false;
                        break;
                    }
                }
                if(possible) {
                    //위치에 값써주기
                    col[row] = c;
                    rec_func(row + 1);
                    col[row] = 0;
                }
            }
        }
    }
    static boolean attackable(int r1, int c1, int r2, int c2){
        if (c1 == c2) return true;           // 같은 행
        if (r1 + c1 == r2 + c2) return true; // 오른쪽 대각선
        if (r1 - c1 == r2 - c2) return true; // 왼쪽 대각선

        return false;
    }
}
```

## 파이썬은 시간초과

1. 같은 로직을 적용했으나 시간초과로 실패했다.
2. 8월자 풀이를 복붙해보았으나 역시 시간초과가 났다. 문제에 문제가 있는걸까 하는 의문이들었다.
3. 진형님께 물어보니 제출할때, `pypy3`으로 하면 시간초과가 안날수도 있다고 했다. `pypy3`로 제출하니 성공....!

```python
import sys

def check(here):
    for i in range(here):
        if col[here] == col[i]: return False
        if abs(col[here] - col[i]) == here - i: return False
    return True


def solve(here):
    if here == N: return 1
    ret = 0
    for i in range(N):
        col[here] = i
        if check(here):
            ret += solve(here + 1)
        col[here] = -1
    return ret


if __name__ == '__main__':
    N = int(sys.stdin.readline())
    col = [-1 for i in range(N * 2)]
    print(solve(0))
```