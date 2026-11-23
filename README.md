# Blue Theater 游戏开发 Skills

> **开发环境版本与验证记录**：见 [docs/环境版本.md](docs/环境版本.md)。环境信息不写在本 README 里，避免技能包更新时被覆盖。

这个文件夹是给后续 agent 使用 **Unity 开发“红警式海战游戏”** 准备的项目本地技能包。它不是游戏源码，也不依赖全局安装；打开 Blue Theater 作为工作目录后，agent 可以直接从 `.agents/skills/` 读取。

## 已安装的 skills

| Skill | 用途 | 为什么适合 Blue Theater |
|---|---|---|
| `router` | 按引擎和任务自动分派 skill | 后续需求从设计、AI 到性能优化时，先走统一路由 |
| `game-docs` | 一页式 GDD、功能索引和设计同步 | 先固定资源、建造、编队、交战和胜负规则 |
| `game-ai` | FSM、感知、转向、A* 和流场寻路 | 舰船追击、巡逻、绕岛、攻击目标和返航 |
| `tower-defense` | 波次、目标优先级、经济曲线和数值检查 | 可借鉴其经济与目标筛选思路，但它不是完整 RTS 模板 |
| `level-design` | 地图布局、节奏和可玩性检查 | 设计海域、岛链、航道、资源点和出生区域 |
| `game-ui-ux` | HUD、菜单、缩放、焦点和无障碍规范 | 资源栏、建造面板、编队状态和战斗提示 |
| `performance-optimization` | 帧预算、对象池和性能瓶颈定位 | 大量舰船、炮弹、迷雾和寻路时的性能控制 |
| `unity-csharp-scripting` | Unity C#、序列化和脚本生命周期 | 舰船、武器、生产和 RTS 系统的主要代码层 |
| `unity-input-system` | Unity Input System | 鼠标选择、框选、点击移动和快捷键 |
| `unity-physics` | Unity 2D/3D 物理与碰撞层 | 舰船碰撞、射弹、射程和选择判定 |
| `unity-animation` | Unity Animator 与动画状态 | 舰船转向、受损、开火和生产反馈 |
| `unity-scriptableobjects` | ScriptableObject 配置资产 | 把舰种、武器、建筑、造价和科技树做成数据 |
| `unity-tilemap-2d` | Unity Tilemap 与规则瓦片 | 海域、岛礁、浅水和可航行区域 |
| `unity-navmesh` | Unity AI Navigation | 岛内或地面单位导航备选，不直接用于海面寻路 |
| `unity-build-pipeline` | Unity 构建与 CI | 生成 Windows 测试包和后续正式版本 |
| `unity-build-size` | Unity 构建体积审计 | 控制纹理、音频和安装包体积 |

## 推荐的开发顺序

1. 用 `game-docs` 写第一版 GDD，明确单人或联机、视角、资源、建造、编队、战斗和胜负条件。
2. 用 `level-design` 与 `unity-tilemap-2d` 做一张可玩的灰色海域地图。
3. 用 `unity-csharp-scripting`、`unity-input-system`、`unity-physics` 和 `unity-scriptableobjects` 实现舰船、鼠标选择、点击移动和数据驱动单位。
4. 用 `game-ai` 的网格 A*、路点图或流场实现海面寻路、目标选择、巡逻、追击和返航；不要假定 NavMesh 可以覆盖海上航道。
5. 从 `tower-defense` 借用经济、波次/敌方进攻和目标优先级思路，再扩展成真正的 RTS 生产与指挥循环。
6. 用 `game-ui-ux` 完成资源栏、建造菜单、编队和战斗 HUD。
7. 用 `performance-optimization` 在大量单位与弹体出现后测量并优化帧预算。
8. 功能稳定后使用 `unity-build-pipeline` 和 `unity-build-size` 生成并检查测试版本。

## 给后续 agent 的起始提示词

```text
先阅读 Blue Theater/README.md 和 .agents/skills/router/SKILL.md。
这是一个类似红警的 2D 海战 RTS，引擎已经选择 Unity。
按 game-docs → level-design → unity-tilemap-2d → unity-csharp-scripting →
unity-input-system → unity-physics → unity-scriptableobjects → game-ai → game-ui-ux 的顺序，
先交付可运行的垂直切片：一张海域地图、资源采集、船厂建造、舰船点击移动、
编队与攻击、敌方 AI，以及基础 HUD。不要一次实现全部内容。
```

## 边界与来源

- 这套技能的引擎部分已经切换为 Unity；技能内容以 Unity 6.3 LTS 为基线。创建项目后必须读取 `ProjectSettings/ProjectVersion.txt`，并按项目实际版本核对 API。
- 海面寻路优先采用网格、路点图或流场；`unity-navmesh` 是岛内/地面导航备选，不应在未验证水面导航的情况下直接使用。
- 仓库中没有成熟的“红警式海战 RTS”专用 skill。`tower-defense` 只复用经济曲线、波次和目标选择结构，海军单位编队、生产建筑、资源采集和基地建造仍需在项目中设计并测试。
- 上游仓库：[gamedev-skills/awesome-gamedev-agent-skills](https://github.com/gamedev-skills/awesome-gamedev-agent-skills)
- 固定版本：`c6ca6c41c839b68319ffc08430b99ab768debc32`
- 许可证：Apache-2.0，完整文本见 `LICENSE`，归属说明见 `NOTICE`。

