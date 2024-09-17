# Compile source code

To install toncli from source on Linux or macOS:

1. Follow the [official instructions to compile](https://ton.org/docs/develop/howto/compile) the TON source code. \
   Note: You need to compile Disintar version  of TON which include needed stuff for toncli. It can be founded here: \[[link](https://github.com/disintar/ton/tree/toncli-local)]\
   Note: If you are using Arch Linux, you can use the [AUR package](https://aur.archlinux.org/packages/ton-git) for toncli. \

2. Install toncli using pip:
   * On Linux: $ `pip install toncli`
   * On macOS: $ `pip3 install toncli`
3. If you see a warning message saying that the toncli script is not on PATH, add the absolute path to the bin directory to your PATH environment variable.
4. Run toncli and pass the absolute path to the func, fift, and lite-client directories as arguments.
