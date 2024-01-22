---
layout: post
title: Where to declare Java Variables?
---

Recently I went to Java Meetup. And it was all about Garbage Collector. So I learned lot more about Garbage Collectors. So Dr. Daya's suggestions was not to declare variable in higher scopes unless we really know what we do. For a example, don't declare class level variables if we are only using it inside on method. Then I was thinking about doing some tests on variable declarations. I used following code:

```java
public class Variable01 {

	public static void main(String[] args) {
		long startTime = System.nanoTime();
		Method();
		long endTime = System.nanoTime();

		long duration = endTime - startTime;

		System.out.println("Method runtime : " + duration + " ms");
	}

	public static void Method() {
		for (int i = 0; i < 100000; i++) {
			String str;
			// Some Logic
			str = Integer.toString(i);
			System.out.println(str);
		}
	}
}
```

Then I used following code to do see the difference. Following code is declaring a variable in a higher scope(which is bad according to Dr.Daya).

```java
public class Variable02 {

	public static void main(String[] args) {
		long startTime = System.nanoTime();
		Method();
		long endTime = System.nanoTime();

		long duration = endTime - startTime;

		System.out.println("Method runtime : " + duration + " ms");
	}

	public static void Method() {			
		String str;
		for (int i = 0; i < 100000; i++) {
			// Some Logic
			str = Integer.toString(i);
			System.out.println(str);
		}
	}

}
```

First Code execution time was **1756557171 ms**.(Variable01.java)
Second Code execution time was **1826556296 ms**.(Variable02.java)

With those statistics, it's clear that declaring objects(Strings) in relevant scopes improves performance. But primitive data types are different. So I did same code for a primitive data type.

```java
public class Variable03 {

	public static void main(String[] args) {
		long startTime = System.nanoTime();
		Method();
		long endTime = System.nanoTime();

		long duration = endTime - startTime;

		System.out.println("Method runtime : " + duration + " ms");
	}

	public static void Method() {
		for (int i = 0; i < 100000; i++) {
			int str;
			// Some Logic
			str = i;
			System.out.println(str);
		}
	}

}

public class Variable04 {

	public static void main(String[] args) {
		long startTime = System.nanoTime();
		Method();
		long endTime = System.nanoTime();

		long duration = endTime - startTime;

		System.out.println("Method runtime : " + duration + " ms");
	}

	public static void Method() {
		int str;
		for (int i = 0; i < 100000; i++) {
			// Some Logic
			str = i;
			System.out.println(str);
		}
	}

}
```

int is a primitive data type. It will not behave like String did. Improvement is upside down here.

Third Code execution time was **1829664932 ms**.(Variable03.java)
Forth Code execution time was **1681147372 ms**.(Variable04.java)

Those statistics were collected from same machine with same condition. And I ran those programs against JRE 1.6.0_45. I saw a difference in result, when I ran those programs on JRE 1.7.0_45. Now I'm digging into it!

### Tags

- Java
- jvm
- garbage collector