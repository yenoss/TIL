# 탐색



##컨셉
* *모든 경우의 수를 다 돌아보자* 
	* brouteForce -> 다 넣어보기,dfs
	* BFS 가 있다. 
	* 여기서는 컨셉이 그래프라고 생각하면 쉽다.
	* 모든 정점을 한번씩 방문. 
		* 정점, 간선이 존재하고,
		* 최소비용을 구하는 문제 => bfs로 풀면됨.

		
		
##BFS (너비우선탐색)
* *너어얿게* 검색하는 방법을 말한다.
* 큐를 이용하여 작업한다. 큐의 first in first out 특징을 이용한다.


```

check(방문여부)
queue.add()
while(!queue.isEmpty()){
	queue.remove()
	
	if:조건이 맞다면
		queue.add()
}

```
* 이럴수있는것이 단계별로 그래프를 방문하기 때문이다.
* 단 사이클이 있으면 안된다. 




##DFS (깊이우선탐색)
* *깊이잎게* 검색하는 방법을 말한다.
* 스택을 이용하여 작업한다. 스택에 쌓이는 방식을 이용한다 first in last out 뒤로 돌아가기 용이하다.
* 스택으로도 가능하지만 인접행렬을 이용한 재귀로 더 많이 쓰인다.

```
check(방문여부)
arr[][](인접행렬, i가 현재노드 j가 연결된 노드가 된다.연결된 정점끼리는 1 아니면 0  노드 (2,3)=> arr[2][3]=1)

check(정점체크)
for(정점의 수만큼)
if(현재노드에서 연결된값이있고(arr값이 1이고), 방문하지않았다면 
	dfs()

```

* dfs문제 풀이로 인한 코드를 보면 아래와같다.

```
import java.util.*;
import java.io.*;

class Main {


    public static int DOT;
    public static int LINE;
    public static int StartPoint;
    public static int[][] arr;
    public static boolean[] checked;
    public static void main(String[] args ) throws IOException {

        BufferedReader in = new BufferedReader(new InputStreamReader(System.in));
        BufferedWriter out = new BufferedWriter(new OutputStreamWriter(System.out));

        //정점의 갯수
        //사선의 갯수
        //시작 정점
        String[] inputt = in.readLine().split(" ");
        DOT = Integer.parseInt(inputt[0]);
        LINE = Integer.parseInt(inputt[1]);
        StartPoint = Integer.parseInt(inputt[2]);

        checked = new boolean[10000];
        arr = new int[10000][10000];

        for (int i=0; i<LINE; i++) {
            String[] line = in.readLine().split(" ");
            arr[Integer.parseInt(line[0])][Integer.parseInt(line[1])]= 1;
            arr[Integer.parseInt(line[1])][Integer.parseInt(line[0])]= 1;
        }

        for (int i=0; i<LINE; i++) {

            for (int j = 0; j < LINE; j++) {
                System.out.print(arr[i][j]);
            }
        }

        dfs(StartPoint);

    }

    public static void dfs(int searchNum) {
        checked[searchNum] = true;
        System.out.println("i==>"+(searchNum));
        //DOT에 수만큼 돌고.
        for(int i=1; i<=DOT ;i++) {

            //다시 dfs를 도는 조건은
            //체크가 안되있고, 1인상태 => 나와!!( 나가중요하다) 연결되어있는 녀석
            //searchNum이 현재의나 i가 검색해야될 녀석이 된다.
            if (arr[searchNum][i]==1 && checked[i] == false) {
                dfs(i);
            }
        }


    }
}
```





## REF.
