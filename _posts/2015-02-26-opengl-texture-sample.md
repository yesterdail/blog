---
layout: post
title: "OpenGL 纹理采样"
tagline: "正确的指定纹理采样坐标"
category : tech
---

OpenGL 内置的纹理采样函数包括：

```c++
gvec4 texture(gsampler1D tex, float P[, float bias]);
gvec4 texture(gsampler2D tex, vec2 P[, float bias]);
gvec4 texture(gsampler3D tex, vec3 P[, float bias]);
gvec4 texture(gsamplerCube tex, vec3 P[, float bias]);
gvec4 texture(gsampler1DArray tex, vec2 P[, float bias]);
gvec4 texture(gsampler2DArray tex, vec3 P[, float bias]);
gvec4 texture(gsampler2DRect tex, vec2 P);
gvec4 texture(gsamplerCubeArray tex, vec4 P[, float bias]);
```

tex是指定纹理，P是纹理坐标。__纹理坐标的范围是在0到1之间，且C++中的数组索引0对应的纹理坐标位置为0.5，数组索引1对应的纹理坐标位置为1.5。__下面举例详细说明。

## 一个简单的纹理采样示例

<img class="myimg25" src="{{ site.baseurl }}\images\texturesample-backBuffer.png"></img>

创建一个大小为256的一维纹理，其值为从0到255。

在256 * 256大小的窗口中渲染图像，使第0列的像素值为0（纹理中的第0个值），第1列的像素值为1（纹理中的第1个值）……最后一列的像素值为255（纹理中的最后一个值），如右图。

有几点要注意的地方：

* 纹理类型指定为8位无符号整数。当纹理上传到GPU以后，会自动的转换为0到1之间的浮点数，即采样函数得到的值是位于0到1之间；
* 在指定顶点时，左下角为(0，0)，右上角是(256,256)；
* 在片元着色器中使用纹理采样函数，vs_coord.x + 0.5指定正确的纹理坐标位置，除以256，将纹理坐标归整到0到1之间。

```C++
// create texture
int window_width = 256;
int window_height = 256;
uint8_t* buffer = new uint8_t[window_width];
for (int idx = 0; idx < window_width; ++idx) {
  buffer[idx] = (uint8_t)idx;
}
texture = new Texture(
  glm::ivec3(window_width, 1, 1),
  GL_R8, 
  GL_RED, 
  GL_UNSIGNED_BYTE, 
  Texture::LINEAR, 
  reinterpret_cast<GLubyte*>(buffer));
delete []buffer;
```

```c++
// rendering
glBegin(GL_QUADS);
glVertex2f(0, 0);
glVertex2f((float)window_width, 0);
glVertex2f((float)window_width, (float)window_height);
glVertex2f(0, (float)window_height);
glEnd();
```

```c++
// fragment shader
in vec3 vs_coord;
out vec4 result;
uniform sampler1D image;
void main()
{
  float value = texture(image, (vs_coord.x + 0.5) / 256).r;
  result = vec4(value, value, value, 1);
}
```










