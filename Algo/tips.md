# Tip



##input/output

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
			//string값에서 48을 빼줘야 숫자로 들어간다(ascii)
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

 



## REF.
[bufferreader](http://cocomo.tistory.com/507)
