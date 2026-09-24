# Underwater Net Perception

柔性拦截网的水下状态感知：把网当成一张 **2.5D 网系地图**，机器人贴网走，标出道 / 跨 / 缝 / 洞 / 底隙，并保持自身相对网的安全工况。

开源仓库。路径规划、清网执行不在本仓库主线；本仓库只做 **感知**。

- Repo: https://github.com/Dalaoyuan2020/underwater-net-perception
- License: MIT

## 一句话

不做水下三维房间图。沿浮纲展开网面，格子记离网距、离底距和特征；机器人在这张网上定位和行走，像扫地机器人在地板栅格上走，只是地板换成了网。

## 三个任务（先做这些）

| # | 任务 | 交付 |
|---|------|------|
| 1 | **网具 2.5D 建图** | 网系栅格 M(s,z)：道、跨、缝、洞、底隙、离网 d、离底 h |
| 2 | **低能见度视觉** | 水下恢复 + 网分割，让浑水图能看清结节和孔 |
| 3 | **自身–网关系** | 位姿 (s,z,d,psi)：在哪一跨、多深、离网多远、是否贴平、是否在作业窗 |

特征识别默认写进地图格子，不单开第四个课题。

## 坐标

- s：沿浮纲（第几跨）
- z：深度
- d：法向离网距
- psi：相对网面偏航（是否与网平行）

## 方案图（给本地 / GPT 画正式图用）

```mermaid
flowchart LR
  subgraph sensors [传感器]
    SONAR[前视声呐/测距]
    CAM[相机+灯]
    IMU[IMU+深度计]
    DOWN[下视测距]
  end
  subgraph t2 [任务2 低能见度视觉]
    UIE[水下图像恢复 UIEB/EUVP]
    SEG[结节/纲线/孔分割]
  end
  subgraph t3 [任务3 自身状态]
    POSE[位姿 s,z,d,psi]
    STOFF[贴网距离与姿态闭环]
  end
  subgraph t1 [任务1 网系2.5D地图]
    GRID[栅格 M(s,z)]
    LABELS[道 跨 缝 洞 底隙]
  end
  SONAR --> POSE
  DOWN --> GRID
  IMU --> POSE
  CAM --> UIE --> SEG --> LABELS
  SONAR --> LABELS
  POSE --> STOFF
  POSE --> GRID
  LABELS --> GRID
  GRID --> WALK[贴网行走 / 覆盖]
```

把这段 mermaid 丢给画图模型即可出架构图。

## 仓库结构

```
docs/tasks/     三个任务说明
docs/papers.md  可引用文献
docs/notes/     现场与装备备忘
viz/            三维示意（浏览器打开）
AGENTS.md       给本地 agent 的入口
```

## 明确不做

- 全渠道三维 SLAM
- 单靠视觉走完全渠
- 空化清网头设计（另线）
- 覆盖规划以外的「智能化」大包

## 本地 agent

先读 `AGENTS.md` 和 `docs/tasks/`。
