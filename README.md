# How to Setup PyBind11

This minimal example shows how to setup PyBind11 on Ubuntu 22.04. To learn more about PyBind11 check out the [official documentation](https://pybind11.readthedocs.io/en/stable/index.html).

To 

```shell
git clone <this_repo>
cd <this_repo>
python -m venv venv
source venv/bin/activate
pip3 install pybind11

clang++ -shared -fPIC -std=c++11 -I./pybind11/include/ `python3.10 -m pybind11 --includes` example.cpp -o mymodule.so `python3.10-config --ldflags`
```

__Note:__ If you encounter an error after running the last command, check out the section **Common Errors** below.

You should now have a binary file called `mymodule.so` in the root directory of your project. You can confirm that it got created by running:

```shell
ls
```

You can now further confirm that your c++ code can be executed from a python script by running:

```shell
ipython3
```

```ipython
import mymodule

mymodule.add(5, 2)
```

Expected output is `7` as per the `add()` function defined in `example.cpp`. 

Have fun with PyBind11!


## Common Errors

For your own reference, see some common errors and possible fixes below.

```shell
Command 'clang++' not found, but can be installed with:
sudo apt install clang
```

Try install clang with:

```shell
sudo apt install clang
```

---

If during the compilation of `example.cpp` you encounter the following error:

```shell
~/YourProject/venv/lib/python3.10/site-packages/pybind11/include/pybind11/detail/common.h:303:10: fatal error: 'cstddef' file not found
#include <cstddef>
         ^~~~~~~~~
1 error generated.
```

Run the following command first and then try again:

```shell
sudo apt install libstdc++-12-dev
```

---


