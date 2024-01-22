---
layout: post
title: "How to swap two integer variables without a third variable? - Java"
---

Well. We can swap two integer variables using third variables. That is not a problem. Let's say we want to swap two variables without using a third variable. For that, you can use simple mathematical operations such as addition/subtraction. But division multiplication will introduce an error to the data for example if you have to swap 1 and 3. Using subtraction and addition, you can swap two variables without affecting their values. 

```java
public class SwapInteger{

	public static void main(String args[]){
		int a = 5;
		int b = 10;

                System.out.println("Before swapping.");

                System.out.println("a = " + a);
                System.out.println("b = " + b);

		b = a + b;
		a = b - a;
		b = b - a;

                System.out.println("After swapping.");

		System.out.println("a = " + a);
		System.out.println("b = " + b);
	}
}
```

## Gist

- <https://gist.github.com/dedunumax/c95642c22ed52fdc4cbb>

### Tags

- Java
- programming
