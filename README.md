# AgiBot Raise A3 Ultra USD
[English](./README_EN.md)

[![USD](https://img.shields.io/badge/format-OpenUSD-7A4EAB)](https://openusd.org/)
[![Isaac Sim](https://img.shields.io/badge/Isaac%20Sim-6.0.1-76B900)](https://developer.nvidia.com/isaac/sim)
[![Asset Structure](https://img.shields.io/badge/Asset%20Structure-3.0-blue)](#资产结构)

智元机器人（AgiBot）Raise A3 Ultra T3D0 的仿真级 USD 资产，面向 NVIDIA Isaac Sim 6.0.1，并按 Isaac Sim Asset Structure 3.0 组织。

仓库包含机器人层级、视觉网格、材质、碰撞体、质量与惯量、关节限制及驱动参数，同时提供通用 USD Physics、PhysX 和 MuJoCo 物理变体。

## 特性

- 完整的双足人形机器人运动学层级
- 视觉模型、材质和碰撞几何
- 刚体质量、质心和惯量参数
- 关节限位、最大驱动力和驱动配置
- Isaac Robot Schema：`IsaacRobotAPI`、`IsaacLinkAPI`、`IsaacJointAPI` 和 `IsaacSiteAPI`
- 可切换的 `Physics` Variant Set：
  - `none`：不加载物理层
  - `physics`：加载引擎无关的 USD Physics 配置
  - `physx`：加载 PhysX 专用配置，默认选项
  - `mujoco`：加载 MuJoCo 物理层
- 米制单位，Z 轴向上

## 兼容性

| 组件 | 版本或约定 |
| --- | --- |
| NVIDIA Isaac Sim | 6.0.1 |
| 资产结构 | Structure 3.0 |
| 文件格式 | OpenUSD（`.usd` / `.usda`） |
| 默认 Prim | `/agibot_a3` |
| 长度单位 | 米 |
| 上轴 | Z |
| 默认物理变体 | `physx` |

> 该资产针对 Isaac Sim 6.0.1 的 Schema 和资产结构编写。其他版本或纯 OpenUSD 工具可以读取基础 USD 内容，但 Isaac/PhysX 专用 Schema 的行为可能不同。

## 资产结构

```text
raise_a3_ultra_t3d0/
├── interface.usda                 # Structure 3.0 推荐入口与 Physics 变体
├── raise_a3_ultra_t3d0.usda       # 兼容入口
└── payloads/
    ├── base.usda                  # 机器人层级、视觉和碰撞实例
    ├── robot.usda                 # Isaac Robot Schema
    ├── geometries.usd             # 二进制几何数据
    ├── instances.usda             # 可复用视觉/碰撞实例
    ├── materials.usda             # 材质定义
    └── Physics/
        ├── physics.usda           # 引擎无关的刚体、关节和驱动参数
        ├── physx.usda             # PhysX 专用覆盖
        └── mujoco.usda            # MuJoCo 物理入口
```

资产通过 USD composition arcs 进行分层：

1. `interface.usda` 引用 `base.usda`，加载运动学层级与几何实例。
2. `robot.usda` 作为 sublayer，添加 Isaac Robot Schema 元数据。
3. `Physics` Variant 按需 payload 对应的物理层。
4. `base.usda` 通过 `materials.usda`、`instances.usda` 和 `geometries.usd` 组合外观与碰撞数据。

## 许可证

本项目采用[木兰宽松许可证第 2 版（Mulan PSL v2）](./LICENSE)授权。
