---
layout: post
title: "[백준1003] 피보나치 함수"
date: 2018-07-22
excerpt: "피보나치 함수의 호출 횟수 구하기"
tag: [Baekjoon, Fibonacci]
category: [ 백준 문제풀이 ]
feature: https://png93.github.io/assets/img/title/bj_title.jpg
comments: true
---

_백준 1003번 문제를 푼 과정입니다._
{: .notice}

<a href = "https://www.acmicpc.net/problem/1003"><img src = "https://png93.github.io/assets/img/title/baekjoon.PNG"></a>

<br/>

입력 N이 주어졌을 때, 다음의 함수가 fibonacci(0), fibonacci(1)을 각각 몇번 씩 호출하는지 구하는 문제이다.

~~~c++
int fibonacci(int n) {
    if (n == 0) {
        printf("0");
        return 0;
    } else if (n == 1) {
        printf("1");
        return 1;
    } else {
        return fibonacci(n‐1) + fibonacci(n‐2);
    }
}
~~~

<br/>

**fibonacci(n) : {'0의 호출 횟수', '1의 호출 횟수'}**
를 적어 내려가 보았다.
- - -
fibonacci(0) : {1, 0} <br/>
fibonacci(1) : {0, 1} <br/>
fibonacci(2) : {1, 1} <br/>
fibonacci(3) : {1, 2} <br/>
fibonacci(4) : {2, 3} <br/>
fibonacci(5) : {3, 5} <br/>
fibonacci(6) : {5, 8} <br/>
...
- - -

위 과정에서 내가 찾은 규칙은 다음과 같다.

>**fibonacci(n) : {x, y} 일때 fibonacci(n+1) : {y, x+y} 이다. (단, n > 0)**


<br/>

_\< Q1003_FibonacciFunction.java \>_
~~~java
import java.util.ArrayList;
import java.util.List;
import java.util.Scanner;

public class Q1003_FibonacciFunction {

	public static void main(String[] args) {
		Scanner sc = new Scanner(System.in);
		int t = sc.nextInt();

		List<int[]> list = new ArrayList<int[]>();
		int[] count = { 1, 0 };
		list.add(count);

		for (int test_case = 0; test_case < t; test_case++) {

			int n = sc.nextInt();

			if (list.size() - 1 < n) {
				for (int i = list.size() - 1; i < n; i++) {
					int[] next = { list.get(i)[1], list.get(i)[0] + list.get(i)[1] };
					list.add(next);
				}
			}

			System.out.println(list.get(n)[0] + " " + list.get(n)[1]);

		}
		sc.close();
	}

}
~~~
