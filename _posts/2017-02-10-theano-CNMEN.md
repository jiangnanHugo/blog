## Problem
Theano: CNMeM is disabled, CuDNN not available
## Solution
cnmem package: https://github.com/NVIDIA/cnmem
```
% cd $HOME
% git clone https://github.com/NVIDIA/cnmem.git cnmem
```
```
% cd cnmem
% mkdir build
% cd build
% cmake ..
% make
```
### link with cnmem
The source folder contains a header file `include/cnmem.h` and the build directory contains the library `libcnmem.so`, put them into your cuda path:  `/usr/local/cuda/include`,`/usr/local/cuda/lib64`

### .thenaorc config
```
[lib]
cnmem=1
```

### Test 
```
>>> import theano
>>> Using gpu device 0: GeForce GTX TITAN X (CNMeM is enabled with initial size: 95.0% of memory, cuDNN 5005)
```