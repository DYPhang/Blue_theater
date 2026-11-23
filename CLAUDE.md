# Blue Theater

@AGENTS.md

## 项目本地技能

- 技能源目录：`.agents/skills/`（来自 awesome-gamedev-agent-skills，Apache-2.0，见 `LICENSE` / `NOTICE`）
- Claude Code 加载副本：`.claude/skills/`。更新源目录后需重新同步，例如：
  `Copy-Item ".agents\skills\*" ".claude\skills\" -Recurse -Force`
- 开工读取顺序：`README.md` → `.agents/skills/router/SKILL.md`，再由 router 只挑当前任务需要的技能，不要一次加载全部。

## 当前状态

- 这是一个类似《红色警戒》的 2D 海战 RTS，引擎已经确定为 **Unity**。
- 环境现状：仅有 Python 3.13；不要假设 Node.js、Unity Editor 或 Unity Hub 已安装。
- 创建或打开 Unity 项目后，先读取 `ProjectSettings/ProjectVersion.txt` 并遵循项目实际版本。
- 海面寻路使用 `game-ai` 中的网格 A*、路点图或流场；`unity-navmesh` 只作为岛内/地面导航备选。
- 玩法行为要用可运行的检查验证，不能只靠看画面。
