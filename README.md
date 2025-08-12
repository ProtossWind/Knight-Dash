# Knight Dash - 项目介绍

- [**项目概况**](#项目概况)
- [**主要贡献**](#主要贡献)
- [**实现细节**](#实现细节)
- [**项目展示**](#项目展示)

## 项目概况
- **项目名称**：Knight Dash（横版过关）

- **开发周期**：2023.08 – 2023.10

- **团队规模**：4 人

- **技术栈**：Unity、C#、HLSL（ShaderLab）、GitHub

- **项目简介**：本游戏为一款横版过关类作品，玩家需操作主角通过跳跃、攻击、防御等动作克服复杂地形与敌人的阻碍。团队自主设计了角色技能、关卡机制、敌人行为及视觉特效。

## 主要贡献
### 角色控制与交互逻辑

- 编写C#脚本实现包含角色攻击、防御、二段跳与冲刺等动作的完整控制系统。

- 实现玩家与道具、敌人之间包括触发器、伤害/效果、受击无敌等交互机制。

### 后处理特效设计

- 独自设计并实现泛光效果（多着色器组合）：

    - `Blooming.shader`：控制物体自身发光亮度；

    - `BloomingObject.shader`：筛选需泛光物体并着色；

    - `GaussianBlur.shader`：对图像进行双通道高斯模糊以实现光的扩散（水平/垂直、GPU优化）；

    - `ComposeBloom.shader`：将模糊图层与原始画面合成，最终产生泛光视觉。

- 编写 `CameraBloom.cs` 脚本管理渲染流程、模糊等级与分辨率缩放。
<p align="center">
  <img src="Images\Bloom-effect\1-origin.png" width="354">
  <img src="Images\Bloom-effect\2-final.png" width="354">
</p>
<p align="center">
    泛光特效应用前后对比
</p>

### 粒子系统开发（激光技能特效）

- 构建Unity粒子系统，创造主角释放光束时的爆发感。

- 调整粒子参数并添加子发射器模拟光束爆发、扩散、衰减的过程。

<p align="center">
    <img src="Images\ParticleSystem\gif.gif" width="443">
</p>

## 实现细节
### 高斯模糊

- 使用双摄像机分离捕捉原图与发光图层。

- 通过 `GaussianBlur.shader` 的调用次数实现泛光强度的改变， 两个通道交替进行水平/垂直方向的高斯模糊以实现2D模糊效果。

- 通过缩放模糊图层分辨率以兼顾画面效果和GPU性能。

### 粒子系统

- 主发射器采用锥形形状、扇形角度控制发射方向。

- 设置发射速度、粒子大小/透明度随生命周期变化。

- 添加子发射器模拟激光产生的闪光与火花。

- 整体特效增强玩家释放技能时的能量感和打击反馈。

## 项目展示
**在线试玩**：[GitHub Pages](https://protosswind.github.io/Knight-Dash/) - 项目已完整实现玩法机制、角色技能与视觉特效，游戏Demo资源齐全且运行稳定。

**演示视频**：[MP4](https://github.com/ProtossWind/Knight-Dash/raw/refs/heads/main/demo.mp4) - 视频内容为项目早期版本，最终版本已完善泛光效果与贴图资源。
