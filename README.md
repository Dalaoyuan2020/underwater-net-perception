# Underwater Net Perception

柔性拦截网的水下状态感知：水下扫地机器人。地板换成阳江核电取水前池的柔性拦污网。

**写报告 / 本地 agent 先读：[`docs/CONTEXT.md`](docs/CONTEXT.md)** → [`docs/STATUS.md`](docs/STATUS.md)

- Repo: https://github.com/Dalaoyuan2020/underwater-net-perception
- License: MIT

## 一句话

地点：广东阳江核电南侧泵房前池 / 明渠末段的冷源取水拦污网。
不做渠道三维房间图。沿浮纲展开 2.5D 网系地图，贴网走，标道 / 跨 / 缝 / 洞 / 底隙。

三个问题：水中自身状态（我是谁）、水中定位（我在哪）、水中识别（网上什么状态）。

## 三个任务

| # | 任务 | 交付 |
|---|------|------|
| 1 | 网具 2.5D 建图 | 栅格 M(s,z) + 道跨缝洞底隙 |
| 2 | 低能见度视觉 | UIE + 结节/孔分割 |
| 3 | 自身–网关系 | 位姿 (s,z,d,psi) 贴网作业窗 |

## 有序加载

1. docs/CONTEXT.md — 地点、环境、装备、问题、进度
2. docs/STATUS.md — 当前做到哪
3. docs/tasks/ — 三个任务
4. docs/papers.md — 文献
5. docs/schema/net-grid.example.json
6. viz/ — 三维示意说明（HTML 在本地材料包）

## 明确不做

全空间 SLAM、空化盘设计、把清网当成主线。
