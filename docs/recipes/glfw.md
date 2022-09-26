# GLFW

Choose an OpenGL version

```cpp
  glfwWindowHint(GLFW_CONTEXT_VERSION_MAJOR, majorVersion);
	glfwWindowHint(GLFW_CONTEXT_VERSION_MINOR, minorVersion);
  glfwWindowHint(GLFW_OPENGL_PROFILE, GLFW_OPENGL_CORE_PROFILE);
```

Create a Window

```cpp
  // monitor and share are nullptr by default
  glfwCreateWindow(width, height, title, monitor, share)
```

Setting a keyboard callback

```cpp
  glfwSetKeyCallback(window,
		[](GLFWwindow *window, int key, int scancode, int action, int mods) {
			if (key == GLFW_KEY_ESCAPE && action == GLFW_PRESS) {
				glfwSetWindowShouldClose(window, GLFW_TRUE);
			}
		}
	);
```

Terminating GLFW

```cpp
  glfwTerminate();
```

## Code snippets

- [Creating a window](https://github.com/ibesora/cg-notes-code/blob/main/Examples/01_GLFW/src/main.cpp)
