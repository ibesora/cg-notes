# Drawing without data

GLSL ES 3.0 introduces `gl_VertexID` which effectively counts vertices.

With that we can define a vertex shader that contains the data itself and use `gl_VertexID` to index the data.

```glsl
#version 460 core
layout (location=0) out vec3 color;
const vec2 pos[3] = vec2[3] (
	vec2(-0.6, -0.4),
	vec2(0.6, -0.4),
	vec2(0.0, 0.6)
);
const vec3 col[3] = vec3[3] (
	vec3(1.0, 0.0, 0.0),
	vec3(0.0, 1.0, 0.0),
	vec3(0.0, 0.0, 1.0)
);
void main() {
	gl_Position = vec4(pos[gl_VertexID], 0.0, 1.0);
	color = col[gl_VertexID];
}
```

We can then draw vertices without adding the data in a buffer via `glDrawArrays(GL_TRIANGLES, 0, 3);`

We don't need to define arrays in the vertex shader though, we can use `gl_VertexID` to compute vertex positions.

```glsl
#version 300 es
uniform int numVerts;
uniform vec2 resolution;

#define PI radians(180.0)

void main() {
  float u = float(gl_VertexID) / float(numVerts);  // goes from 0 to 1
  float angle = u * PI * 2.0;                      // goes from 0 to 2PI
  float radius = 0.8;

  vec2 pos = vec2(cos(angle), sin(angle)) * radius;

  float aspect = resolution.y / resolution.x;
  vec2 scale = vec2(aspect, 1);

  gl_Position = vec4(pos * scale, 0, 1);
  gl_PointSize = 5.0;
}
```

## Code snippets

- [Drawing a triangle](https://github.com/ibesora/cg-notes-code/blob/main/Examples/02_Triangle/src/main.cpp)
