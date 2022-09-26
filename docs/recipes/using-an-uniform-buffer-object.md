# Using an uniform buffer object

Create the object and upload the data,

```cpp
  // Define a uniform buffer struct
  struct PerFrameData
  {
    mat4 mvp;
    int isWireframe;
  };
```

bind it,

```cpp
  const GLsizeiptr kBufferSize = sizeof(PerFrameData);
	GLuint perFrameDataBuffer;
	glCreateBuffers(1, &perFrameDataBuffer);
	glNamedBufferStorage(perFrameDataBuffer, kBufferSize, nullptr, GL_DYNAMIC_STORAGE_BIT);
```

upload the data to the buffer,

```cpp
  PerFrameData perFrameData = { .mvp = p * m, .isWireframe = false };
	glNamedBufferSubData(perFrameDataBuffer, 0, kBufferSize, perFrameData);
```

draw it,

```cpp
  glBindBufferRange(GL_UNIFORM_BUFFER, 0, perFrameDataBuffer, 0, kBufferSize);
```

and delete the resources

```cpp
  glDeleteBuffers(1, &perFrameDataBuffer);
```
