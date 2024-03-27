## Cpp project settings

## Install package manager for windows

1. **Installing Scoop**: [*Click Here for install scoop*](https://scoop.sh/)
    ```powershell
    Set-ExecutionPolicy -ExecutionPolicy RemoteSigned -Scope CurrentUser
    Invoke-RestMethod -Uri https://get.scoop.sh | Invoke-Expression
    ```

2. **Verify Installation**: After installation completes, verify Scoop is installed by running:
    ```powershell
    scoop help
    ```

3. **Install GCC Compiler**: Once Scoop is installed, you can install GCC compiler by running:
    ```powershell
    scoop install gcc
    ```

4. **Install CMake**: Install CMake. [Click Here](https://cmake.org/download/)

### Create Project

1. **Create CMakeLists.txt**: In the root directory project. Set up variables before the project() line in CMakeLists.txt
    ```CMake
    cmake_minimum_required(VERSION 3.10)

    set(CMAKE_C_COMPILER "C:/Users/sergi/scoop/apps/gcc/current/bin/gcc.exe")
    set(CMAKE_CXX_COMPILER "C:/Users/sergi/scoop/apps/gcc/current/bin/g++.exe")

    project(MyProject)

    # ...

    add_executable(MyProject main.cpp)
    ```
    *In CMAKE_C_COMPILER, enter your compiler path, it may not be the same*

2. **Create Build Directory**: Open PowerShell in your desired location and run:
    ```powershell
    mkdir build && cd build
    ```

3. **Run CMake**: Run CMake to generate build files for your project. You have 2 options:
    - **For `Make`**
        - Install Make:
            ```powershell
            scoop install make
            ```
        - Use "MinGW Makefiles" as the generator for GCC for your project:
            ```powershell
            cmake -G "MinGW Makefiles" ..
            ```
            *If not function, try:*
            ```powershell
            cmake -G "MinGW Makefiles" -DCMAKE_MAKE_PROGRAM="C:\path\to\make.exe" ..
            ```

    - **For `Ninja`** (Modern and Fazt buildin)
        - Install Ninja:
            ```powershell
            scoop install ninja
            ```
        - Use "Ninja" as the generator for GCC for your project
            ```powershell
            cmake -G Ninja ..
            ```

4. **Build Project**: Once CMake has configured the project, build it by running:
    ```powershell
    cmake --build .
    ```

### Execute Project:

1. **Run Executable**: After successful build, you can find the executable in the build directory. Run it using:
    ```powershell
    ./executable.exe
    ```

### Visual Studio Code Configuration Path

- If you have used scoop, put the following configurations in `settings.json` in VSCode
    ```json
    {
        "C_Cpp.default.includePath": [
            "C:/Users/sergi/scoop/apps/gcc/13.2.0/include/**",
            // other library paths ...
            "C:/Users/sergi/scoop/apps/glfw/3.4/include/**", // for glfw library headers
        ],
    }
    ```


## Debuggin in C++
### In terminal (with GDB)
1. **Compile your program in the terminal:**
    ```bash
    g++ programa.cpp -g -o programa
    ```
    El parametro `-g` incluye la depuracion
2. **Load your program with GDB:**
    ```bash
    gdb programa
    ```
3. **Setting Breakpoints in your program:**
    "Write `break` followed by the line number where you want it to stop your program."
    ```bash
    (gdb) break 7
    ```    
    Also you can execute:
    ```bash
    (gdb) info breakpoints
    ```  
    To list all the breakpoints
4. **Execute `run` for the program to execute until it reaches the breakpoint:**
    ```bash
    (gdb) run
    ```    
5. **For inspect variables:**
    ```bash
    (gdb) print i
    ```    
    *Replace i with name variable*
6. **View the Call Stack:**
    ```bash
    (gdb) backtrace
    ```  
    or
    ```bash
    (gdb) bt
    ```  
7. **To continue the execution line by line:**
    ```bash
    (gdb) step
    ```  
    or
    ```bash
    (gdb) s
    ```  
8. **To Continue to the next breakpoint:**
    ```bash
    (gdb) continue
    ```
9. **To exit GDB:**
    ```bash
    (gdb) quit
    ```  

### In VScode
1. **Open the Source File**
2. **Set Breakpoints:**
    Click on the left margin of the source code at the line(s) where you want to set breakpoints. A red dot will appear indicating a breakpoint.
3. **Open Debugger:**
    In VS Code, you can open the Debugger panel from the sidebar or use the keyboard shortcut Ctrl+Shift +D
4. **Configure Debugger:**
    In the Debugger panel, click on the gear icon to configure the debugger.
    Choose the environment you are using ("C++ (GDB/LLDB)").
    And choose configuration: C/C++:g++.exe build and debug active file
5. **Start Debugging:**
    Click the green play (Start Debugging) button in the top-left corner of the Debugger panel.
    Alternatively, use the keyboard shortcut F5.
6. **Debugging:**
    The debugger will start and halt at the first breakpoint encountered.
    You can inspect variables in the Variables panel, control the execution in the Call Stack panel, and see console output in the Debug Console panel.
7. **Stepping Through Code:**
    Use the debugger controls in the top of the Debugger panel to step through your code.
    "Step Over" (F10): Executes the current line and stops at the next line.
    "Step Into" (F11): Moves the debugger into a function call.
    "Step Out" (Shift+F11): Steps out of the current function.
    "Continue" (F5): Resumes execution until the next breakpoint.
8. **Inspecting Variables:**
    While debugging, you can hover over variables to see their current values.
    Variables panel: Displays all variables in the current scope.
    Watch panel: Add specific variables or expressions to monitor during debugging.
9. **Stopping Debugging:**
    Click the red square (Stop) button in the top-left corner of the Debugger panel.
    Alternatively, use the keyboard shortcut Shift+F5.

