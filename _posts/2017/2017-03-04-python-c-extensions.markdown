---
layout: "post"
title: "python C extensions"
date: "2017-03-04 22:16"
comments: true
---

### Note:
 these content is collect from book [Intermediate Python](http://book.pythontips.com/en/latest/python_c_extension.html) and [Hitchhiker's Guide to Python](http://docs.python-guide.org/en/latest/scenarios/clibs/).

## 1. C Foreign Function Interface

`CFFI <https://cffi.readthedocs.io/en/latest/>` provide a simple to use mechanism for interfacing with C from CPython and PyPy. It supports two model:

1. a inline ABI compatibility model, you can dynamically load and run functions from executable modules
2. an API model, can build C extension modules.

ABI Interaction
```python
from cffi import FFI
ffi=FFI()
ffi.cdef("size_t strlen(const char*);")
clib=ffi.dlopen(None)
length=clib.strlne(String to be evaluated.)
#print:23
print("{}".format(length))
```


## 2. CTypes

the ctypes modules provides C compatible data types and functions to load DLLs so that calls can be made to C shared libraries without having to modify them.

Simple C code to add two numbers, save it as `add.c`
```c
// sample C file to add 2 numbers -int and floats

#include<stdio.h>
int add_int(int,int);
int add_float(float,float);

int add_int(int p,int q){
  return p+q;
}

float add_float(float p,float q){
  return p+q;
}
```
Next we compile the C file to a `.so` file (or `DLL`) :
```
gcc -shared -Wl,-soname,adder -o adder.so -fPIC add.c
```

Now in your python code:
```python
from ctypes import *

# load the shared object file
adder=CDLL('./adder.so')

# Find sum of integers
res_int=adder.add_int(4,5)
print "Sum of 4 and 5 =" +str(res_int)

# >>> Sum of 4 and 5 = 9


# find sum of floats
a=c_float(5.5)
b=c_float(4.1)

add_float=adder.add_float
add_float.restype=c_float
print "Sum of 5.5 and 4.1 = ", str(add_float(1,b))

# >>> Sum of 5.5 and 4.1 =  9.60000038147
```
## 3. Simplified Wrapper and Interface Generator (SWIG)
In this method, the developer must develop an extra interface file which is an input to SWIG.  This is a great method when you have a C/C++ code base, and you want to interface it to many different languages.

The C code `example.c` that has avariety of functions and variables
```c
#include<time.h>
double my_variable=3.0;

int fact(int n){
  if(n<1) return 1;
  else  return n*fact(n-1);
}

int my_mod(int x,int y){
  return (x%y);
}

char* get_time(){
  time_t ltime;
  time(&ltime);
  return ctime(&ltime);
}
```

The interface file `example.i` - this will remain the same irrespective of the language you want to port yout C code:
```
/* example.i */
 %module example
 %{
 /* Put header files here or function declarations like below */
 extern double My_variable;
 extern int fact(int n);
 extern int my_mod(int x, int y);
 extern char *get_time();
 %}

 extern double My_variable;
 extern int fact(int n);
 extern int my_mod(int x, int y);
 extern char *get_time();
```

And compile it:
```
unix % swig -python example.i
unix % gcc -c example.c example_wrap.c \
        -I/usr/local/include/python2.1
unix % ld -shared example.o example_wrap.o -o _example.so
```

Finally, the Python output:
```
>>> import example
>>> example.fact(5)
120
>>> example.my_mod(7,3)
1
>>> example.get_time()
'Sun Feb 11 23:01:07 1996'
>>>
```
It's too complex.

## 4. C/Python API
Its the most widely used method - it’s simplicity and you can manipulate python objects in your C code.

All python object are represented as `PyObject` struct which is defined in `Python.h` header file. For example,
 if the PyObject is also a PyListType (basically a list), the we can use the `PyList_Size()` for the length of the list ( equal to `len(list)`). Most of the basic functions/operations are defined in `Python.h`


`adder.c`
```c
//

```
waiting for update.
