# Creating a vertex array object

Create the object and upload the data,

```cpp
  GLuint vao;
	glCreateVertexArrays(1, &vao);
```

bind it,

```cpp
  glBindVertexArray(vao);
```

upload the data to the buffer (this is an optional step because data can be generated in shaders),

```cpp

```

draw it,

```cpp
  glDrawArrays(GL_TRIANGLES, 0, 36);
```

and delete resources

```cpp
  glDeleteVertexArrays(1, &vaoID);
```
