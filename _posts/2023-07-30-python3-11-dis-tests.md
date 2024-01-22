---
layout: post
title: "Python 3.11 dis tests"
---

I recently found out about `dis` module in Python. I wrote two simple functions.

```python
def function_1(x, y):
  x + y


def function_2(x, y);
  return x + y
```

I used `dis` module to find out about the bytecode operations for each function. 

```python
from dis import dis

print("="*60)
dis(function_1)
print("="*60)
dis(function_2)
print("="*60)
```

I thought the first function would have fewer bytecode operations. But this is the output I got from the `dis` module.

```console
============================================================
  5           0 RESUME                   0

  6           2 LOAD_FAST                0 (y)
              4 LOAD_FAST                1 (z)
              6 BINARY_OP                0 (+)
             10 POP_TOP
             12 LOAD_CONST               0 (None)
             14 RETURN_VALUE
============================================================
  9           0 RESUME                   0

 10           2 LOAD_FAST                0 (y)
              4 LOAD_FAST                1 (z)
              6 BINARY_OP                0 (+)
             10 RETURN_VALUE
============================================================
```

Turns out the first function has more bytecode operations. It loads the None value and return it. I wanted to run some tests around the running time. I ran the function for thousands of times and recorded the running time. 

![](/resources/16.png)

![](/resources/17.png)

Above two figures shows the difference between `function_1` and `function_2` execution time on an AMD Dual core processors. I was hoping to see more clear evidence, I thought `function_2` would be slightly faster. X axis shows number of times I ran the functions in a loop. Y axis shows the difference in time (function_1 time - function_2 time).

![](/resources/18.png)

![](/resources/19.png)

Above two charts shows the same test on an Intel chip. I don't see any clear evidence.

![](/resources/20.jpeg)

I ran the same number of functions calls for 250 times and got this variation in differences. I am still not sure about the results. I will investigate this further.

### Tags

- python
- dis
- disassembler
