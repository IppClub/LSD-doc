# 来源与实现盘点

盘点日期：2026-10-03。下面所有“源码确认”结论仅针对本次本地文件快照，不代表运行通过。

## 1. 工作目录与基线

| 项目 | 本地位置 | 基线及状态 | 本轮用途 |
| --- | --- | --- | --- |
| 游戏主工程 | `/Users/Jin/Workspace/Dora/LSD` | `3dbaf75168d0a214815b2305f9fd74852ce5bb26`；盘点开始时 Git 工作区干净；配置了 github、gitee、gitcode 三个远程 | 游戏源码与资源基线，后续实现优先在此推进 |
| 游戏另一个副本 | `/Users/Jin/Workspace/Dora/LSD_git` | `79ed42f`；有多个二进制资产和 `Test/FigureTest` 修改 | 保留；本轮不同步或覆盖；对照确认 Script/UI/Data 中 `.lua/.yue/.tl/.xml/.ts/.tsx/.yarn` 与 LSD 无差异，不含 init、Test 和二进制比较 |
| 文档网站源码 | `/Users/Jin/Workspace/github/LSD-doc` | `f4e91b0fde1525e723d0f21301d12fc4a8556a2e`；盘点开始时 Git 工作区干净 | Sphinx + MyST；新增开发章节的正式位置 |
| 数据模型设计 | `/Users/Jin/Workspace/lsd-docs` | `6872743b369189af4fa6bf3f53cfe9f6308e8832`；`story.chnr.json` 已修改，另有三个未跟踪备份 | 只读参考；这是含实体关系图的数据建模文件，不是网站源码，也不是已经安装的游戏数据库 |

公开网站：[灵数奇缘项目白皮书](https://luv-sense-digital.readthedocs.io/zh-cn/latest/)。本轮打开了首页、项目描述、计划、玩法与剧本目录，随后以本地策划原文作详细分析。没有核验本地全部页面与线上内容逐字一致；线上展示也不代表程序已实现。

## 2. 策划来源索引

下表路径相对网站 `docs/source`。历史文档原文不改写；新增规则放在本开发章节。

| ID | 来源 | 可继承内容 | 需要细化或处理的差异 |
| --- | --- | --- | --- |
| S01 | [项目描述](../../gamedoc/project-description.md) | 2D 动作、示范训练、剧情养成、小队即时战术 | 是产品方向，不是逐条验收规格 |
| S02 | [长期计划](../../summary/plan.md) | 用现有资产做小体量 Game 0，包含三个章节 | 不将小切片误称三章完整作品 |
| S03 | [交互流程](../../gamedoc/gameplay/game0/ideas/gameplay-flow.md)及两张流程图 | 开场、建角、教程、基地、通讯、训练结算、采用模型、编队、战斗、回基地 | 图中线上账号、借调角色、维护费用等扩展需分期；五人编队不直接作为首个切片规模 |
| S04 | [采集设计](../../gamedoc/gameplay/game0/ideas/data-collection.md) | 自身/敌方状态、距离、动作构成训练输入 | 需限定可观测特征、采样时点、样本去重及数据版本 |
| S05 | [AI 训练想法](../../gamedoc/gameplay/game0/ideas/3-ml-thoughts.md) | 动作成功时采样；模仿效果、性格、协作的讨论 | 历史说明未采 idle/走路，并用默认追敌；连续动作、性格算法和迭代协作都仍需验证 |
| S06 | [战斗 Demo](../../gamedoc/gameplay/game0/ideas/demo-design.md) | 小规模、逐级增加单位数、训练到实战的验证方法 | 剑盾/大锤/弓箭与当前教程枪械动作不一致；其伤害、减伤、时间不是现行数值基线 |
| S07 | [战斗体验](../../gamedoc/gameplay/game0/ideas/battle-experience.md)、[方案 5](../../gamedoc/gameplay/game0/ideas/battle-experience5-detail.md)、[角色技能](../../gamedoc/gameplay/game0/ideas/char-skill.md) | 多种战斗方向、队员目标选择与临时调度、可配置技能 | 多套互斥方案，不能合并成一个无限扩张的首版需求 |
| S08 | [人物缺陷](../../gamedoc/gameplay/game0/ideas/cde.md)、[房间地图](../../gamedoc/gameplay/game0/ideas/room-map.md) | 成长与剧情结合；任务图、占领及触发 | 随机失误可能遮蔽学习效果；占领计时规则要与关卡目的匹配 |
| S09 | [玩法正式设计目录](../../gamedoc/gameplay/game0/design/index.md) | 目标、机制、技能、道具、挑战和失败的章节框架 | 六个子页面均仍为“待补充”；本轮细化稿见玩法文档 |
| S10 | [Game 0 设定](../../gamedoc/story-scripting/game0/game-settings.md)、[剧情梗概](../../gamedoc/story-scripting/game0/game-summary.md)、[主要人物](../../gamedoc/story-scripting/game0/main-character.md) | 世界层级、接触事件、人物动机、故事终点线索 | 角色名字在不同稿中不一致；完整梗概内容明显超过首个切片 |
| S11 | [对话剧本](../../gamedoc/story-scripting/game0/dialogue-script.md)、[开场 PV](../../gamedoc/story-scripting/game0/opening-pv.md) | 第一、二章对话及开场素材 | 第三章仅“待补充”；不能宣称已有完整结局剧本 |
| S12 | [版权与社区说明](../../community/licencing.md) | 代码与美术音乐有不同授权来源 | 发布包需保留原有来源和署名信息，不把代码 LICENSE 当作全部资产说明 |
| S13 | `lsd-docs/story.chnr.json` | Story、Conversation、Character、Mission、Paragraph、Answer、StoryProgress 等 11 个实体 | 数据模型需适配当前 Yarn 对话，不直接替换其文本或导入旧库 |
| S14 | `lsd-docs/battle.chnr.json` | Character、属性、装备、技能、Attack、Defects、Warehouse、TrainData 等 11 个实体 | TrainData 已有方向/距离/动作字段；没有证明运行时使用这些表 |

已查看两张交互流程图本身，包含训练成果“采用/放弃”、战术指令、队员视角及线上扩展。流程图不只有正文标题，后续设计需要保留它们的语义。

## 3. 实现与缺口矩阵

路径相对游戏工程根目录，除引擎能力一行外。

| 系统 | 本轮源码证据 | 判定 | 下一步 |
| --- | --- | --- | --- |
| 启动及配置 | `init.yue` 设置 Script/Spine/Image/Font 搜索路径；`Script/Start.yue` 挂载 `lsd.db`、加载配置后进入开场和教程 | 主流程入口存在；启动又直接设 `skipOP=0`、默认角色与姓名，恢复行为待验证 | 跑启动基线；检查“新建/继续/重置”的分离 |
| 开场与建角 | `Script/System/PlayOP.yue`、`Command.yue`、`UI/Story.yue`；支持姓名/角色命令、Yarn 对话 | 有实现；完整建角及开场视觉未验收 | 检查资源、输入、跳过与保存 |
| 教程战斗 | `Script/Tutorial/Level.yue`、`System.tl`、`Action.tsx`、`AI.yue`、9 个 `.yarn` 文件 | 有实体、动作、怪物、对话和事件；是固定 AI 与教学流程 | 实际走完移动、闪避、武器、击败怪物 |
| 教程到学院 | `Tutorial/System.tl` 末段在搭乘电梯后调用 `Academy.Level.Arrive` | 源码上有连接，不能当作已通关 | 验证条件与 UI/Entity 清理 |
| 学院与场景 | `Academy/Level/Arrive.yue`、`Academy/System.yue`、`Academy/Map.yue` 和 20 个 Scene `.yue` | 存在到达关、NPC、房间路线；地图默认解锁等级使用 `#states`，可能不等于剧情进度 | 明确解锁条件和每个交互用途 |
| 配置/存档 | `Data/Config.tl` 只有 skipOP、char、charName、heroine | 不能代表任务、训练模型、编队及章节存档 | 设计独立版本化存档及迁移 |
| 训练 | `UI/Training.xml`、`Test/TrainingTest.yue`；展示固定角色、属性和怪物，开始训练按钮未见对应训练业务处理 | UI 原型存在；本轮查阅的游戏业务代码未发现示范采集→训练模型→采用闭环 | 查遗留外部实现，再接首名学员训练 |
| NPC AI | `Tutorial/AI.yue`、`Academy/AI.yue` 手写条件树；学院 NPC 主要转向和 idle | 规则 AI 已存在，与学习生成模型不同 | 学习模型与底层合法动作/安全规则分离 |
| 编队与通讯 | `UI/Formation.xml` 支持原型选择显隐；`UI/Phone.xml` 有 Tab 切换和固定消息/任务文本 | 有交互 UI 原型，未证明与任务/角色持久数据连接 | 绑定任务、学员、技能与采用的模型版本 |
| 战役、结算、失败 | `UI/Settlement.xml`、`MissionFail.xml` 及对应 Test；学院 Level 目录只找到 Arrive | 界面存在，未发现完整战役控制链路；运行待验证 | 配置第一任务、胜负、重试、奖励和回基地 |
| 引擎 ML | Dora-SSR `Source/ML/ML.h/.cpp`，`Assets/Script/Lib/Dora/zh-Hans/Dora.d.ts` 的 `ML.BuildDecisionTreeAsync`、QLearner | 引擎接口存在，不等于 LSD 已接入 | 先验证 CSV→树节点→合法决策执行的最小链路 |

## 4. 文件和资产规模

按递归文件计数，排除 `.DS_Store`；生成 Lua 与源文件分别计数，不能将数量换算为完成率。

| 目录 | 文件数 | 构成 |
| --- | --- | --- |
| Script | 86 | 34 Yue、37 Lua、4 Teal、1 TS、1 TSX、9 Yarn |
| UI | 136 | 56 XML、66 Lua、9 Yue、3 Teal 声明、1 TS 声明、1 TSX |
| Spine | 256 | 85 atlas、85 PNG、86 skel（含子目录） |
| Image | 31 | 15 PNG、3 JPG、4 JSON、8 clip、1 model |
| Music | 13 | 12 MP3、1 OGG |
| Font | 4 | 2 OTF、2 TTF |
| Test | 24 | 12 Yue 原型测试入口及 12 Lua |

Spine 文件数不成完全一一匹配，需要逐资源检查 atlas 页引用、骨架兼容和动作存在性；目前没有逐项验收。已有 `charM/charF/ninilite`、饕餮、学院、训练场等候选素材，可优先复用。`Training.xml` 中的 `moyu` 只是显示原型，不能据此锁定首名可训练学员。

同名配对静态检查发现 `Spine/hualei.skel` 没有同目录同名 `.atlas/.png`。这是一项资产核查线索，不直接判定游戏启动失败：需确认它是否被引用、是否复用其他 atlas，以及是否属于当前首版必需资产。

Test 目录多为创建 UI 或场景的独立入口；本轮没有执行，不能称为自动化通过 12 项。

## 5. 已完成与未完成的盘点边界

已完成：定位四个相关目录；Git 基线与已有修改核对；读取关键策划、流程图、故事/战斗实体模型；追踪入口、教程转场、学院路线；检查关键 UI 原型；确认 ML 接口定义；记录初步资产规模。

待完成：当前 Dora 运行兼容性；所有资产引用；真实启动/教程/转场；训练闭环；主战役/故事终点；存档；各平台输入、性能与画面。盘点结果用于排任务，不能作为可玩或发布结论。

## 原怪物素材补充核对（2026-10-08）

桌面原美术目录新增定位八份可继续制作的分层PSD：大小穷奇、大小貔貅、工业区和其他地区大小赛博幽灵。层数41至97，原肢体/铠甲/武器/特效组件保留；这三个物种目录未找到Spine工程，原动作要求仍标为待提出需求。详见[敌人/Boss专项](enemy-boss-iteration.md)和游戏`Docs/evidence/2026-10-08/original-monster-layer-inventory`13文件来源证据。只能计为原素材定位，不能计为已经动画化、已接入或已实战通过。
