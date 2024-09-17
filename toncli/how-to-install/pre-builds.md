# Pre-builds

## Linux or macOS (Intel)

1.  Download the needed pre-builds for Linux or macOS from the SpyCheese repository:

    * Linux: \[[link](https://github.com/SpyCheese/ton/actions/runs/3176936192)]
    * macOS: \[[link](https://github.com/SpyCheese/ton/actions/runs/3176936191)]&#x20;

    Note: You need to be logged in to GitHub to download the pre-builds.
2. Install Python 3.9 or higher.
3. Install toncli using pip:
   * On Linux: $ `pip install toncli`
   * On macOS: $ `pip3 install toncli`
4. If you see a warning message saying that the toncli script is not on PATH, add the absolute path to the bin directory to your PATH environment variable.
5. Run toncli and pass the absolute path to the func, fift, and lite-client directories from the first step as arguments.

## Windows

To install and run toncli on Windows:

1.  Download and install the latest version of Python 3.9 or higher from the official website.&#x20;



    Note: Do not install the Microsoft Store version, as it will not work. \
    \
    Tip: On the first screen of the installer, click the "Add Python to PATH" checkbox to make it easier to run Python and toncli from the command line.\
    ![image](https://user-images.githubusercontent.com/19264196/160259049-8ed99862-a765-4653-84cb-b6818c0aa0b3.png)
2. Open the console by pressing `Win+X` and selecting `Windows Terminal` from the menu.
3. Install `toncli` using pip: `pip install toncli`
4. Download the compiled TON binaries from the [SpyCheese repository on GitHub](https://github.com/SpyCheese/ton/actions/runs/3176936196).\
   You need to be logged in to GitHub to download the files.
5. Unzip the downloaded archive and add the [libcrypto-1\_1-x64.dll](https://disk.yandex.ru/d/BJk7WPwr\_JT0fw) file to the unzipped files.
6. Open the folder containing the unzipped files in the console. \
   Tip: To open the folder in the console, right-click on the folder and select "Open in Terminal" in Windows 11, or copy the path of the folder in Explorer and run `cd [copied path]`"in PowerShell (Win+X).
7. Run `toncli` in the console.&#x20;

Success! You can now use toncli on Windows.
