---
layout: post
title: "[백준2749] 피보나치 수와 피사노 주기, Fibonacci numbers and Pisano period"
date: 2018-07-22
excerpt: "피사노 주기를 이용하여 N번째 피보나치 수를 1,000,000으로 나눈 나머지 구하기"
tag:
- Baekjoon
- Fibonacci
category: [ 백준 문제풀이 ]
feature: https://png93.github.io/assets/img/title/bj_title.jpg
comments: true
---

_백준 2749번 문제를 풀면서 공부한 내용입니다._
{: .notice}

<a href = "https://www.acmicpc.net/problem/2749"><img src = "https://png93.github.io/assets/img/title/baekjoon.PNG"></a>

<br/>

## 피보나치 수
피보나치 수는 앞에 있는 두 수의 합이 현재의 수가 되는 규칙을 가지는 수 이다.

| 0 | 1 | 2 | 3 | 4 | 5 | 6 | 7  | 8  | 9  | 10 |...|
|:---|:--:|:--:|:--:|:--:|:--:|:--:|:--:|:--:|:--:|:--:|---:|
| 0 | 1 | 1 | 2 | 3 | 5 | 8 | 13 | 21 | 34 | 55 |...|
{: rules="groups"}

<br/>

## 피사노 주기
2749번 문제의 출력 조건은 "n번째 피보나치 수를 1,000,000으로 나눈 나머지를 출력한다." 인데, 피보나치 수를 나눈 나머지들은 반드시 주기를 가지며, 이를 피사노 주기라고 한다는 사실을 알게 되었다.[^1] [^2]

[^1]: <http://taekho-nology.tistory.com/75>
[^2]: <http://ksj14.tistory.com/entry/%EC%88%98%ED%95%99%ED%94%BC%EB%B3%B4%EB%82%98%EC%B9%98-%ED%94%BC%EB%B3%B4%EB%82%98%EC%B9%98-%EC%88%98>

위 내용을 참고해 2749번 문제를 풀면서 사용한 정의는 다음과 같다.

<hr>
**피보나치 수를 나눌 수를 K라고 할 때, \\( k = 10^{n} \\) 이면, 피사노 주기는 \\( 15*10^{n-1} \\)이다.**
<hr>


문제에서 \\( 10^{6} \\) 으로 나눈 나머지를 구하라고 했으므로 주기는 **1,500,000** 이 된다는 것을 알 수 있다.

따라서 입력의 최대값이 1,000,000,000,000,000,000 이더라도, 최대 1,500,000번째 까지만 \\( 10^{6} \\)로 나눈 나머지 값들을 알면 그 이후의 위치는 따로 계산할 필요가 없게 된다.

<br/>

\< 코드 작성 과정 \>

*길이가 p인 long 타입 배열에 피보나치 수를 \(10^{6}\)으로 나눈 나머지 값을 저장한다.
입력 n이 주기 p 보다 작은 값이라면 n번째 까지 구한후 반복문을 빠져나온다.
만약 n이 p보다 큰 값이라면 "n mod p" 번째 위치를 출력한다.*

~~~java

import java.util.Scanner;

public class Q2749_FibonacciMatrix {

	public static void main(String[] args) {
		Scanner sc = new Scanner(System.in);
		long n = sc.nextLong();
		sc.close();

		int p = 1500000; // 피보나치 수열을 10^6로 나누었을 때 주기

		long[] modArr = new long[p];

		modArr[0] = 0;
		modArr[1] = 1;

		for (int i = 2; i < p; i++) {
			if (i > n)
				break;

			modArr[i] = modArr[i - 1] + modArr[i - 2];
			modArr[i] %= (long) Math.pow(10, 6);
		}

		if(n >= p) {
			n %= p;
		}

		System.out.println(modArr[(int)n]);

	}

}
~~~
