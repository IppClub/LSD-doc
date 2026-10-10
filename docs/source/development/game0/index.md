# Game 0 开发规划

更新时间：2026-10-09。本文档组包含原始盘点、持续设计细化及当前验收记录。

目标是基于原有策划、程序和社区资产完成《灵数奇缘》Game 0：玩家通过亲自示范教会学员战斗，再把训练成果用于小队任务，在剧情推进中建立与人物的连接。本轮保留已有三个章节与多个结局，将现有战斗内容完整接回主线，再通过连续试玩和打包验收交付全内容可玩版。最新范围与顺序见[MVP方案](mvp-playable-plan.md)，不以缩减章节或提前结尾定义完成。

工程已进入完整内容整合与验收阶段。已有三章脚本主路径、训练成果部署、编队武器、资源结算、剧情返回和保存记录；正式Boss可玩性、全部既有结局、真实连续操作、视听与同版本稳定性仍需收口。最新冻结版本及实际回归状态只维护在[当前进度](progress.md)，各项证据注明版本与覆盖范围。网站未发布，整体尚未完成。

## 从哪里开始

| 文档 | 用途 |
| --- | --- |
| [全内容可玩版方案](mvp-playable-plan.md) | 本轮范围与执行顺序，覆盖三章、已有结局、战斗接入和交付门槛 |
| [战斗接入盘点](battle-integration-matrix.md) | 正式入口、资源/结算、剧情返回和具体运行证据 |
| [结局路径核对](ending-paths.md) | 已定位路径与其他分支的盘点缺口 |
| [当前开发进度](progress.md) | 首先阅读：当前任务、未解决问题、下一动作与退出条件 |
| [历史记录索引](progress-history.md) | 追溯历次实现与验证；不作为当前待办 |
| [敌人体系与Boss战补完](enemy-boss-iteration.md) | 未用素材、技能缺口、敌群与正式Boss交付 |
| [下一轮迭代方案](next-iteration.md) | 当前迭代范围、顺序、交付和验收门槛 |
| [来源与实现盘点](inventory.md) | 区分历史策划、代码、UI 原型和未验证的运行状态 |
| [首版范围与玩法细化](game-design.md) | 规定玩家循环、训练、战斗、成长及失败规则 |
| [剧情与内容计划](story-content.md) | 原剧情盘点与章节、任务和事件设计 |
| [技术与数据设计](technical-design.md) | 规定状态、数据、模块边界、训练模型和存档契约 |
| [开发路线与任务表](roadmap.md) | 历史里程碑与任务ID；当前全内容排期见MVP方案 |
| [当前验收核对](acceptance-current.md) | 当前证据、适用版本与剩余缺口 |
| [验收方案](acceptance.md) | 规定每一步的可玩、数据、视觉和恢复证据 |
| [决策与问题记录](decisions.md) | 记录提案、设计冲突和后续选择依据 |
| [辅助机模型与动画](auxiliary-machines.md) | 原素材、制作方式、九动作与真实冒险接入边界 |
| [狐狸带路与据点侦察](fox-trail.md) | 原2-13操作、持久化、重读与验证范围 |
| [指挥室归来与分工](command-assembly.md) | 原2-14集合、分工记录及恢复验收 |
| [九尾狐Q版动画](fox-animation.md) | 原作动作研究、关节约束与形象验收 |
| [工厂潜入](factory-infiltration.md) | 原2-15完整范围、守卫实战与待接入边界 |
| [音频接入与听验](audio-design.md) | 场景选曲、响度测量、播放归属和听验缺口 |

## 阅读与维护规则

当前任务状态统一维护在 `progress.md`，目标60行以内；每轮更新对应行，不追加长日志。详细过程另建阶段记录并加入历史索引，原始输出放游戏证据目录。方案说明范围与验收门槛，历史记录只说明当时事实。

- **历史设计**：保留原作者与原页面；不同方案不是同时生效的需求。
- **源码确认**：仅证明代码或资源存在，不能写成运行验收通过。
- **新增提案**：本目录的具体规则和参数，待原型验证后收敛。
- **待验证**：尚未取得对应运行、视觉或数据证据。
- **完成**：任务的交付和验收均通过，并在进度文档登记证据。

当前采用 `Dora/LSD` 为盘点基线；网站文档保存在 `github/LSD-doc`。`Dora/LSD_git` 和 `lsd-docs` 原有修改保持原样。目录绝对位置、基线提交和选择依据见盘点文档。

开发按里程碑验收，不把重置卡额度或固定日历日期作为完成标准。每轮形成可继续的版本、问题清单和下一项明确任务。

```{eval-rst}
.. toctree::
   :maxdepth: 1
   :caption: Game 0 开发文档

   progress
   round-closure-2026-10-09
   progress-evidence-2026-10-05
   progress-history
   battle-integration-matrix
   mvp-playable-plan
   ending-paths
   candidate-package
   single-package-journey-2026-10-07
   next-iteration
   resource-economy
   enemy-boss-iteration
   inventory
   game-design
   story-content
   chapter-adaptation
   chapter-three
   technical-design
   auxiliary-machines
   audio-design
   fox-trail
   fox-animation
   command-assembly
   factory-infiltration
   roadmap
   acceptance
   acceptance-current
   decisions
```

```{eval-rst}
.. toctree::
   :hidden:

   progress-log-2026-10-09-settlement-scroll
   progress-log-2026-10-09-learner-muzzle
```
