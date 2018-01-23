# DynamicProgramming



##컨셉
* *큰 문제를 작은 문제로 나눠서 풀자.* 
    * ex)0,1,1,2,3,5,8 피보나치 수열같은경우.
    * Fn = Fn-1+Fn-2 과 같이 표현할수있음
    * Fn을 풀기위해 n-1 n-2를 사용
    * 항시 이전의 값을 가져다 씀으로 memoization 즉 한번이상 쓸것을 저장해두는것임.
    * n 번째 피보나치수는 -> n-1 n-2를 구해야함.

* *이미 정해진값이 유지되야한다.*
	* 작은 문제들의 값은 어떠한 요소에 의해도 한번 정해지면 변경되어서는 안된다 ==> 당연! 그래야 쪼갤수있고, 해당 쪼갠것을 저장해서 쓴다는것이 말이되지!
	* 즉 정답을 구할때마다 값이 같다.
    

##피보나치수

```
//피보나치
int fibo(int n) {
//초기값일때
	if(n<=1){ return n }
	else {
		return fibo(n-1) + fibo(n-2)
	}	
}
```

* 시간 복잡도는 어떻게될까?
	* 1 2 4 ... o(2^n)
	* fibo(30) => 2^30 어마어마하게 크다. 
	* 경우의수가 1억이 넘어가면 보통 1초라고 생각하면 된다.
	* 그래서 추가적으로 경우의수를 1억아래로 맞추는게 좋다 하여 어떠한 문제의 n의 값의 범위를 꼭 잘 보아야한다.
	    
* fibonacchi는 같은 값을 계속 사용한다
	* fibo(10) -> fibo(9) + fibo(8)
	* fibo(9) -> fibo(8) + fibo(7)
	* 여기서 fibo(8)이 중복된다. 만약 이 8을 내가 메모 할수 있다면? ==> 성능 이득.
	* memoization을 하면  중복이 사라지기때문에 o(n)으로 처리할 수 있다.


```
// memoization
int fibo(int n) {
	if(n<=1){ return n }	
	else {
	//메모가 0이아니랄면 메모에 값을 넣어준다.
		if(memo[n] != 0){ return memo[n] };
		memo[n] = fibo(n-1) + fibo(n-2)
		return memo[n]
	}	
}
```

##방법
* Top Down
	* 작은 문제로 나누어 풀기 => 기존 위에서의 피보나치 
	* fibo(n-1) + fibo(n-2)
	* ===> Recurrence

* Bottom Up
	* 작은수부터 서서히 더하도록.

```
public static int[] d = new int[100];
public static int fibo(int n) {
	d[0] = 0;
	d[1] = 1;
	for (int i=2; i<=n; i++) {
		d[n] = d[n-1] + d[n-2]
	}
	return d[n];

}
```

##문제를 어떻게 푸나?
1. 문제를 구하는 것을 하나의 문장으로 표현
	* n번째의 피보나치수를 구하여라

2. 점화식을 세워본다
	* f(n) = f(n-1) + f(n-2)

3. TopDown or BottomUp
	* Recur or For loop

4. Memo할 것의 포인트를 잡아본다.
 
 
 
##++ 새로운 문제01

* 정수들이 저장된 n*n행렬에서 좌상단 -> 우상단 으로 이동할때 방문한 칸에 있는 모든 정수들의 합이 최소가 되도록하라!(단 오른쪽과 아래로만 움직일 수 있다.)

* 판단해보자
	1. 기존 값을 가져다쓸 수 있는가? ( 어떠한 점에서 이미 최소값이 존재하고 이는 변경될 수 없다.)
	2. 작은 문제로 나누어 쓸 수 있는가? ( 이전의(작은문제) 최소값 + 현재값을 더해주자.)

* 정의와 점화식을 내리자.
	* 정의 : L[i,j] = (1,1)에서 (i,j)의 최소값.
	* 점화식 : 
		* L[i,j] = { 
		* (i=0,j=0) => L[i][j],
		* (i=0) => L[0,j-1] + m[i][j](맨 윗줄 가로일때),
		* (j=0) => L[i-1,0] + m[i][j](맨 왼쪽 세로일때)

* 이를 코드로 나타낸다. 중복되는 부분이있음으로 memo를 사용하여 중복을  제거한다.


```		
    public static int mins(int i,int j) {

        if(memo[i][j] !=0) return memo[i][j];
        if( i==0 && j==0 ) {

            return memo[i][j]= arr[i][j];
        } 
        else if( i==0 ) {

            return memo[i][j] = arr[i][j] + mins(0,j-1);
        }
        else if( j==0 ) {

            return memo[i][j]= arr[i][j] + mins(i-1,0);
        }

        else{

            return memo[i][j] = Math.min(mins(i-1,j),mins(i,j-1))+arr[i][j];
        }
    }
```
		

	

 
 
 



## REF.
