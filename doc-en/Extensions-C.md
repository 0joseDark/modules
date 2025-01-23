**Extensions in C/C++**: Python allows creating extensions in C/C++ that can be called directly from Python code. This can be achieved with tools such as **Cython**, **ctypes**, **cffi**, and **CPython API**.

**Assembly Code**: It is rare, but we can use Assembly in Python indirectly by incorporating it into C libraries.

### 1. Using C code with `ctypes`

The `ctypes` library allows loading C libraries and calling functions directly from Python. First, we create a C library and then call its functions in Python.

#### Example with `ctypes`

1. **Create a C library**: Let's create a file `calculator.c` with basic functions.

   ```c
   // calculator.c
   #include <stdio.h>

   int add(int a, int b) {
       return a + b;
   }

   int subtract(int a, int b) {
       return a - b;
   }
   ```

2. **Compile the library**: In the terminal, compile the C code as a shared library:

   ```bash
   gcc -shared -o calculator.so -fPIC calculator.c
   ```

   On Windows, the command would be:

   ```bash
   gcc -shared -o calculator.dll calculator.c
   ```

3. **Use the library in Python**:

   ```python
   # main.py
   import ctypes

   # Load the library
   calculator = ctypes.CDLL('./calculator.so')  # On Windows, './calculator.dll'

   # Configure the return types of the functions
   calculator.add.restype = ctypes.c_int
   calculator.subtract.restype = ctypes.c_int

   # Use the functions
   result_add = calculator.add(10, 5)
   result_subtract = calculator.subtract(10, 5)

   print("Addition:", result_add)          # Output: Addition: 15
   print("Subtraction:", result_subtract)  # Output: Subtraction: 5
   ```

### 2. Using C code with `cffi`

The `cffi` library is another way to call C functions in Python. It allows for more detailed interaction and is useful for accessing complex C structures.

1. **Create the C library** (use the same `calculator.c` code as in the previous example).

2. **Compile the library** (as shown above).

3. **Use `cffi` in Python**:

   ```python
   # main.py
   from cffi import FFI

   ffi = FFI()

   # Declare the C functions we want to use
   ffi.cdef("""
       int add(int a, int b);
       int subtract(int a, int b);
   """)

   # Load the library
   calculator = ffi.dlopen('./calculator.so')  # On Windows, './calculator.dll'

   # Use the functions
   result_add = calculator.add(10, 5)
   result_subtract = calculator.subtract(10, 5)

   print("Addition:", result_add)          # Output: Addition: 15
   print("Subtraction:", result_subtract)  # Output: Subtraction: 5
   ```

### 3. Using Assembly with Python (via C)

Python does not directly support Assembly, but we can use Assembly in C functions and then call them in Python using `ctypes` or `cffi`.

1. **Create a C code with embedded Assembly**:

   ```c
   // assembly_func.c
   #include <stdio.h>

   int add(int a, int b) {
       int result;
       __asm__ ("add %1, %2; mov %2, %0"
                : "=r"(result)       // Output
                : "r"(a), "r"(b)    // Inputs
                );
       return result;
   }
   ```

2. **Compile the C code into a library**:

   ```bash
   gcc -shared -o assembly_func.so -fPIC assembly_func.c
   ```

3. **Use the library in Python**:

   ```python
   # main.py
   import ctypes

   # Load the library
   assembly_func = ctypes.CDLL('./assembly_func.so')  # On Windows, './assembly_func.dll'

   # Configure the return type of the function
   assembly_func.add.restype = ctypes.c_int

   # Use the function
   result = assembly_func.add(10, 5)
   print("Result (Assembly):", result)  # Output: Result (Assembly): 15
   ```

### 4. Creating Extensions with Cython

**Cython** compiles Python code into C code, allowing the use of C data types and direct access to C libraries.

1. **Create a `.pyx` file**:

   ```python
   # calculator.pyx
   cdef int add(int a, int b):
       return a + b

   cdef int subtract(int a, int b):
       return a - b
   ```

2. **Create the setup to compile with Cython**:

   ```python
   # setup.py
   from setuptools import setup
   from Cython.Build import cythonize

   setup(
       ext_modules=cythonize("calculator.pyx")
   )
   ```

3. **Compile the Cython module**:

   ```bash
   python setup.py build_ext --inplace
   ```

4. **Use the compiled module in Python**:

   ```python
   # main.py
   import calculator

   print("Addition:", calculator.add(10, 5))          # Output: Addition: 15
   print("Subtraction:", calculator.subtract(10, 5))  # Output: Subtraction: 5
   ```

These techniques allow integrating Python with low-level code, offering significant flexibility and control over performance.
