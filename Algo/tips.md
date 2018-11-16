# Tip



## input/output

* input/output이 많을 경우 java에서 쓰이는 scanner와 system.out은 매우 느리다.
* inputstream과 outputstream을 사용하면 빠르게 이용할 수 있다.
* !!io 라이브러리를 꼭 추가해줘야하고, exception을 달아줘야한다.

```
import java.util.*;
import java.io.*;


public class Main {
	public static void main(String[] args) thorws IOException {
		BufferReader in = new BufferReader(new InputStreamReader(System.in));
		BufferWriter out = new BufferWriter(new OutputStreamWriter(System.out));
		
		//in 은 다음과같이 라인별로 추출이가능하다
		// asdf
		String input = in.readLine(); 
		// 1 2 3 4
		String[] inputs = in.readline().split(" ");
		
		//만약 int로 받으려면
		//1234
		//int[] a = new a[3];
		String line = in.readLine();
		for (int i=0; i<3; i++) {
			//string값에서 48을 빼줘야 숫자로 들어간다(ascii)0~9까지만.
			// java auto casting
			a[i] = line.chart(i)-48;
		}
		
		//out은 간단하다.
		//다만 뒤에 "" 처럼 스트링을 추가해줘야한다.
		out.write(input+ "");
		//!!!! 꼭 closse해줘야한다.
		out.close();
	}
}


```

## recurrence

* 재귀함수는 아래와같은 대부분 함수내부에 아래와 같은 조건이 붙는다.
	1. 종료조건( 무한대로 돌면안되니 특정 시점에서 멈추게.. fibo 에서 `if(n<=1)  return n;` 와 유사하다. )
	2. 다시 함수를 콜하는  조건( 주요 로직 특정 조건에서 다시 재귀함수를 콜하는 부분을 말한다.)
	3. + memo dp 에서 쓰일경우 memo의 값이 존재하면 있는값을 쓰는 경우가있다. if(memo[n]>0){ return memo[n]);




## REF.
[bufferreader](http://cocomo.tistory.com/507)
