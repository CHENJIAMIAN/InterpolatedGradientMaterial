# InterpolatedGradientMaterial
>
> 物体表面热力图 - Three.js InterpolatedGradientMaterial Temperature Heatmap Demo
> 这是一个使用 **Three.js** 和自定义材质 **InterpolatedGradientMaterial** 创建的热力图演示。它展示了如何在 3D 空间中可视化不同温度值，用户可以动态控制几何体和热力图的显示。

`InterpolatedGradientMaterial` 是一个自定义的 ShaderMaterial，用于在 Three.js 场景中实现带有插值渐变效果的材质。通过不同的数值和颜色，您可以可视化数据点并生成平滑的颜色渐变。

## 特性

- **动态数据点**：支持在运行时更新数据点和数据值。
- **多种权重函数**：提供三种权重函数选项（逆距离、逆平方和指数），以影响渐变效果。
- **平滑边缘控制**：可以定义用于平滑渐变的边缘值。
- **颜色插值**：通过指定低色和高色，可以实现从一种颜色到另一种颜色的平滑过渡。

## 安装

确保您已经在项目中安装了 Three.js：

```bash
npm install three
```

然后将 `InterpolatedGradientMaterial` 导入到您的项目中：

```javascript
import { InterpolatedGradientMaterial } from './path/to/InterpolatedGradientMaterial';
```

## 使用示例

```javascript
import * as THREE from 'three';
import { InterpolatedGradientMaterial } from './path/to/InterpolatedGradientMaterial';

// 创建场景
const scene = new THREE.Scene();
const camera = new THREE.PerspectiveCamera(75, window.innerWidth / window.innerHeight, 0.1, 1000);
const renderer = new THREE.WebGLRenderer();
renderer.setSize(window.innerWidth, window.innerHeight);
document.body.appendChild(renderer.domElement);

// 定义数据点和数据值
const dataPoints = [new THREE.Vector3(0, 0, 0), new THREE.Vector3(1, 1, 0)];
const dataValues = [0, 1];

// 创建自定义材质
const material = new InterpolatedGradientMaterial({
    dataPoints: dataPoints,
    dataValues: dataValues,
    colorLow: new THREE.Color(0x0000FF),  // 蓝色
    colorHigh: new THREE.Color(0xFF0000), // 红色
    minValue: 0,
    maxValue: 1,
    weightFunction: 'inverse_square',
    smoothstepEdges: { min: 0.0, max: 1.0 }
});

// 创建几何体
const geometry = new THREE.SphereGeometry(1, 32, 32);
const mesh = new THREE.Mesh(geometry, material);
scene.add(mesh);

// 设置摄像机位置
camera.position.z = 5;

// 渲染循环
function animate() {
    requestAnimationFrame(animate);
    renderer.render(scene, camera);
}

animate();
```

## 属性

### 构造函数参数

- `dataPoints` (Array<THREE.Vector3>): 用于插值的3D数据点数组。
- `dataValues` (Array<float>): 与每个数据点相关联的值数组。
- `colorLow` (THREE.Color): 插值范围的起始颜色。
- `colorHigh` (THREE.Color): 插值范围的结束颜色。
- `minValue` (float): 数据值的最小值。
- `maxValue` (float): 数据值的最大值。
- `weightFunction` (string): 权重计算方法 ('inverse', 'inverse_square', 'exponential')。
- `smoothstepEdges` (Object): 包含两个浮点数 `min` 和 `max`，用于控制渐变的平滑边缘。

### 方法

- `updateData(dataPoints, dataValues)`: 更新材质的数据点和数据值。
- `recompileShader(newLength)`: 当数据点的数量改变时，重新编译Shader。

## 注意事项

- 在使用自定义材质时，要确保传递的数据点和数据值长度匹配。
- 该材质是一个 WebGLShaderMaterial，因此在使用前需要了解 Three.js 的基础知识。

## 许可证

MIT License.  
请参阅 `LICENSE` 文件以获取更多信息。

## 示例截图
![image](https://github.com/user-attachments/assets/3be567e0-f7c3-4315-ad21-a5b9dcac8363)

## 贡献

欢迎贡献！您可以通过 `fork` 该项目并提交 `pull request` 来进行贡献。
