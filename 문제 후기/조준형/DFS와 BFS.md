# 백준 1206번

### 그래프 순회 개념을 처음 접했다. stack, queue 개념을 활용해 해당 문제를 해결할 수 있다고 한다.
### 알고리즘 문제에서 해당 개념은 필수적으로 수반해야 한다고 하는데, 개념 정리해서 벨로그에 쓰자!


```
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.LinkedList;
import java.util.Queue;
import java.util.StringTokenizer;

public class Main {

	static StringBuilder sb = new StringBuilder();
	static boolean[] check;
	static int[][] arr;
	
	static int node, line, start;
	
	static Queue<Integer> q = new LinkedList<>();

	public static void main(String[] args) throws IOException {
		
		BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
		
		StringTokenizer st = new StringTokenizer(br.readLine());
		node = Integer.parseInt(st.nextToken());
		line = Integer.parseInt(st.nextToken());
		start= Integer.parseInt(st.nextToken());
		
		arr = new int[node+1][node+1];
		check = new boolean[node+1];
		
		for(int i = 0 ; i < line ; i ++) {
			StringTokenizer str = new StringTokenizer(br.readLine());
			
			int a = Integer.parseInt(str.nextToken());
			int b = Integer.parseInt(str.nextToken());
			
			arr[a][b] = arr[b][a] =  1;	
		}
        
        dfs(start);
        sb.append("\n");
        check = new boolean[node+1];

        bfs(start);

        System.out.println(sb);
		
		}
    
	public static void dfs(int start) {
		
		check[start] = true;
		sb.append(start + " ");
		
		for(int i = 0 ; i <= node ; i++) {
			if(arr[start][i] == 1 && !check[i]) dfs(i);
		}
		
	}
	
	public static void bfs(int start) {
		q.add(start);
		check[start] = true;
		
		while(!q.isEmpty()) {
			
			start = q.poll();
			sb.append(start + " ");
			
			for(int i = 1 ; i <= node ; i++) {
				if(arr[start][i] == 1 && !check[i]) {
					q.add(i);
					check[i] = true;
				}
			}
		}
		
	}

}
```