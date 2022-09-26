# Using a texture

Create the object and upload the data,

```cpp
  int w, h, comp;
	const uint8_t* img = stbi_load(path, &w, &h, &comp, 3);
	GLuint texture;
	glCreateTextures(GL_TEXTURE_2D, 1, &texture);
	glTextureParameteri(texture, GL_TEXTURE_MAX_LEVEL, 0);
	glTextureParameteri(texture, GL_TEXTURE_MIN_FILTER, minFilter);
	glTextureParameteri(texture, GL_TEXTURE_MAG_FILTER, maxFilter);
	glTextureStorage2D(texture, 1, GL_RGB8, w, h);
	glPixelStorei(GL_UNPACK_ALIGNMENT, 1);
```

bind it,

```cpp
  glBindTextures(0, 1, &texture);
```

upload the data to the buffer,

```cpp
  glTextureSubImage2D(texture, 0, 0, 0, w, h, GL_RGB, GL_UNSIGNED_BYTE, img);
	stbi_image_free((void*)img);
```

and draw it

```glsl
  layout (location=0) in vec2 uv;
  layout (location=0) out vec4 out_FragColor;
  // Notice that we don't need to send which texture we are using because they are bound in order
  uniform sampler2D texture0;
  void main() {
    out_FragColor = texture(texture0, uv);
  }
```
