原理简介
- 核心部分的素描渲染效果参考经典论文Real-Time Hatching。（论文链接  http://hhoppe.com/hatching.pdf）
- 以论文中给出的一组Tonal Art Maps为基础，用混合纹理的形式模拟素描笔触效果。
- 纹理由左到右表示亮度由亮到暗的素描效果，亮的纹理图片是暗的纹理图片的子集。
- 根据点受到的光照强度采样对应的纹理贴图，6张基础纹理将亮度分为6段，每段混合相邻两张纹理。

实现方法
- 采用three.js实现，需要实现的主要步骤：
  - 模型、场景构建，使用了提供的几何体搭建简单场景。
  - 着色器Shader的实现，在片元着色器中实现对应混合纹理贴图。
  - 监听鼠标操作，场景移动、缩放。（相机改变透视投影矩阵，鼠标操作视角改变）

参数
- 调节光照参数对素描笔触效果影响较大，调节uv纹理坐标参数使得笔触变得稀疏或密集，对于不同形状的物体uv纹理坐标乘以不同的参数可能会得到更好的效果。
- Phong 光照模型
  - 环境光照 Ambient Lighting
  - 漫反射光照 Diffuse Lighting
  - 镜面光照 Specular Lighting
  - 光泽度 Shineness
- 纹理坐标(u,v)
  -u=u*uscale，v=v*vscale
  -每个分量乘个线性的值（稀疏、密集）
