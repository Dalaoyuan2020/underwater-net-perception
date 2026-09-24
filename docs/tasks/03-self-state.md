# 任务 3：自身状态 / 与网的关系

## 目标

机器人必须知道：**自己在哪一跨、多深、离网多远、是否与网平行、是否在作业窗内。**

这是贴网行走的前提。没有这一项，2.5D 地图对不齐。

## 状态

x = (s, z, d, psi)

| 量 | 传感器 | 含义 |
|----|--------|------|
| s | 跨号先验 + 沿纲里程 + Tag | 在哪一跨 |
| z | 深度计 | 水深条带 |
| d | 前视声呐 / 激光 | 离网是否安全 |
| psi | IMU + 网面法向 | 是否贴平 |
| h | 下视测距 | 离底，写进地图 |

作业窗示例：d 在 0.2–0.4 m，姿态与网平行。超出则先矫正再标特征。

## 学术名

relative pose regulation on a deformable surface；wall following + standoff control。
不是开水域 AUV 导航，不单独立项 SLAM 论文。

## 相关工作

- FFT 估网相对位姿（Schellewald；Frontiers in Robotics 2025）
- 定深定距绕网巡检，ROS + Gazebo（JMSE 2025）
- TagSLAM + BlueROV2 网箱巡检（arxiv 2503.00482）
- 主动调到能看清的距离再检测（Sci. Rep. 2025）
