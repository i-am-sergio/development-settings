## OpenGL Configurations

1. **Download glew**: `Binaries` for windows. [**Click Here**](https://glew.sourceforge.net/)
2. **Download glfw**: `Binaries` for windows. [**Click Here**](https://www.glfw.org/download.html)
3. **Extract Folders**: Put folder in C root directory `C:\`

## Compile OpenGL project

1. **Compile with GCC**: Run the following command:
    ```powershell
    g++ -g -std=c++17 `
    -IC:\glfw-3.4.bin.WIN64\include `
    -IC:\glew-2.1.0\include `
    -LC:\glew-2.1.0\lib\Release\x64 `
    -LC:\glfw-3.4.bin.WIN64\lib-mingw-w64 `
    C:\Users\sergi\Desktop\project\src\main.cpp `
    -lglfw3dll -lglew32 -lopengl32 `
    -o C:\Users\sergi\Desktop\project\executable.exe
    ```
    <!-- ```powershell
    g++ -g -std=c++17 -IC:\Users\sergi\Desktop\project\include -LC:\Users\sergi\Desktop\project\lib C:\Users\sergi\Desktop\project\src\main.cpp C:\Users\sergi\Desktop\project\src\glad.c -lglfw3dll -o C:\Users\sergi\Desktop\project\executable.exe
    ``` -->

2. **Compile with CMake**:
    - Create a `CMakeLists.txt`:
        ```cmake
        cmake_minimum_required(VERSION 3.10)
        project(OpenGLProject)

        # Version of C++ language
        set(CMAKE_CXX_STANDARD 17)
        set(CMAKE_CXX_STANDARD_REQUIRED ON)

        # Add directories of the libraries for including (header files)
        include_directories(
            C:/glfw-3.4.bin.WIN64/include
            C:/glew-2.1.0/include
        )

        # Add the directories of the libraries for linking
        link_directories(
            C:/glew-2.1.0/lib/Release/x64
            C:/glfw-3.4.bin.WIN64/lib-mingw-w64
        )

        configure_file(C:/glfw-3.4.bin.WIN64/lib-mingw-w64/glfw3.dll ${CMAKE_BINARY_DIR}/glfw3.dll COPYONLY)

        add_executable(OpenGLProject src/main.cpp)

        # Link the openGL and GLFW libraries
        target_link_libraries(OpenGLProject -lopengl32)
        target_link_libraries(OpenGLProject -lglew32)
        target_link_libraries(OpenGLProject -lglfw3dll)
        ```
    - Create build directory in root project:
        ```powershell
        mkdir build && cd build
        ```
    - In build directory project, for create makefiles run:
        ```powershell
        cmake -G Ninja
        ```
    - Compile project running:
        ```powershell
        cmake --build .
        ```

3. **Explore Samples using OpenGL**: 
    - `Sample 1:`
    ```cpp
    #include <GLFW/glfw3.h>

    void display()
    {
        glClear(GL_COLOR_BUFFER_BIT);
        glColor3f(1.0, 1.0, 1.0); // Draw a white grid "floor" for the tetrahedron to sit on.
        glBegin(GL_LINES);
        for (GLfloat i = -2.5; i <= 2.5; i += 0.25)
        {
            glVertex3f(i, 0, 2.5);
            glVertex3f(i, 0, -2.5);
            glVertex3f(2.5, 0, i);
            glVertex3f(-2.5, 0, i);
        }
        glEnd();

        // Draw the tetrahedron.  It is a four sided figure, so when defining it
        // with a triangle strip we have to repeat the last two vertices.
        glBegin(GL_TRIANGLE_STRIP);
        glColor3f(1, 1, 1);
        glVertex3f(0, 2, 0);
        glColor3f(1, 0, 0);
        glVertex3f(-1, 0, 1);
        glColor3f(0, 1, 0);
        glVertex3f(1, 0, 1);
        glColor3f(0, 0, 1);
        glVertex3f(0, 0, -1.4);
        glColor3f(1, 1, 1);
        glVertex3f(0, 2, 0);
        glColor3f(1, 0, 0);
        glVertex3f(-1, 0, 1);
        glEnd();

        glFlush();
    }

    void init()
    {
        // Set the current clear color to sky blue and the current drawing color to white.
        glClearColor(0.1, 0.39, 0.88, 1.0);
        glColor3f(1.0, 1.0, 1.0);

        // Tell the rendering engine not to draw backfaces.  Without this code,
        // all four faces of the tetrahedron would be drawn and it is possible
        // that faces farther away could be drawn after nearer to the viewer.
        // Since there is only one closed polyhedron in the whole scene,
        // eliminating the drawing of backfaces gives us the realism we need.
        // THIS DOES NOT WORK IN GENERAL.
        glEnable(GL_CULL_FACE);
        glCullFace(GL_BACK);

        // Set the camera lens so that we have a perspective viewing volume whose
        // horizontal bounds at the near clipping plane are -2..2 and vertical
        // bounds are -1.5..1.5.  The near clipping plane is 1 unit from the camera
        // and the far clipping plane is 40 units away.
        glMatrixMode(GL_PROJECTION);
        glLoadIdentity();
        glFrustum(-2, 2, -1.5, 1.5, 1, 40);

        // Set up transforms so that the tetrahedron which is defined right at
        // the origin will be rotated and moved into the view volume.  First we
        // rotate 70 degrees around y so we can see a lot of the left side.
        // Then we rotate 50 degrees around x to "drop" the top of the pyramid
        // down a bit.  Then we move the object back 3 units "into the screen".
        glMatrixMode(GL_MODELVIEW);
        glLoadIdentity();
        glTranslatef(0, 0, -3);
        glRotatef(50, 1, 0, 0);
        glRotatef(70, 0, 1, 0);
    }

    int main(void)
    {
        GLFWwindow * window;

        if (!glfwInit()) // Initialize the library
            return -1;

        // Create a windowed mode window and its OpenGL context
        window = glfwCreateWindow(640, 480, "Square", NULL, NULL);
        if (!window)
        {
            glfwTerminate();
            return -1;
        }

        glfwMakeContextCurrent(window); // Make the window's context current

        // Loop until the user closes the window
        while (!glfwWindowShouldClose(window))
        {
            int width, height; // Set the viewport size
            glfwGetFramebufferSize(window, &width, &height);
            glViewport(0, 0, width, height);
            glClear(GL_COLOR_BUFFER_BIT); // Clear the color buffer

            init();
            display(); // Call the display function

            glfwSwapBuffers(window); // Swap front and back buffers

            glfwPollEvents(); // Poll for and process events
        }
        glfwTerminate();
        return 0;
    }
    ```

[***View More Examples***](https://cs.lmu.edu/~ray/notes/openglexamples/)

