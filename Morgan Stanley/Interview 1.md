Implement a Python decorator `timeit` that:

* Takes a function `func`
* Returns a new function that:

  * Measures how long `func` takes to run (in milliseconds)
  * Stores that value in a global variable `execution_time`
  * Returns the same output as `func`

---

Here’s the completed `timeit` decorator in Python:

```python
import time
from typing import Callable

execution_time = 0  # global variable to store execution time in ms

def timeit(func: Callable) -> Callable:
    def wrapper(*args, **kwargs):
        global execution_time
        start = time.time()
        result = func(*args, **kwargs)
        end = time.time()
        execution_time = int((end - start) * 1000)  # convert to ms
        return result
    return wrapper
```

### ✅ Example Usage:

```python
@timeit
def delay_max(a, b, c, delay=150):
    import time
    time.sleep(delay / 1000)  # convert ms to seconds
    return max(a, b, c)

print(delay_max(3, 4, 1, delay=150))
print("Execution time:", execution_time)
```

This will:

* Print `4`
* Print something close to `150` (in milliseconds)

