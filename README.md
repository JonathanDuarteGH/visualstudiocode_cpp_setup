# Visual Studio Code C/C++ Setup

- This is a repo specifically made to setup and test C/C++ on Visual Studio Code for Windows 10

- The original instructions on setting up C/C++ for various platforms can be found using the following link: [`https://code.visualstudio.com/docs/languages/cpp`](https://code.visualstudio.com/docs/languages/cpp)

- The link includes setups for C++ and other specific environments such as WSL, Mingw-w64, Clang/LLVM on macOS, and MSVC.

- The following will explain how to setup C/C++ using either MinGW or MinGW-w64 on Windows 10

## Table of Contents

- [Installing Microsoft C/C++ extension](#Installing-Microsoft-C/C++-extension)
- [Installing MinGW or MinGW-w64](#Installing-MinGW-or-MinGW-w64)
- [Configuring PATH](#Configuring-PATH)
- [Next Steps](#Next-Steps)
  - [Clone](#Clone)
  - [No Clone](#No-Clone)
  - [Following Steps](#Following-Steps)
- [Setting up JSON files](#Setting-up-JSON-files)
  - [Configuring the compiler path](#Configuring-the-compiler-path)
  - [Create a build task](#Create-a-build-task)
  - [Configure debug settings](#Configure-debug-settings)
- [Test](#Test)
- [FAQ](#FAQ)
  - [What is MinGW/MinGW-w64?](#What-is-MinGW/MinGW-w64?)
  - [Can Windows 10 run MinGW despite being a 32 bit architecture?](#Can-Windows-10-run-MinGW-despite-being-a-32-bit-architecture?)
  - [Why am I'm getting a “/bin/bash: [command] command not found” after setting up tasks.json and c_cpp_properties.json?](#Why-am-I'm-getting-a-“/bin/bash:-[command]-command-not-found”-after-setting-up-tasks.json-and-c_cpp_properties.json?)
  - [How do I know if MinGW/MinGW-w64 is installed correctly?](#How-do-I-know-if-MinGW/MinGW-w64-is-installed-correctly?)
  - [What if MinGW is not on the Path variable but it is still being referenced by another program or file directory?](#What-if-MinGW-is-not-on-the-Path-variable-but-it-is-still-being-referenced-by-another-program-or-file-directory?)
  - [Why are you using MinGW-w64 7.3.0 and not 8.1.0?](#Why-are-you-using-MinGW-w64-7.3.0-and-not-8.1.0?)
- [Acknowledgements](#Acknowledgements)
- [Contact](#Contact)

## Installing Microsoft C/C++ extension

- Simply click on the Extension icon on the sidebar of VSCode and search for "c++".

## Installing MinGW or MinGW-w64

- Install either [MinGW](https://sourceforge.net/projects/mingw/) or [MinGW-w64](https://mingw-w64.org/doku.php/start) to a folder that has no spaces in its directory. In this tutorial, it is assumed that either program is installed under `C:\MinGW` or `C:\mingw-w64`. 

- If you wish to install [MinGW](https://sourceforge.net/projects/mingw/), do so under these instructions:
  1. Click `Continue` on Step 1 and Step 2.
  2. Under the MinGW Installation Manager, right click and select on `Mark for Installation` for all the packages.
  3. Click on `Installation > Apply Changes > Apply`.
  4. Close the Installation manager.

- If you wish to install [MinGW-w64](https://mingw-w64.org/doku.php/start), do so under these settings:
  - Version: 7.3.0
  - Architecture: x86_64
  - Threads: win32
  - Exception: seh
  - Build revision: 0

## Configuring PATH

**Please read carefully. Any of the steps not taken will yield unexpected errors.**

1. In the Windows 10 search box, type `path`. Then choose `Edit the system environment variables` from the results list.

2. Scroll down under `System variables` and look for `Path`. Double click it. (You can also click on `Path` once, then click on `Edit`).

3. Scroll down on `Edit environment variable` and click `New`. Type in the path to where your file is installed. In this case it should be under `C:\MinGW\bin` or `C:\mingw-w64\x86_64-7.3.0-win32-seh-rt_v6-rev0\mingw64\bin`, depending on the version you've installed. Proceed by clicking `Ok`.

4. Under the `User variables for (YourComputersName)`, proceed to `Path` by double clicking or using the method explained above.

5. Type in the same exact path by clicking on `New` and then save it by clicking `Ok`.

6. Now **restart** your computer to initialize the paths.

## Next Steps

- You can either clone the repo to gain the complete files from this tutorial and/or follow along.

### Clone 

- You can skip the following (**No Clone**) and continue this tutorial. Make sure you have your terminal's directory set to where you can find your file. 

- I suggest setting up your directory to your `Desktop` and downloading the repo `git clone https://github.com/JonathanDuarteGH/visualstudiocode_cpp_setup.git`

### No Clone

- Make a `New Folder` in your Desktop and call it whatever you wish that is relevant to this tutorial.

### Following Steps

- Launch VS Code and click on the "Explorer" icon. 

- Add your newly created folder or the repo that you've just cloned to the workspace:
- `File > Add Folder To Workspace...`

## Setting up JSON Files

- Under your workspace, create a new C/C++ file and call it whatever you wish. In this tutorial, lets use `main.cpp`.

- Copy, paste, and save this code for testing:
```
#include <iostream>

using namespace std;

int main()
{
  
  int a = 21;
  int b = 22;
  cout << "The value of a and b are: " << a << " and " << b << endl;

  return 0;
}
```

### Configuring the compiler path

- Press `Ctrl+Shift+P` and in type in "C/C++: Edit Configurations".

- Select the workspace that you've added.

- Under your newly created `c_cpp_properties.json` file, copy and paste the following depending on the version of MinGW you are using:

MinGW:
```
{
    "configurations": [
        {
            "name": "Win32",
            "defines": [
                "_DEBUG",
                "UNICODE"
            ],
            "compilerPath": "C:/MinGW/bin/g++.exe",
            "intelliSenseMode": "gcc-x64",
            "browse": {
                "path": [
                    "${workspaceRoot}"
                ],
                "limitSymbolsToIncludedHeaders": true,
                "databaseFilename": ""
            }
        }
    ],
    "version": 4
}
```

MinGW-w64:
```
{
    "configurations": [
        {
            "name": "Win32",
            "defines": [
                "_DEBUG",
                "UNICODE"
            ],
            "compilerPath": "C:/mingw-w64/x86_64-7.3.0-win32-seh-rt_v6-rev0/mingw64/bin/g++.exe",
            "intelliSenseMode": "gcc-x64",
            "browse": {
                "path": [
                    "${workspaceRoot}"
                ],
                "limitSymbolsToIncludedHeaders": true,
                "databaseFilename": ""
            }
        }
    ],
    "version": 4
}
```

### Create a build task

- Press `Ctrl+Shift+P` and in type in "Tasks: Configure Task".

- Find your workspace folder (if prompted) and select "Create task.json file from template".
  - If it asks you for "C/C++: [cl.exe, cpp.exe, or g++.exe] build active file (yourWorkspaceFolder)", select any one of them

- Under your newly created `tasks.json` file, copy and paste the following:

```
{
  "version": "2.0.0",
  "tasks": [
    {
      "label": "echo",
      "type": "shell",
      "command": "g++",
      "args": [
        "-g", "${file}", "-o", "${fileBasenameNoExtension}.exe"
      ],
      "group": {
        "kind": "build",
        "isDefault": true
      },
      "problemMatcher": {
        "owner": "cpp",
        "fileLocation": ["relative","${workspaceRoot}"],
        "pattern": {
          "regexp": "^(.*):(\\d+):(\\d+):\\s+(warning|error):\\s+(.*)$",
          "file": 1,
          "line": 2,
          "column": 3,
          "severity": 4,
          "message": 5
        }
    }
  }]
}
```

- Select your `main.cpp` program and press `Ctrl+Shift+B` to build it.

- `main.exe` file should be created after the build.

### Configure debug settings

- Click on the "Debug" icon and press the drop down button

- Locate your workspace and Select "C++ (GDB/LLDB)" 

- Under your newly created `launch.json` file, copy and paste the following depending on the version of MinGW you've installed:

MinGW:
```
{
  "version": "0.2.0",
  "configurations": [
    {
      "name": "(gdb) Launch",
      "type": "cppdbg",
      "request": "launch",
      "program": "${fileDirname}\\${fileBasenameNoExtension}.exe",
      "args": [],
      "stopAtEntry": false,
      "cwd": "${workspaceFolder}",
      "environment": [],
      "externalConsole": false,
      "MIMode": "gdb",
      "miDebuggerPath": "C:/MinGW/bin/gdb.exe",
      "setupCommands": [
        {
          "description": "Enable pretty-printing for gdb",
          "text": "-enable-pretty-printing",
          "ignoreFailures": true
        }
      ]
    }
  ]
}
```

MinGW-w64:
```
{
  "version": "0.2.0",
  "configurations": [
    {
      "name": "(gdb) Launch",
      "type": "cppdbg",
      "request": "launch",
      "program": "${fileDirname}\\${fileBasenameNoExtension}.exe",
      "args": [],
      "stopAtEntry": false,
      "cwd": "${workspaceFolder}",
      "environment": [],
      "externalConsole": true,
      "MIMode": "gdb",
      "miDebuggerPath": "C:/mingw-w64/x86_64-7.3.0-win32-seh-rt_v5-rev0/mingw64/bin/gdb.exe",
      "setupCommands": [
        {
          "description": "Enable pretty-printing for gdb",
          "text": "-enable-pretty-printing",
          "ignoreFailures": true
        }
      ]
    }
  ]
}
```

## Test

- Delete the `main.exe` file. 

- Begin building the `main.cpp` program by pressing `Ctrl+Shift+B`.

- Click on the "Debug" Icon and click on your workspace from the drop down arrow.

- Click the green play button to see the debugging in action.

- If you would like to know how to use the debugger, please visit [`https://code.visualstudio.com/docs/languages/cpp`](https://code.visualstudio.com/docs/languages/cpp)

## FAQ

### What is MinGW/MinGW-w64?

- They are a Linux development environments that runs on Windows to create applications.

- MinGW and MinGW-w64 both have g++ compliers as well as gdb debuggers that can be used to run on the native Microsoft Windows platform.

### Can Windows 10 run MinGW despite being a 32 bit architecture?

- Programs under MinGW have 32 bits executables. But they can be used on 64 bits version of Windows. Therefore, you don't have to worry too much on compatibility.

### Why am I'm getting a “/bin/bash: [command] command not found” after setting up tasks.json and c_cpp_properties.json?

- This is because you are not setting your paths correctly. Please revisit [`Configuring the compiler PATH`](###-Configuring-the-compiler-PATH) to set it up exactly as it is written (i.e: did your **restart** your machine?).

### How do I know if MinGW/MinGW-w64 is installed correctly?

- Open your command prompt terminal and type `g++ --version`. This will give you the current version of MinGW/MinGW-w64.

### What if MinGW is not on the Path variable but it is still being referenced by another program or file directory?

- Open the command prompt and type `where g++`. This will reveal the location of your other MinGW in your system. 

- After finding your other MinGW, delete it.

- Move your **newly installed** MinGW folder into the directory the **old** MinGW was being called previously.

- Copy the new file path of that MinGW and paste it into your `environment variables` and `User variables for (YourComputersName)`. 
  - For example, codeblocks was referencing another MinGW folder. So I deleted it and moved my recently installed MinGW folder in its place. Then I copied its path `C:\Program Files (x86)\CodeBlocks\mingw-w64\x86_64-8.1.0-win32-seh-rt_v6-rev0\mingw64\bin`.

### Why are you using MinGW-w64 7.3.0 and not 8.1.0?

- According to this github issue, [`[gdb] [windows] unknown target exception 0x4000001f at 0x40163e #2285`](https://github.com/Microsoft/vscode-cpptools/issues/2285), there is an ongoing problem with with MinGW-w64 8.1.0 where the 64bit `gdb` crashes frequently. The `gdb` is the debugger for the compiler.

## Acknowledgements

- [Visual Studio Code Language Docs (C/C++)](https://code.visualstudio.com/docs/languages/cpp)

## Contact

This is an ongoing repo doc. So feel free to contact me for any feedback, suggestions, or questions.

Jonathan Duarte - [jonathanduarte313@gmail.com](mailto:jonathanduarte313@gmail.com)