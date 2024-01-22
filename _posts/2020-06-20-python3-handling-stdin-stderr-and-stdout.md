---
layout: post
title: "Python 3: Handling stdin, stderr and stdout with subprocess"
---

I don't like using subprocess that often. Using `subprocess` to invoke `curl` instead of using `requests` is not how you should use it. But there are valid exceptions.

Below example, I write to the `stdin` and then read `stdout` and `stderr`.

```python
from subprocess import Popen, PIPE

try:
    command = ["awk", "-F ", "{print  $2}"]
    process = Popen(command,
                    stdin=PIPE,
                    stdout=PIPE,
                    stderr=PIPE,
                    universal_newlines=True)
    process.stdin.write("column1 column2 column3\ndata1 data2 data3")
    process.stdin.close()
    process.wait()

    print("Process exited with " + str(process.returncode))
    print("Printing standard output")
    print(str(process.stdout.read()))
    print("Printing standard error")
    print(str(process.stderr.read()))
except FileNotFoundError:
    print("Program not found")
```

This is the output.

```
Process exited with 0
Printing standard output
column2
data2

Printing standard error

```

### Tags

- python
- subprocess