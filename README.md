# LearnRust

Let's look at Rust through the lens of Python.

**Type safe:** \
In Python, you're used to being able to assign any type of value to a variable without much fuss. For example:

```python
x = 5  # x can be a number
x = "hello"  # now x can be a string
```

But in Rust, it's a bit stricter. Imagine if Python checked the type of variable each time you tried to use it, making sure you're not mixing things up unintentionally. It's like Python, but with extra guardrails:

```rust
let mut x = 5;  // x is a number
x = "hello";  // This would give an error in Rust because you can't change the type of x
```
---

**Memory safe:** \
In Python, memory management is mostly taken care of for you by the Python interpreter. You create objects, and Python cleans them up when they're not needed anymore. But in Rust, you have more control. It's like Python, but you have to be more mindful of where your data is and who's using it. For example, in Python:

```python
x = [1, 2, 3]  # Creates a list
y = x  # y now points to the same list as x
```

Here, both `x` and `y` point to the same list, and Python takes care of making sure the list sticks around as long as either `x` or `y` needs it. In Rust, it's a bit more explicit:

```rust
let mut x = vec![1, 2, 3];  // Creates a vector
let y = &x;  // y is a reference to x
```

In Rust, we're explicitly saying that `y` is a reference to `x`. This means that `y` can look at the data in `x`, but it can't change it. This prevents accidental changes that could mess things up.
---
**Data race free:** \
Python's Global Interpreter Lock (GIL) prevents multiple threads from executing Python bytecode at once, so data races are less of a concern in Python. But in Rust, where you can have multiple threads running simultaneously, it's important to make sure they don't step on each other's toes. It's like Python, but with a built-in referee to make sure everyone plays fair.

```python
# Python
import threading

def count():
    global x
    for _ in range(1000000):
        x += 1

x = 0
thread1 = threading.Thread(target=count)
thread2 = threading.Thread(target=count)
thread1.start()
thread2.start()
thread1.join()
thread2.join()
print(x)
```

In Python, even though we're using multiple threads here, the GIL makes sure that only one thread can execute Python bytecode at a time, so we don't have to worry about data races. But in Rust, the borrow checker would stop us from even trying something like this.
---
**Zero-cost abstractions:** \
Python's list comprehensions and higher-order functions like `map` and `filter` let you write code that's both concise and efficient. But in Rust, you have even more control over performance without sacrificing clarity. It's like Python, but with a turbo boost:

```python
# Python
squares = [x**2 for x in range(10)]
```

```rust
// Rust
let squares: Vec<i32> = (0..10).map(|x| x * x).collect();
```

In Rust, we're using a closure (`|x| x * x`) inside `map` to square each element of the range. This gives us the same result as the Python list comprehension, but with the added benefit of explicitness and control.
---
**Minimal runtime:** \
Python comes with a lot of built-in functionality, like garbage collection and dynamic typing, that make it easy to get started but can add overhead. Rust, on the other hand, gives you more control over what's included in your program, so you can keep things lean and mean. It's like Python, but with a leaner physique:

```python
# Python
def add(x, y):
    return x + y

result = add(3, 5)
```

```rust
// Rust
fn add(x: i32, y: i32) -> i32 {
    x + y
}

let result = add(3, 5);
```

In Rust, we're specifying the types of our function parameters (`x` and `y`) and return value (`-> i32`). This helps the compiler generate more efficient code because it knows exactly what types to expect.
---
**Targets bare metal:** \
Python is great for high-level tasks like web development and data analysis, but it's not as well-suited for low-level programming where you need to interact directly with hardware. Rust, on the other hand, can do it all. It's like Python, but with a hard hat and work boots:

```rust
// Rust
fn main() {
    println!("Hello, world!");
}
```

In Rust, this simple program prints "Hello, world!" to the console, just like a Python script would. But Rust can also be used to write operating systems, device drivers, and other low-level software where Python would struggle to keep up.

So, while Python and Rust have a lot in common, Rust gives you more control and flexibility, especially when it comes to performance and low-level programming. It's like Python's cool older sibling who's really good at everything!
---
