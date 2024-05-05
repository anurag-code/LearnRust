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


## Let's explore the Rust module system from the perspective of Python.

## Modules in Python

In Python, a module is a file containing Python definitions and statements. Modules allow you to organize your code into logical units, similar to how Rust's module system works.

Here's how the Rust module system concepts translate to Python:

### Crates in Rust vs. Packages in Python
- In Rust, a **crate** is the smallest compilable unit of code. In Python, the equivalent is a **package**.
- A Python package is a collection of Python modules, organized into a directory structure. This is similar to how a Rust crate can contain a hierarchy of modules.
- Just like Rust crates, Python packages can be distributed and reused across different projects.

### Modules in Rust vs. Modules in Python
- In Rust, a **module** is a collection of related items (functions, structs, traits, etc.) that are grouped together.
- In Python, a **module** is a single Python file that contains definitions and statements.
- Both Rust and Python use the `mod` keyword to define modules, but the syntax and usage differ.

### Paths in Rust vs. Imports in Python
- In Rust, you use **paths** to access items within modules and crates.
- In Python, you use **imports** to access modules and their contents.
- The `use` keyword in Rust is similar to the `import` statement in Python, but the syntax and semantics differ.

Here's an example to illustrate the differences:

**Rust**
```rust
// Crate: my_crate
mod utils {
    pub fn do_something() {
        println!("Doing something!");
    }
}

mod app {
    use crate::utils;

    pub fn run() {
        utils::do_something();
    }
}

fn main() {
    app::run();
}
```

**Python**
```python
# Package: my_package
# Module: utils.py
def do_something():
    print("Doing something!")

# Module: app.py
from my_package.utils import do_something

def run():
    do_something()

if __name__ == "__main__":
    run()
```

In the Rust example, we have a crate named `my_crate` with two modules: `utils` and `app`. The `utils` module exposes a `do_something()` function, which is then used in the `app` module. The `main` function calls the `run()` function from the `app` module.

In the Python example, we have a package named `my_package` with two modules: `utils.py` and `app.py`. The `utils.py` module defines a `do_something()` function, which is then imported and used in the `app.py` module. The `if __name__ == "__main__":` block ensures that the `run()` function is executed when the `app.py` module is run directly.

The key differences are:
- Rust uses crates and modules, while Python uses packages and modules.
- Rust uses the `mod` keyword to define modules, while Python uses the file system to organize modules.
- Rust uses paths to access items, while Python uses imports.
- Rust has explicit visibility control with the `pub` keyword, while Python relies on the file system and import statements.

Overall, the Rust module system and the Python module system serve similar purposes of organizing code, but the specific syntax and implementation details differ between the two languages.

Citations:
[1] https://doc.rust-lang.org/rust-by-example/mod.html
[2] https://dev.to/stevepryde/intro-to-rust-modules-3g8k
[3] https://aloso.github.io/2021/03/28/module-system.html
[4] https://www.sheshbabu.com/posts/rust-module-system/
[5] https://web.mit.edu/rust-lang_v1.25/arch/amd64_ubuntu1404/share/doc/rust/html/book/first-edition/crates-and-modules.html

---

### More on Crates and Modules

**Crates and Modules: Building Blocks of Rust Programs**

- **Crates:** Similar to Python packages, crates are self-contained units of code in Rust. They act as the smallest compilation unit, meaning the Rust compiler processes them as a whole. A crate can either be:
    - **Binary Crate:** Compiles into an executable program you can run directly, like a Python script.
    - **Library Crate:** Provides reusable code that other crates (including binary crates) can import and use. This is analogous to Python modules.
- **Modules:** Just like in Python, modules help you organize code within a crate. They group related functions, variables, and types together, promoting readability and maintainability. Modules can nest within each other, creating a hierarchy.

**Paths and Privacy Control**

- **Paths:** Imagine paths as addresses for accessing code elements in your Rust program. They specify the location of a definition, like a function, variable, or module. Similar to Python's dot notation (e.g., `module.function()`), paths in Rust use double colons (::) to separate module and element names (e.g., `crate_name::module_name::function_name`).
- **Privacy Control:** Modules offer a powerful feature for controlling code visibility. By default, items within a module are private and cannot be accessed directly from outside that module. This helps you hide implementation details and promotes encapsulation. To make something publicly accessible, you explicitly declare it with the `pub` keyword. This is similar to Python's concept of private and public members within classes or modules.

**Using Crates and Libraries: Expanding Your Toolkit**

- **Rust Standard Library (std):** Built-in with Rust, the `std` library provides essential building blocks for common programming tasks. It includes definitions for:
    - Data types (e.g., `String` for text, `Vec<T>` for dynamic arrays)
    - Primitive operations (e.g., mathematical functions, string manipulation)
    - Utility functions (e.g., file I/O, environment interaction)
    - Much more!
- **Third-Party Crates:** The `crates.io` repository offers a vast collection of reusable code beyond the standard library. These crates cover various functionalities, from:
    - Command-line argument parsing (`structopt`)
    - Date and time handling (`chrono`)
    - Regular expressions (`regex`)
    - Data serialization/deserialization (`serde`)
    - And countless others!
- **Importing Code with `use`:** To utilize code from a crate or library in your Rust program, you employ the `use` keyword. It brings the specified items into scope, allowing you to use them without constantly writing the full path each time. Imagine it as importing modules in Python's `import` statement.

**Illustrative Examples (Python Equivalents):**

1. **Defining and Using a Module:**

   ```rust
   // crate_name/src/my_module.rs (Rust)
   mod my_module {
       fn greet(name: &str) {
           println!("Hello, {}!", name);
       }
   }

   // crate_name/src/main.rs (Rust)
   fn main() {
       use crate::my_module; // Import the entire module
       my_module::greet("Alice"); // Access the greet function
   }
   ```

   **Python Equivalent:**

   ```python
   # my_module.py
   def greet(name):
       print(f"Hello, {name}!")

   # main.py
   from my_module import greet  # Import the greet function
   greet("Alice")
   ```

2. **Using the Standard Library for File I/O:**

   ```rust
   use std::fs;

   fn main() {
       let content = fs::read_to_string("myfile.txt").unwrap();
       println!("File content: {}", content);
   }
   ```

   **Python Equivalent:**

   ```python
   import os

   with open("myfile.txt", "r") as file:
       content = file.read()
   print(f"File content: {content}")
   ```

By understanding crates, modules, paths, and how to use external libraries, you'll be well on your way to writing modular, reusable, and efficient Rust code, similar to what you're familiar with in Python!

---

**Use Rust crates and libraries**
The Rust Standard Library std contains reusable code for fundamental definitions and operations in Rust programs. This library has definitions for core data types like String and Vec<T>, operations for Rust primitives, code for commonly used macro functions, support for input and output actions, and many other areas of functionality.

There are tens of thousands of libraries and third-party crates available to use in Rust programs most of which can be accessed through Rust's third-party crate repository crates.io. You'll learn later how to access these crates from your project, but for now here are some crates used in the programming exercises:

**std** - The Rust standard library. In the Rust exercises, you'll notice the following modules:
- std::collections - Definitions for collection types, such as HashMap.
- std::env - Functions for working with your environment.
- std::fmt - Functionality to control output format.
- std::fs - Functions for working with the file system.
- std::io - Definitions and functionality for working with input/output.
- std::path - Definitions and functions that support working with file system path data.
- structopt - A third-party crate for easily parsing command-line arguments.
- chrono - A third-party crate to handle date and time data.
- regex - A third-party crate to work with regular expressions.
- serde - A third-party crate of serialization and deserialization operations for Rust data structures.

By default, the std library is available to all Rust crates. To access the reusable code in a crate or library, we implement the use keyword. With the use keyword, the code in the crate or library is "brought into scope" so you can access the definitions and functions in your program. The standard library is accessed in use statements with the path std, as in use std::fmt. Other crates or libraries are accessed with their name, such as use regex::Regex.

---

## Cargo in Rust

Let's explore how the Rust Cargo tool compares to project management in Python.

## Project Management in Python

In Python, there are a few common ways to manage projects and dependencies:

1. **Virtual Environments**: Python's built-in `venv` module (or third-party tools like `pipenv` or `poetry`) allow you to create isolated Python environments with their own dependencies.
2. **Requirements Files**: You can use a `requirements.txt` file to list your project's dependencies, which can then be installed using `pip install -r requirements.txt`.
3. **Setuptools/Distutils**: These are Python's built-in tools for packaging and distributing Python projects. They allow you to define metadata, dependencies, and other project-related information in a `setup.py` file.
4. **Poetry**: A modern dependency management and packaging tool for Python, with features like dependency resolution, virtual environments, and publishing to PyPI.

While these tools provide functionality similar to Rust's Cargo, the specific commands and workflow differ. Let's compare how Cargo and these Python tools handle common project management tasks.

### Creating a New Project
**Cargo**:
```
cargo new my_project
```
This command creates a new Rust project with the following structure:
```
my_project/
├── Cargo.toml
└── src/
    └── main.rs
```
The `Cargo.toml` file is the project manifest, which contains metadata and dependency information.

**Python**:
There is no single command to create a new Python project. Typically, you would manually create a new directory and set up the project structure, which may include a `setup.py` file, a `requirements.txt` file, and a `src/` or `my_project/` directory for your Python modules.

### Adding Dependencies
**Cargo**:
To add a dependency, you edit the `Cargo.toml` file and add the crate name and version under the `[dependencies]` section:
```toml
[dependencies]
serde = "1.0"
```
Then, you can use the crate in your Rust code:
```rust
extern crate serde;
```

**Python**:
To add a dependency, you can either:
1. Add the package name and version to your `requirements.txt` file:
   ```
   requests==2.28.1
   ```
   Then install the dependencies using `pip install -r requirements.txt`.
2. Use a tool like `pip`, `pipenv`, or `poetry` to add the dependency directly:
   ```
   pip install requests
   ```

### Building and Running the Project
**Cargo**:
```
cargo build  # Compile the project
cargo run   # Build and run the project
```
Cargo will handle compiling the project, including any dependencies, and generating the final executable.

**Python**:
There is no single command to build and run a Python project. Typically, you would:
1. Ensure your virtual environment is activated.
2. Run the Python interpreter directly on your main script:
   ```
   python my_project/main.py
   ```
   Or, if you've set up a `setup.py` file, you can use `python setup.py install` to install the project, and then run the installed script.

### Testing the Project
**Cargo**:
```
cargo test  # Run the project's tests
```
Cargo's built-in testing framework makes it easy to write and run tests for your Rust project.

**Python**:
Python has several testing frameworks, such as `unittest`, `pytest`, and `doctest`. To run tests, you would typically use the framework's command-line tool:
```
pytest my_project/tests/
```
or, if you've set up a `setup.py` file, you can use `python setup.py test`.

### Publishing the Project
**Cargo**:
```
cargo publish  # Publish the project to crates.io
```
Cargo handles the entire process of publishing your Rust library or application to the central crates.io repository.

**Python**:
To publish a Python project, you would typically:
1. Ensure your `setup.py` file is properly configured with metadata and dependencies.
2. Use `python setup.py sdist` to create a source distribution.
3. Use `python setup.py bdist_wheel` to create a binary distribution.
4. Upload the distributions to PyPI using a tool like `twine`.

Overall, while the specific commands and workflow differ, both Cargo and the various Python tools serve the same purpose of managing project dependencies, building, testing, and publishing your code. The Rust Cargo tool provides a more integrated and streamlined experience compared to the more fragmented approach in the Python ecosystem.

Citations:
[1] https://www.youtube.com/watch?v=WIB6xqdWMqk
[2] https://www.programiz.com/rust/cargo
[3] https://www.kevsrobots.com/learn/rust/13_cargo.html
[4] https://blog.waleedkhan.name/rust-modules-for-python-users/
[5] https://crates.io/crates/python-project-generator/0.3.0