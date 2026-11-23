# Strategy Implementation Simulation（战略落地模拟）

一个面向 EMBA 课堂的中英双语网页模拟游戏：玩家扮演变革推动者，在有限资源（时间/精力）内说服组织成员接受新战略，最后按「转化人数」生成结局评价，并接入全球排行榜。

## 在线游玩

直接打开仓库根目录的 `index.html` 即可运行（单文件、无构建依赖）；或者通过 GitHub Pages 访问（开启 Pages 后地址为 `https://<用户名>.github.io/strategy/`）。

## 玩法简介

- 每回合有有限的「时间块」（资源），选择行动：邮件通报 / 全员宣讲 / 信息打探 / 深度劝说 / 私下劝说等。
- 每位成员有立场档位与隐藏的深层偏好；一对一「深度劝说」和「私下劝说」才能真正推动高阻力成员。
- 全部成员转化（或资源耗尽）后结算，按转化人数、剩余资源、回合数生成结局报告，并计入排行榜（演示局永远垫底）。
- 页面上有常驻按钮可一键切换 中文 / English。
- 支持本地自动存档：输入相同姓名可恢复上一局进度。

## 维护说明（给修改者）

本仓库的产物是根目录的 `index.html`（可直接部署），由 `src/` 下的流水线生成：

1. **只改 `src/game.html`**（中文文案与玩法的唯一真相源）。
2. 如需改词典，编辑 `src/dict-*.json`（`dict-z.json` 最后加载、覆盖前面的重复键）。
3. 在 `src/` 目录里运行 `python build.py`，重新生成双语版 `game_i18n.html`。
4. 用 `game_i18n.html` 覆盖根目录的 `index.html`。
5. 改完词典后可跑 `node runtime_check.js` 做中英回译回归（基线：FAILS 为有意的占位人名，约 8 条）。

注意：**永远不要直接编辑根目录 `index.html`**，它是生成物。

### 排行榜后端

排行榜使用云端服务：`https://6xvtcs5llrd6k.kimi.site`（`courseId=strategy-cn`，按课区分榜单；换课程时在 `src/leaderboard.js` 里改 `courseId` 即可）。玩家完成一局后自动提交成绩；`demo:true` 的演示局永远排在最后。

## 文件说明

| 文件 | 作用 |
|---|---|
| `index.html` | 可直接运行的双语游戏（生成物） |
| `src/game.html` | 中文游戏源码（唯一要改的文件） |
| `src/i18n-engine.js` | 运行时中英切换引擎 |
| `src/leaderboard.js` | 排行榜前端（含存档/恢复逻辑） |
| `src/build.py` | 双语构建脚本 |
| `src/dict-*.json` | 中英词典（分片，`dict-z` 最后覆盖） |
| `src/runtime_check.js` | 回译回归检查 |
| `src/to_translate_clean.json` | 词典生成的中间产物 |

## License

课堂教学用途，保留出处即可。
