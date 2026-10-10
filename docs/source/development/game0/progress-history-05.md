# 开发历史记录 · 第 05 卷

> 2026-10-05 从旧进度页归档。以下为当时记录，含已被后续结果替代的状态，不作为当前待办。请从[当前进度](progress.md)或[历史索引](progress-history.md)继续阅读。

## 原始记录

<!-- preserved-progress-start -->
## 2026-10-04 佛陀 v3 关节注册与乘坐生命周期

新版图集按实际肩、肘、腕中心注册：上臂锚点 (278,473)/512×576，肘偏移 (4.5,-95.5)，前臂锚点 (226,430)/512×576，腕偏移 (7.5,-90.25)，左右肩根分别适配三分之四视图。候选参数集中于 `Test/BuddhaChibiStyle.lua`，生产默认图集不变。原生对照截图显示肘腕错位减少，但六臂根部遮挡及造型仍需视觉复核。

`Rescue/BuddhaCarrier.lua` 等自身调度进入后才启动有限动作，避免新场景首帧影响；等待原生完成事件及完整片长两者均满足才切换循环。支持 sit→ride→stand→idle，返回 idle 使用 recovery .2；重入返回 BUSY，移除节点后中止并返回 CLOSED。候选样式参数可传入，便于与同一玉资源验证。

旧测试将 recovery 与 .2 直接相等比较，实际原生读回 0.200000002980232，已改为浮点容差并报告落地状态。此次测试移除外部 .05 秒预热，直接创建后坐上；原生 1791093747 通过两轮移动护盾、坐上/落地（各约 .816 秒）、恢复原点/idle，以及中途移除和重入拒绝。落地图片中机器人消失、玉站回地面，乘坐图片仍需进一步检查裙摆接触。证据 `Docs/evidence/2026-10-04/yu-carrier-lifecycle-native.json`、`yu-carrier-riding-1.png`、`yu-carrier-landed.png`。这是独立组件测试，尚未接入真实救援关卡，不代替完整模拟游玩或最终美术验收。


## 2026-10-04 佛陀乘坐接入实际救援与出口死锁修复

`Rescue/Battle` 使用单一 BuddhaCarrier，取代战斗中的独立玉演员和 wardView。坐上完整播放后以原移动速度前进到 x=4650，护盾状态和受击脉冲绑定同一个机器人，结算前完成落地。正式资源位于 `Image/Rescue/buddha-guard-chibi.png`、`Spine/StoryActions/yu-riding.json`，无 Docs 运行依赖；来源和散列见游戏 `Docs/artwork/buddha-guard/runtime-carrier-manifest.json`。初次会面 Arrival 仍用旧表示，后续需统一。

首次真实救援测试 1791093902 揭示既有到达死锁：后一名双子在 1 像素到达容差内停止，前一名剩余 1.3506 像素却只剩 .4165 可用间距，低于 .5 起步门槛，敌人清空后仍超时。改为 .001 起步门槛，保留间距约束和速度上限。失败原始记录保存在 `Docs/evidence/2026-10-04/carrier-evacuation-spacing-failure.json`。

随后 `JourneyFreshTwinsEvacuation` 原生运行 1791094175 PASS：两段撤离 35.65 秒，双子终点 5399.064/5559.482，最低间距 160.4165，生命 100/48。sit 约 .810 秒、stand 约 .814 秒，均覆盖 .8 秒片长；结算后 carrier 为 ground，护盾 2 次吸收对应 2 次脉冲。位置门禁、非法证明拒绝、写入失败重试、幂等结算、队伍更新及返回研发室检查均通过，原有表保持。使用独立 QA 数据库，不修改用户主存档。

证据 `Docs/evidence/2026-10-04/carrier-rescue-route-native.json` 和 `carrier-battle-live.png`。测试由游戏内控制事件驱动，osInput=false，不能代替真实键鼠/触控测试。六臂最终视觉品质、会面与战斗的视觉统一、全流程 OS 游玩及其他 Game 0 验收项仍未完成。


## 2026-10-04 初次会面与战斗造型统一

研发室 `Rescue/Arrival` 改用与双子战斗相同的 BuddhaCarrier 和正式素材。未完成救援时玉在佛陀托掌上播放 ride 循环；已完成救援的读档返回保持 ground，玉站在支撑点，机器人透明度为 0。移除该场景旧的独立玉演员和 wardView，避免重复显示。初次会面的护盾有效范围与剧情门禁保持由原有逻辑负责。

原生 `JourneyFreshJadeArrival` 1791094408 PASS：从 PassageA 经 PassageC、PassageD 实际移动进入 RDRoom，障碍阻挡、12 行交谈、1.216 秒开通道、存档失败重试、重复阅读不写入、重新载入骑乘及循环均通过。截图发现菜单挡脸，随后将未救援时的菜单向左偏移 160；位置交互门禁不移动，最终截图待复核。

衔接上述新 QA 存档运行 `JourneyFreshTwinsEvacuation` 1791094500 PASS：完整战斗、结算和返回后 carrier 确认为 ground，机器人收起；护盾两次脉冲、保存重试及幂等检查通过。证据为游戏 `Docs/evidence/2026-10-04/carrier-arrival-route-native.json`、`carrier-arrival-return-native.json`、`carrier-arrival-restored.png`。仅游戏内控制事件模拟，尚不算 OS 操作验收；所有运行使用隔离 QA 数据库。

菜单最终复核：原生运行 1791094614 再次通过初次会面路线；`carrier-arrival-menu.png` 确认菜单在佛陀左侧，不再遮挡面部，`carrier-arrival-menu-native.json` 保留完整结果。此次仍为游戏内事件驱动，非 OS 点击验收。


## 2026-10-04 研发室实际键鼠交谈与键盘补齐

通过 CUA 原生鼠标点击左移后的「重读初次交谈」，确认命中正常。旧 UI.Story 仅绑定鼠标，实测 Return 无推进，已在 Yue 源及生成 Lua 中补充 Return/Space：每次按下只推进一次，KeyUp 解除防重复标志，隐藏或回顾状态忽略推进，选项/异步剧情仍由原 nextSentence 门禁负责。

加载新版后使用实际鼠标打开交谈，Return 从第一句进入玉的第二句、Space 进入第三句；打开回顾后两键均不推进，关闭回顾后继续正常。使用实际键盘完成全部 12 行重读并回到研发室。原生只读结果 1791095207 确认 phase=complete、rows=12、storyBusy=false、playerBusy=false，载具仍 riding。证据为游戏 `Docs/evidence/2026-10-04/jade-dialogue-os-input.json` 与 `jade-dialogue-os-complete.png`。此前更新后的路线回归 1791094949 通过。

此次 OS 覆盖仅此段重读交谈及回顾；没有声称首次通关、全章节键鼠流程、长按按键防连跳、窗口失焦时持有移动键等验收已完成。后两项仍需实际输入条件验证。


## 2026-10-04 审讯正式资源迁移后的原生复核

将 ResearcherActions 和 InterrogationContact 的读取路径从 Docs 导出目录改为正式 Spine/StoryActions；Choreography 本来通过 Factory.InterrogationActors 使用正式资源。新证据写入 2026-10-04，不覆盖 10-03 的历史图。安装检查确认六项原资源与正式副本及 manifest 相符。

原生结果：InterrogationChoreography 1791095326 PASS，男女主角各完成 coverReach、coverRelease、狐狸警告与击打；击打事件约 .333 秒、导师动作 .9 秒、研究员倒地 1.35 秒后进入 unconscious。InterrogationContact 1791095397 PASS，呼吸持握最大距离 2.2226，两个镜像/起始相位检查最大 2.2651、2.1587（角色局部坐标单位），均低于测试阈值 3。ResearcherActions 1791095470 PASS，12 个正反向时间切片，完整倒地 1.3667 秒，恢复参数 .15。

检查了男女主角组合终态、捂嘴持握和倒地中间帧图片。三份原始结果为游戏 `Docs/evidence/2026-10-04/interrogation-choreography-runtime.json`、`interrogation-contact-runtime.json`、`researcher-actions-runtime.json`。测试在离屏原生节点运行，不替换玩家当前场景，也不写入剧情进度；不能据此宣称实际关卡完整审讯或最终动画品质已全面验收。此前“迁移后尚未原生验证”这一具体缺口现已补齐。


## 2026-10-04 最新运行资源 staging-c 验证

新目录 `/private/tmp/lsd-game0-stage-20261004-c` 包含 874 文件、262622660 字节，排除 Docs/Test/Tools 和隐藏开发目录。874 个文件散列全部匹配，271 个 Lua 文件语法通过；86 atlas、89 页面、22 clip、399 裁剪矩形、11 model 的静态依赖/边界检查通过。

扩展 StagedContinue，在清空游戏模块和缓存、移除源项目搜索路径后，从隔离存档进入 stage 的标题继续游戏并抵达 PreparationRoom；随后仅从 stage 加载新版佛陀/玉，完成 sit→ride→stand→idle，并执行男女主角各一遍捂嘴、松手、狐狸警告、击打及倒地。1791095675 PASS，两个 .8 秒乘坐动作实际均约 .816 秒，正式审讯事件完整。运行搜索路径仅含 staging-c 和引擎公共 Script/Lib，开发资源不可见。

证据位于游戏 `Docs/evidence/2026-10-04/stage-c-native.json`、`stage-c-integrity.json`、`stage-c-atlases.json`、`stage-c-continue.png`。未捆绑引擎，也不是平台安装包；coldProcess=false，尚未证明冷进程启动、全流程打包游玩或其他平台通过。当前引擎保留 staging-c 的准备室与隔离存档，下一次测试清理时恢复原搜索路径和 writablePath。


## 2026-10-04 制作人员 v2 显示与片尾返回验收

使用实际鼠标从 9 页片尾记录逐页进入署名页，检查第 4 页长姓名列表、第 8 页「佛陀机器人部件：基于周大西设计，AI辅助制作」、第 9 页最终致谢，均完整显示。最终继续按钮关闭独立预览，原生读取确认 ending/credits 均已记录。该页面为分页形式，无滚动列表；OS 证据 `credits-v2-os.json`、`credits-v2-os.png`（游戏 Docs/evidence/2026-10-04 下）。

随后真实入口回归 JourneyFreshEndingFlow 1791096063 PASS：未看完不计完成、保存失败重试、返回标题、进入受损学院、终章重播、模态阻止底层退出、再次加载及不重复奖励均通过；原有表未改动。此回归为游戏内事件驱动，证据 `credits-v2-ending-flow.json`。

最后从真实 Ending.Hub records 入口用实际鼠标点击返回，画面显示 GAME 0 标题和继续旅程/重看终章/受损学院入口，原生确认 mode=title。证据 `credits-title-os.json` 与截图。全部使用隔离 QA 存档。本轮证明当前桌面尺寸下的署名和返回交互，不涵盖全章节 OS 通关、所有尺寸或其他平台。


## 2026-10-04 护盾型无人机工厂分支验证

新增 Test/FactoryDefenceRoute.lua，沿公开部署入口选择 defence，使用既有医疗 QA 存档的独立副本，完成实际探索、战斗和返回采集。原生运行 1791096346 PASS：两位学员沿用已训练模型，实际战斗 16.124 秒获胜；妮妮莉特生命 64、乌云 22，分别命中 8/6 次，均未使用后备决策。护盾机战斗末生命 100，消耗能量 27.5879，累计恢复 25.9614，采集序号 2。

探索能量消耗、探索状态带入战斗及胜利后延续、妮妮莉特伤势保留、奖励保存失败回滚与重试、材料采集及医疗提示、解锁仅一次、训练模型记录不变均通过。证据为游戏 Docs/evidence/2026-10-04/factory-defence-route-native.txt 和 factory-defence-live.png。测试由游戏内控制事件驱动，未改动用户主存档；不代表该分支已通过完整 OS 输入游玩。此前护盾型无人机工厂胜利分支的具体覆盖缺口已补齐。


## 2026-10-04 佛陀六臂接口与托臂姿态调整

原生对照发现旧肩根坐标未对应新版躯干的六个绘制接口。先尝试只移动肩根，虽改善连接位置，却拉开下方双掌；因此未将该中间方案用于正式场景。最终同时将上臂锚点改到连接轴端部 (291,501)/512×576、肘偏移改为 (-2.25,-101.25)，左右三组肩根分别对应躯干接口，并给下方左右托臂独立初始角度 -10/-1 度，保持双掌向内承托。

Rescue.BuddhaPrototype 支持可选逐侧肩角，旧默认不变；正式 BuddhaChibiStyle 使用修正坐标。已查看正常/镜像方向及待机/护盾截图，托掌随玉的位置计算保持工作。证据为游戏 Docs/evidence/2026-10-04/yu-buddha-shoulder-fit-guard.png、yu-buddha-shoulder-mirror-guard.png 及对应 native.json。图像检查不等同于全部动画帧视觉验收，接口边缘和裙摆接触仍保留最终美术验收项。

正式资源生命周期测试 1791096975 PASS：两轮坐上/移动/落地均完整播放约 .816 秒，落地 rider 回到 (0,0)、ground 状态、recovery .2，重入拒绝和中途移除取消通过。证据 yu-carrier-shoulder-lifecycle-native.json。旧 staging-c 仍保存调整前参数，不能据旧包验收证明本次参数已验证。

实际救援路线复核 1791097022 PASS：35.759 秒完成两段撤离，护盾吸收两次并对应两次闪光；玉 sit/stand 分别约 .810/.814 秒，结算 ground、返回后机器人收起。保存失败重试、幂等结算与旧表保留通过。已查看 shoulder-rescue-battle.png，调整后骑乘中的玉双脚仍在地面上方；完整数据 shoulder-rescue-route-native.json。该轮仍为游戏内控制事件，非 OS 全流程游玩。


## 2026-10-04 男主角开局实际游玩及左方向教学修复

新增 OpeningOS 隔离入口，只创建空白存档目录和正式标题，不代填姓名、性别、进度或派发操作。实际鼠标开始新旅程、输入 JourneyOS、选择男、完整播放片头，再用 Return 和鼠标完成首次会面及道具选项。1791097165 只读观察确认 charM、skipOP=1、进入 LoopTowerA，原始记录 opening-male-os-initial.json。尚未完成教程和学院到达。

实际轻按 A、拖动和点击左摇杆未推进闪避教学，而 D 能推进。原因是 Tutorial.Level 左方向使用 Observer Add，HUD 已先初始化 keyLeft=false，后续 true 属于变更；右方向本来使用 AddOrChange。现将 Yue 源及对应 Lua 左方向统一为 AddOrChange，保留其余教学行为。生成 Lua 与新编译结果去除注释后逐行一致，并保留原文件行号注释以避免无关差异。

TutorialLeftOS 1791097765 使用独立女主 QA 存档、自动推进会面，仅在确认 keyLeft=false 且教学已就绪后等待真实输入。通过 CUA 实际轻按 A，画面出现左闪避回应“好的。”，随后触发 Tutorial.Weapon，结果 PASS；证据 tutorial-left-os-native.txt。该检查的前置对话自动化，只有左方向操作是真实 OS 输入，不能合并宣称完整开局 OS 通关。男女完整流程、左摇杆修复后单独复核及学院到达继续待验收。


## 2026-10-04 教程射击、实际出口与标题继续

沿 TutorialLeftOS 女主 QA 场景继续游玩，实际 J 射击命中并触发武器说明，随后敌人死亡、妮妮莉特引导前往学院。实际点击摇杆右侧的原生事件记录含 Right=true/false，键盘记录含 KeyDown D，证明命中和输入已到达；短点击的位移很小，不以静态镜头判断输入失效。

长距离移动采用 HUD Right 持续事件，从 x=791.615 行走至 x=6222.832 的实际电梯交互范围，没有传送。之后通过 CUA 鼠标点击“搭乘”，进入 PreparationRoom，玩家可操作、学院导航已加载、tutorialCompleted 数据库值为 1。结果 tutorial-hybrid-academy.json（runId 1791098104），osInputOnly=false：前置对话和持续行走自动化、闪避和射击及出口由原生输入完成。

将刚完成的 QA 存档复制到新隔离存档目录，TutorialContinueOS 仅打开正式标题，实际鼠标点击“继续旅程”。1791098318 PASS，直接回到可操作学院，StarRiver/charF 身份保持；证据 tutorial-continue-os.json 和截图。不是冷进程启动，也未完成男主角后续或三章节连续键鼠流程。用户主存档未触及。


## 2026-10-04 学院新手交谈与训练经历一致性

在刚完成教程且尚无采用成果的学院存档中，实际点击妮妮莉特“对话”，原台词却声称此前一起训练并要求查看已采用成果。Academy.Companion 现优先保留学院受损后的专属对话；正常学院读取妮妮莉特自己的训练档案，没有有效采用成果时使用 companion-ninilite-first-training.yarn，有成果时保持原复盘对话。新台词先提示查看通讯安排，再说明备战室右门→B区→右门训练室及其中的虚拟训练场入口，不虚构过去训练经历。

使用实际鼠标重开同一新手存档的交谈，Return 逐句完成四行，路线文本完整显示并返回漫游。证据 companion-first-training-os.json/png；运行路径实际选择新文件，adopted=false。随后 AcademyCompanion 1791098711 PASS：真实六条示范的已有训练存档仍选择原复盘文件，人物资料、路线和返回操作正常，训练记录与剧情节点数量未改变；证据 companion-trained-followup-native.txt。测试使用隔离 QA 存档，新手段为 OS 输入，已有成果段为游戏事件驱动。受损学院分支本轮未重跑，未据此宣称全部学院流程验收完成。


### 学院训练入口原生点击复核（2026-10-04）

academy-training-hybrid-os runId=1791099195 PASS：沿备战室→B区走廊→训练室→虚拟训练场实际经过对应场景；房门和发光终端均由原生鼠标点击。虚拟训练场实际点击统一等待技能，样本从0增至1；旧成果仍显示6条已保存。原生点击返回训练室后，训练专用HUD与控制面板均已清理，重新读取采用成果仍为6条。路线与game-design中学院漫游入口设计一致。

这是混合输入验证：长距离移动通过既有HUD的Right事件驱动，没有传送；门、终端、等待技能、返回为原生点击。使用隔离的lsd-companion-qa-1791098711.db，不是主存档，也没有在本轮重做建模、三场试战或采用。证据位于游戏Docs/evidence/2026-10-04/academy-training-hybrid-os.json及同名PNG。


### 真实存储权限故障与原生重试（2026-10-04）

SaveStorageFailure runId=1791099365 PASS：从真实已通关QA库复制独立目录，目录权限置0555（进程用户501），未替换数据库API或模拟备份返回值。原生点击标题“继续旅程”，实际VACUUM备份失败返回BACKUP_FAILED；未留下打开的lsd连接、备份数仍为0，原库逐字节和SHA-256、旧选择记录均保持。恢复仅该测试目录至0755后，再次原生点击同一按钮，成功打开该库、生成1份备份并保存选择。测试结束已关闭该库连接。

标题页增加备份失败、恢复写入失败、选择写入失败、选择记录不可读的对应提示，说明检查存储状态、空间或权限及可重试；本轮运行时直接覆盖的是BACKUP_FAILED提示。Lua语法检查通过，真实原生画面文字完整。证据Docs/evidence/2026-10-04/save-storage-readonly-native.json与save-storage-readonly-error.png，专项入口Test/SaveStorageFailure.lua及Test/storage-failure-fixture.json。测试只验读档边界和失败重试，onOpen回调截断后续入场；不据此宣称冷启动或完整继续旅程通过。真实磁盘耗尽、游戏内写入中断、备份容量策略仍未验收。主存档未操作。


### 最新运行资源隔离与冷进程继续（2026-10-04）

新建/private/tmp/lsd-game0-stage-20261004-d，875文件/262624085字节，包含最近佛陀肩位、新手交谈、左方向教学、存储错误提示7个变化文件。875项SHA-256及271份Lua语法全部通过；86图集/89页面、22clip/399矩形、11模型引用检查通过。静态证据runtime-stage-d-static.json、runtime-stage-d-atlases.json及runtime-stage-d-changes.json。暂存中不含Docs/Test/Tools，新增交谈Yarn的运行路径也被显式验证。

StagedContinue 1791099585 PASS：同进程隔离搜索路径下继续至学院、玉上下托掌和两性别审讯动作通过。随后正常退出旧原生进程73986，并由进程查询确认不存在，再用debug引擎cli doctor --fix启动82077。新进程首个游戏入口StagedColdContinue（1791099681）仅从stage-d加载运行资源，复制既有真实教程通关QA存档至/private/tmp/lsd-stage-save-1791099681/lsd.db；原生鼠标点击继续，恢复PreparationRoom与可操作人物/导航，JourneyQA/charF/skipOP保持。新进程再次完成玉sit/stand及两性别cover/release/warn/slap生命周期检查。

冷进程证据staged-cold-continue-d-native.json附退出/新PID观察，staged-cold-continue-d.png为恢复画面。测试原始结果保留coldProcess=false及requiresExternalProcessEvidence=true，归档加入本轮外部进程证据后才标记冷进程成立。只有继续按钮为原生输入，动画检查由测试调用；本轮不包含全流程OS操作。该目录未捆绑引擎，不是安装包或发布产物；直接双击安装包、完整通关、多平台验收继续保持未完成。用户主存档未使用。


### 训练界面紧凑窗口验证（2026-10-04）

TrainingCompactLayout 1791100055 PASS：回放此前真实试战对照数据，实际调整原生窗口为640×360与480×320（Retina渲染分别1280×720与960×640）。12个管理按钮全部位于画面内，已查看两种比例截图，状态、操作说明、三行对照与技能图标未裁切。480×320窗口实际鼠标点击返回训练室成功，训练面板清理。完成后恢复原896×568窗口。

本轮前两次测试的边界计算错误地直接使用居中UI世界坐标，导致断言失败；补入半屏坐标偏移，并改为普通循环避免原生each回调吞掉断言后才通过。未因此修改生产布局。这里是历史数据视觉回放，不是新试战胜利证据，也不等同真实低DPI屏幕、触屏、手柄或全部UI验收。证据training-compact-layout-native.json、training-compact-640x360.png、training-compact-480x320.png。


### 初始任务目标随训练记录推进（2026-10-04）

此前Story.Service在警戒任务前统一要求“先进入训练室采用成果”，即使已采用也不改变。现读取妮妮莉特训练记录：未采用时提示备战室右门→B区右门→终端、示范/三场试战/采用；已采用时提示A区电梯→C区右门→指挥室中央终端与编队。读取失败单独提示检查记录状态，不将错误当作尚未训练。后续剧情分支优先级保持。

InitialObjective 1791100324 PASS：独立空白QA库验证未训练分支，再从已有训练QA复制真实成果到该库验证已采用分支；模型表保持、无剧情或任务奖励。实际打开学院日志并查看新目标换行和布局，截图initial-objective-journal.png，报告initial-objective-native.json。本轮是明确构造阶段的目标/UI检查，没有宣称重新完成训练。StoryService原任务/房间门槛、远程重读、原子回滚、幂等和后续目标回归通过，见initial-objective-story-regression.txt。stage-d早于这次提示修改，不能作为这项修改的打包验证。


### 男主角实际建角存档完成教程（2026-10-04）

从opening-male-os-initial.json记录的JourneyOS/charM真实建角存档复制隔离继续档，未注入教程完成或覆盖身份。实际点击标题继续、Return推进首次会面、点击幽兰草印章选项、完成全部交谈。实际点击左摇杆后出现“好的”并解锁射击按钮，补齐左摇杆修复后的鼠标证据。枪械按钮和J均实际开火；数次射击错过眩晕窗口，只扣普通生命，读取轨迹确认命中而非男主角伤害故障。随后覆盖完整协同攻击周期的J输入成功击倒怪物并出现跟随对话。

长距离行走通过现有HUD Right事件驱动（不传送），到达可交互电梯后实际点击“搭乘”。male-tutorial-hybrid-academy.json PASS：进入可操作PreparationRoom、导航已附加、JourneyOS/charM保持，tutorialCompleted在运行时和只读SQLite查询均为1。图像male-tutorial-hybrid-academy.png。属于混合输入教程通关，与前次建角证据衔接；不是三章连续OS试玩、冷启动或所有男主角战斗验收。未修改用户主存档，也未因操作时机问题修改战斗规则。


### 佛陀与玉的 Q 版风格重新对照（2026-10-04）

重新读取桌面 `LSD/Q版 玉.png`、`LSD美术/设计/角色设计稿/新人设/玉 v3.png` 与 `玉 v3 佛陀.png`。风格以 Q 版原图为准：暖橙金、奶白、蓝紫暗部、简洁色块与较粗轮廓；佛陀保留六臂与机械佛冠，但需要更明显的大头小躯干关系。

内置 image_gen 生成 v4 并保存 `Docs/artwork/buddha-guard-chibi-v4.png`；完整提示与两次编辑记录在 `Docs/artwork/buddha-guard/chibi-v4-generation.json`。首次输出躯干和光环越过图集分格，未接入；第二次修正后六格边界无 alpha>128 的不透明像素穿越，详见 chibi-v4-atlas-check.json。这是裁切边界检查，不代表所有透明残影或接点都通过。

`Test/YuBuddhaStyleV4.lua` 原生引擎 runId=1791101687 成功加载并产生待机/防御并排截图 `yu-buddha-style-v4.png` 与 `yu-buddha-style-v4-guard.png`。肉眼复核发现色块简化有效，但缩入分格后头部放大幅度不足，下方两臂连接仍需校准。候选不替换正式资源，视觉验收保持未通过；报告 PASS 仅指比较场景运行成功。下一步应分离头部与躯干以独立调整比例，重新对齐实际肩根，再检查左右朝向、托举接触和 recovery。


### 佛陀 V5 独立头身与实际救援接入（2026-10-04）

内置 image_gen 根据 v4 分离头部和无头躯干，保存 `Docs/artwork/buddha-guard-head-torso-v5.png`。实际输出1254×1254，运行时按真实627像素分界读取；头身分界无 alpha>128 的像素穿越。完整提示/来源见 chibi-v5-generation.json，资源哈希与边界检查见 chibi-v5-asset-check.json。

BuddhaPrototype 支持可选独立头部/躯干贴图矩形、锚点、缩放及层次；旧式调用仍使用原图集。正式 BuddhaChibiStyle 改用 v5 头身、v4 简化色块的手臂，头部和躯干独立缩放为0.38，降低头部位置以收短双重颈环，六臂根节点按新插口重新定位。原 v3 图集保留，测试对照固定到 V3Baseline，避免正式切换后对照组随之改变。Arrival/Battle 继续通过原 Carrier 使用新版，不更改保护场数值或技能行为。

原生并排比较1791101998、镜像检查1791102164生成待机/防御截图并已查看；头相对胸肩明显增大、暗部与玉采用类似蓝紫色，但最终美术验收仍未通过用户确认。YuCarrierV5Lifecycle 1791102101 PASS：两轮坐上/站起均约0.816秒，完整播放、落地归零、recovery=0.2、重复进入拒绝和清理中断通过。BuddhaV5RescueRoute 1791102218 PASS：真实救援战斗35.77秒、两次保护场命中反馈、乘坐与落地完整、结束机器人隐藏、写失败重试及幂等验证通过。实际画面 buddha-v5-rescue-battle.png；报告 buddha-v5-rescue-route-native.json。本轮战斗使用引擎事件驱动，不计OS全程操作验证。仍需全流程美术统一和最新发行包验证，不将候选接入或数值PASS等同Game 0整体完成。


### 男主角最新版本接续训练、首任务与调查（2026-10-04）

从 male-tutorial-hybrid-academy 记录的 JourneyOS/charM 教程完成档复制隔离数据库。首次测试误把已创建但为空的 Game0Training 表当作已有训练，读取源表确认零行后修正测试断言；没有修改源存档。MaleAcademyCurrent 1791102682 PASS：物理漫游到训练室、6条公开HUD示范、原生建树、候选三场3/3、采用存盘、通过学院房门到指挥室、导师HUD移动与射击、学员模型参战并赢得警戒任务、返回指挥室。只读数据库复核sampleCount=6、唯一任务尝试won、library-lead解锁。未导入模型或插入胜利。

MaleStoryCurrent 1791102901接续前段真实成果副本，PASS：准备室→研发室→邮件→资料室暗格→站台简报→C区；姓名性别保持，模型恢复，四个剧情节点与原任务胜利保留，重读没有重复记录。此次删除旧回归中的故障注入分支，以正常玩家流程推进，没有注入存盘失败。已查看运行画面并保存male-story-current.png。证据male-academy-current-native.txt/save.json、male-story-current-native.txt/save.json。

本轮通过现有HUD/门/按钮事件驱动连续路线，不传送，不计OS全程试玩；此前真实开场与教程通过复制的来源档接续，也不是从开场到站台的一次不间断进程。本轮覆盖第一章出发准备，列车、地面与后两章仍需在这条最新版本链路继续。


### 男主角接续列车、地面救援与第一章收束（2026-10-04）

MaleCurrentTrain 1791103125从前段male-story-current真实成果副本继续：实际学院房门→站台登车位置→TrainA，李叶娜实体、争执Yarn、第二封邮件与页码恢复、登车距离门槛和返回站台落点通过。移除旧测试中的故障注入及直接Service重读调用，保持正常玩家路径。

MaleCurrentGround 1791103195接续该列车档，通过真实编队按钮测试未编队不可出征，再进入废弃城市，物理拾取、剧情/日志暂停资源消耗、探索辅助机消耗带入战斗、导师移动射击与集合、乌云实际支援均通过。真实战斗12.59秒、学员8次命中/8次模型动作、fallback=0、导师1次命中、乌云2次命中及4段完整动作。六样本模型保持，救援结果正常保存，随后救援剧情→休息室→询问乌云，记录chapter-one-complete。

已在原生窗口观察最终休息室三人和交谈入口；保存male-current-ground.png及两个阶段native.txt/save.json。数据库只读复核JourneyOS/charM保持，剧情节点与任务解锁来自上述流程；未注入胜利或保存失败。两段均由现有HUD与交互事件驱动，并非OS全程操作；源档接续在隔离副本中完成，不称一次不间断新建通关。第一章当前链路已到收束，后续第二/三章与最终包仍需继续验收。


### 男主角第二章会面与乌云公开训练（2026-10-04）

MaleCurrentCooperation 1791103434 PASS：从本轮第一章真实成果副本开始，学院房门到休息室、来访者实体与原立绘对话、地面计划门槛、夜光镜一次解锁、日志重读、地图地点切换与关闭通过；妮妮莉特模型保持。此正常路线移除保存故障注入。随后通过CUA真实鼠标点击夜光镜打开、关闭并观察页面；这两个操作可单独计OS输入，主路线仍为引擎交互事件。

MaleCurrentWuyunTraining 1791103557 PASS：接续会面副本，物理进入训练室并公开切换乌云，近战/射击/接近各6条，共18条成功采样；每次刀击约0.400秒命中、1.000秒完成并回prepare。额外6次前摇期间射击请求被拒，属于动作保护检查，不是训练示范。候选学习规则在不同距离选择三种动作；候选/基础AI各三场3/3、平均生命93.33、fallback=0。候选平均5.996秒、基础6.544秒；候选16次模型动作中近战5、射击10、接近1。仅此固定对照不能推广为全面优于基础AI。

公开采用、切换学员重载、返回训练室通过；只读SQLite确认妮妮莉特6样本与乌云18样本分别保存，原妮妮莉特表逐字节保持。未导入模型、预设胜利或注入保存失败。证据male-current-cooperation-native.txt、male-current-wuyun-training-native.txt、male-current-wuyun-save.json。后续能源任务应从male-current-wuyun-training-resume-fixture继续，不能使用旧女主角档替代当前男主角链路。


### 男主角能源任务与阶段提示纠错（2026-10-04）

MaleCurrentEnergy先以1791103789通过实际任务，在CUA结束画面发现能源已回收但探索状态栏仍要求继续向右找能源箱。修正Ground.EnergySite：进入场景从已保存事实读取secured/recovered，回收对话结束后仅在实际完成记录存在时更新recovered；Ground.Expedition按清理伏击、收取能源、返回学院报告三阶段显示提示，不逐帧查询数据库。

修复后1791103987重新沿当前男主角双学员训练成果副本跑公开编队、物理城市路线、夜光镜定位、三敌战斗、结果返回、拾取能源、回收对话及日志。三个阶段提示分别断言并原生观察最终向左返回提示。真实战斗13.17秒，妮妮莉特/乌云各5次模型动作与5次命中、fallback均0，导师12次命中；模型表未改，辅助机状态带回探索，实际回收记录与唯一解锁由只读SQLite复核。

证据male-current-energy-native.txt、male-current-energy-save.json、male-current-energy.png。全程为HUD/按钮事件驱动，无胜利或模型夹具，无保存故障注入；不计全程OS输入。下一段使用male-current-energy-resume-fixture继续报告与阿焰线。本次修改尚未重新打包。


### 男主角阿焰带路与李叶娜协作/切磋接续（2026-10-04）

MaleCurrentAyan 1791104214从当前能源任务成果副本继续，经实际学院房门到训练室。远程会面与日志代替首次发现被拒；实际靠近后完整播放会面11行、绕路9行、参观14行，姓名插值为JourneyOS。阿焰实际行走超过1500，跟随/纠错后解锁李叶娜邀请；两位已采用模型保持，随后原训练入口可进入且带路UI清理。

MaleCurrentLiyena 1791104302接续该成果：真实训练终端→协作战→挑战对话→切磋→认可对话→训练室。两场开始前均等待玩家准备，双方真实命中；正常完成动作时长与攻击释放帧逐条检查通过，未完成动作必须记录中断原因。合作15.02秒、李叶娜9次命中；切磋男主角20次命中并以52生命获胜。Yarn挑战4行/认可5行完整，唯一认可记录和两个任务解锁保存，活动任务归零、两学员模型与能源奖励保持。

本轮移除旧回归中的保存故障注入和直接Service重放调用；操作仍由原HUD/交互事件驱动，不计OS全程试玩。原生窗口观察了切磋中的男主角姿态，保存male-current-ayan.png、male-current-liyena.png、两个native.txt及liyena-save.json。后续从male-current-liyena-resume-fixture接第三封邮件、阿焰餐点与记忆片段，再进入医务室和翻译器准备线，未宣称第二章整体通关。


### 男主角第三封邮件、餐点与医务室接续（2026-10-04）

MaleCurrentAfterTrial 1791104522 PASS：从李叶娜认可成果副本继续，第三封邮件明确阅读和转发后才开放餐点，实际角色面前交付、记忆片段首次现场解锁、人物故事重读、隐藏真相不提前披露、五项唯一解锁与物理到达休息室通过。两名学员已采用模型及能源奖励保持，未注入存档错误。报告 male-current-aftertrial-native.txt，画面及只读数据库快照同前缀。

MaleCurrentMedical 首轮1791104811 PASS：学院漫游到诊疗区，医师35行对话、林睿哲3行材料委托、两位同伴15行行动准备完整，包含原策划的主攻西医、三顾茅庐、砗磲贝、沼泽、废弃工厂和牵挂。首次远程解锁被拒，已读医师剧情可从日志重播；角色不重复生成，三项解锁各一次，姓名JourneyOS/charM与模型保持。复核原策划 dialogue-script.md 466、475、487、513附近文本。截图发现准备完成后仍提示确认行动，随后修正学院导航，等待本轮复测结果记录。

MaleCurrentFactory 首轮1791104912 PASS：从医务准备真实成果副本，实际学院房门→列车→工厂，选择机动辅助机、夜光镜定位、沿场景行走、塞壬对话、三敌实战16.27秒、歌谣两次完整释放并解惑。妮妮莉特9次命中、乌云6次命中，两模型fallback=0，导师12次命中。辅助机燃料及采集账目跨战斗保持，妮妮莉特毒伤未被维生场抹除；实际采集砗磲贝、通知医师与唯一奖励通过。结束画面也发现工厂导航仍要求清怪采集，已与医务提示一起修正，待复测。上述路线均为引擎HUD/交互事件驱动，非完整OS输入或一次不间断三章通关。


导航修正的医务复测1791105030 PASS：完成15行行动准备后，画面实时改为“行动准备已记录……废弃工厂的砗磲贝”，不再要求重复确认；male-current-medical.png已重新生成并查看。导航在场景创建与Story.Recorded时读取已保存的剧情目标，未逐帧查询存档。工厂同样按已记录剧情更新目标，等待最新整段复测。


工厂导航首轮复测1791105136通过，但CUA发现下方生命/燃料状态面板还有独立旧文案。进一步修改Factory.Expedition：场景初始化和Story.Recorded后缓存已保存目标；采集后优先下一步任务而非旧夜光镜路标，清除过期提示，不逐帧查询数据库。最新整段复测1791105274 PASS，两块面板均断言已通知医师与返回列车，CUA实际画面一致。报告male-current-factory-native.txt及只读数据库male-current-factory-save.json，截图male-current-factory.png。当前男性链路已到采材并通知医师，下一段返院治疗与遗迹出发；MaleCurrentRecovery.lua已准备且语法通过，尚未运行。最新修改尚未打包，完整三章与最终验收继续保持开放。


### 男主角返院治疗、翌日恢复与遗迹集合（2026-10-04）

MaleCurrentRecovery 1791105418 PASS：来源为最新工厂实际胜利与采材通知成果副本1791105274，未导入胜利或注入写失败。正常Start恢复到备战室后，经学院房门进入休息室；18行治疗原文、两名医师原comp动作完整并带recovery，医师各自实际步行离开。治疗后生命仍保持毒伤值；明确选择休息至翌日后全队恢复100，辅助机维生上限随康复解除（构造器隔离检查与实际存档阶段检查分别进行）。

林睿哲7行消息明确点击后，三名角色各获止伤水与贴药各一份，共6行；重读不重复领取。7行调查准备→实际学院路线到站台→10行集合讨论通过，五项剧情奖励各一次，两位已采用模型保持。只读SQLite确认charM与6份物资，证据male-current-recovery-native.txt/save.json/png。原策划dialogue-script.md 552–578附近的花妖毒素、草原民族奇闻、次日恢复和阿岩失踪委托逐项对应。路线为游戏HUD与按钮事件驱动，非整段OS输入，开始恢复到备战室不等同物理返程列车全程。


### 男主角遗迹搜救与返程掩护复测（2026-10-04）

MaleCurrentRuins从本轮恢复/站台成果副本继续，不注入保存故障。首轮1791105512在返程掩护烟雾等待超时：测试在toolAnimations.flare计数增加后立即输入烟雾，而pursuitTool动作仍未退出，实际界面出现ACTION_BUSY。保留生产动作保护和完整动画，修正测试等待实际isDoing结束；旧JourneyFreshRuins同处等待也同步修正，旧女主路线尚未重跑。

同时改进PursuitLevel道具按钮反馈：前一动作未结束、冷却和无需用药分别使用中文说明，成功操作清除过期提示。新测试主动在火光动作中请求烟雾，验证不打断动作且显示明确中文；随后等待完整动作退出再使用烟雾，并验证旧提示清除。新一轮实际路线正在复测，不能将此前已到达追击战视为通关。


复测1791105671 PASS：41行双胞胎会面含真实投射物与护盾阻挡、完整动作；双胞胎各实际步行护送超过1000；7行发现阿岩、7行人物日记和8行数据回收完整，回收流至少1.39秒后移除遗体。继而同次运行进入5行返程遇袭与真实掩护战20.75秒，导师69生命、射击/火光各1命中、烟雾阻断1次、烟雾/火光各1次完整动作、三个路线检查点和四人撤离通过。主动过早道具输入被保护拒绝、中文反馈及成功后清除通过。六份物资与已采用模型保持，任务奖励唯一；只读数据库复核charM及ruins-diversion-complete。

原生结算画面已查看，再以CUA真实鼠标点击“继续旅程”，当前场景确认为OuterHeaven、valleyVisit有效、男主角保持，并实际显示吊床与万薇莉。此单次转场计OS输入，前段仍为游戏HUD事件。证据male-current-ruins-native.txt、male-current-pursuit-report.json、male-current-ruins-save.json、male-current-ruins.png、male-current-valley-os-entry.json/png。下一步接桃源谷剧情及后续第三章；现有吊床/日记等原型美术与整体最终美术验收仍有待完善，不将路线通过视为高质量最终交付。用户主存档未触及，最新修改未进入最终包。


### 男主角桃源谷苏醒与五项活动（2026-10-04）

MaleCurrentValley 1791105964从当前掩护胜利成果副本继续，Start实际恢复OuterHeaven；32行苏醒/相识对话、饮水/喂食完整动作、骑行、友善怪物安抚、花瓣环境启动通过。逃离的学员未错误出现在谷中，日志重读不重复实体演出，valley-met只解锁一次。音乐与环境声仅证实已启动，未作为听觉混音验收。

原生画面发现活动白字叠在明亮天空上、顶部仍要求首次会面。为ValleyActivities说明增加半透明底板，与现有导航配色保持一致；Navigation在谷中已相识后使用已保存的剧情目标。MaleCurrentValleyActivities 1791106068 PASS：从该成果副本实际走到五个活动地点，定时钓鱼、播种/浇水/等待生长/收获、赏花观察、追鸡和静心语言答题通过。错误回答不奖励，完整动作检查、五项奖励各一次、万薇莉实际跟随到8000以外和重新进场恢复通过。只读SQLite确认charM与五条奖励，报告和数据库快照为male-current-valley及male-current-valley-activities前缀。

活动画面进一步发现桃树遮住角色头部，调整桃树到-10层（人物层约-2至2），保留鱼塘/作物等其它道具层次。下一段MaleCurrentValleyDays加入实际走到桃林的截图与树层断言，再返回吊床继续休息和狐狸登场。本轮仍为HUD与交互事件驱动，未注入保存失败，用户主存档未改；道具原型美术尚未完成高质量替换。


MaleCurrentValleyDays 1791106206 PASS：从五活动真实成果副本，实际走到桃林检查层次并截图，人物头身完整显示在桃树前方；返回吊床后完整睡眠/醒来、数日练习门槛和24行后续对话通过。怪物/大狐狸/万薇莉原说话者保持；Q版Spine狐狸实际走入超过450距离，停下恢复idle、recovery=0.2，日志重读不重复休息和登场。只读数据库确认fox-route-offered唯一与charM保持。已查看male-current-valley-peach-layer.png和male-current-valley-days.png，后者顶部已更新为跟随狐狸调查断网组织。报告和存档快照同male-current-valley-days前缀。下一段从male-current-valley-days-resume-fixture接狐狸侦察路线；当前修改尚未重新打包，旧原型素材和完整设备/布局/混音验收仍开放。


### 男主角狐狸侦察：可操作过场输入修复（2026-10-04）

MaleCurrentFoxTrail从当前男主桃源谷成果副本继续。首轮1791106398在fox-trail-return的walk-open阶段停在x=4083.35，无法走到4500；实际运行状态确认player.busy=false但keyRight被清掉。FoxTrail只隐藏了对话view，未发Story.Display恢复整套HUD，InputAvailability因父HUD隐藏而清除输入。修正可操作走路命令：先显示既有HUD，再解除冻结；走到开阔处后重新冻结并恢复对话显示。保留原摇杆与输入可用性保护，没有直接设位置或修改移动速度。

复测加入HUD及摇杆可见断言、完整食物动作时长断言，并保存狐狸AnimationEnd时间序列、各段实际移动日志与夜光镜扫描时长。本段正常路径移除旧测试的保存失败注入，模型与胜利均来自此前真实成果副本；尚待最终结果。


修复后MaleCurrentFoxTrail 1791106622 PASS：原有HUD在walk-open阶段可见并可控制，三人实际走到开阔处，再正常返回OperationRoom。狐狸AnimationEnd间隔约1.17–1.18秒（0.85动画速度），第二段实际行走7.50秒，食物动作1.80秒、扫描3.02秒、开阔处步行2.00秒。万薇莉实际从后方走入而非直接出现；22行剧情及跨场景日志重播保持，食物只扣一次，医疗物资不变。日志与截图见male-current-fox-trail-motion.json、native.txt、save.json、png。

MaleCurrentCommand 1791106707 PASS：从上述成果副本恢复指挥室，9位原角色及Q版狐狸齐全；实际走近中央，汇报前分工拒绝，28行原剧情与说话者对应，10项职责保存。四组手机分工说明、日志重读不重复写入、旧编队入口及返回通过，训练/物资/食物/任务表保持。只读数据库10项职责，证据male-current-command-native.txt/save.json/png。CUA返回画面发现人物落点与林睿哲重叠，顶部仍显示首次汇报提示；这两项体验问题需在下一段前修正，当前报告PASS仅覆盖现有流程断言，不代表该画面质量通过。下一段从male-current-command-assembly-resume-fixture继续工厂潜入。


### 指挥室编队返回修正与男主潜入（2026-10-04）

Navigation只针对已进入狐狸归队阶段、从missionBriefing返回指挥室的情况，将玩家落点从中央+280改为中央空位；避免与中央+270的林睿哲重叠，其他场景落点保持原规则。已保存command-assembly后，导航改读当前剧情目标，不再要求首次汇报。MaleCurrentCommand复测1791106923 PASS：28行汇报、10项职责、编队进出和数据保持均通过，返回时逐个断言与9位演员横向间距大于200，并断言提示已更新。CUA实际画面确认分开站位、原菜单可见且工厂潜入入口存在。其它来路落点尚未以此回归证明。


MaleCurrentInfiltration 1791106984 PASS：从本轮汇报成果副本，经原菜单进入工厂潜入、夜光镜扫描、接敌对话和首场真实巡逻战，21.40秒获胜。两位已采用模型分别12/14次模型动作、12/9次命中、fallback=0；导师11次命中，火7次、风3次、联动7次，导师剩余22生命。报告中15段守卫攻击均完成约1.6秒，实际释放位于动作区间内；原生报告独立检查后归档male-current-infiltration-combat.json。正常路线未注入保存失败或未来版本修改，其他原有表保持。

胜利后返回厂区、记录patrol-cleared，重复请求未重复开战，再返回指挥室并从日志重读通过。继续用的male-current-infiltration-resume-fixture指向战后仍处于潜入状态的副本，后续退出验证在另一运行数据库继续，因此下段从该中段成果接续。证据male-current-infiltration-native.txt、save.json与png；操作包含菜单事件和战斗command接口，不计完整OS试玩。下一段继续隐蔽路线与研发人员，未宣称第三章或最终作品完成。


### 男主角隐蔽路线与研发人员（2026-10-04）

MaleCurrentInfiltrationPath 1791107162 PASS：从首巡逻战成果副本恢复，实际暴露被巡逻发现一次、退回安全点后重新择机移动，三处箱后以原行动按钮隐藏/离开，动作按钮在视口内。路线实际移动1851.68、用时31.03秒，三处隐藏均约5秒；过路和研发人员侦察共3行原剧情，完成凭据不能靠仅给终点坐标跳过。正常路径没有保存故障注入；中段报告/图像保存为male-current-infiltration-path及cover前缀。已查看第二掩体画面，角色透明表示隐藏；这不代表整体美术已最终验收。

MaleCurrentResearcher 1791107220 PASS：接上述成果，经原继续行动入口、2行接敌对话和真实战斗制服研发人员。返回Factory落点4100、研发人员受控状态、核实指挥中心提示与后续对话门槛通过；不重复开战、首份战报不被重写，先前模型/物资/其它表保持。首份无内容胜利被拒，没有注入HP或成功结果。证据male-current-researcher-native.txt、combat.json、save.json、png，CUA已查看战后实际场景。测试使用游戏交互事件和战斗command接口，非OS全程操作。下一段须先做researcher-interrogation，再进入第二巡逻战，不跳过审问。


### 男主角审问与留守队伍验证（2026-10-04）

MaleCurrentInterrogation 1791107396 PASS：从本轮研发人员真实制服成果继续，12行原对话、捂嘴/松开、狐狸露齿、男主动作与研发人员倒地完整。狐狸牙齿补片逐帧跟随mouthCenter锚点，距离小于3，警告持续约1.23秒；男主动作约0.90秒、影响点约0.33秒，倒地完整1.35秒。剧情和演出证明各保存一次，原模型/物资等表保持；查询指向第七层控制舱与乌云留下看守，与原策划dialogue-script.md 840–848对应。已查看male-current-interrogation-fox-warning.png，报告male-current-interrogation-native.json。正常路线无写失败注入；第二巡逻战正在接续验证。


MaleCurrentSecondPatrol 1791107433 PASS：原继续行动入口进入三守卫战，乌云实体未生成，目标仅导师与妮妮莉特，风技能按钮隐藏且命令返回ROLE_ABSENT。准备阶段无伤害，真实战斗27.97秒获胜，导师16生命/17命中、妮妮莉特16次模型动作/16命中、fallback=0，火15命中、风0。返回厂区后乌云在x=4680留守，控制舱入口可用；先前表保持，战报幂等。报告和只读数据库归档male-current-second-patrol-native.json/save.json。来源为本轮审问真实成果副本，未导入胜利，未注入存盘故障；操作为菜单事件与战斗command，非OS全程试玩。


MaleCurrentControlPod 1791107513 PASS：从第二巡逻真实成果副本通过原入口进入控制舱，导师/妮妮莉特/Q版狐狸三人同行、乌云未进入。逐层1→7共六段实际计时穿行，每段约8.72秒、横向跨度约1000且每段524次记录；越级提交与过早开门被拒。第七层原HUD持续向右遇封门碰撞，人物不能越过x=1500；操作舱门后2.81秒完成开启，实体阻挡移除、门角105度。声音仅验证启动句柄，未作为混音听验通过。先前表保持，当前charM及控制舱存档只读归档，证据male-current-control-pod-native.json/save.json/png。CUA查看了实际旋转阶梯第六至七层过渡；下一段接舱内研发人员对话与屋顶通道，整体作品/最终包验收仍未完成。


### 佛陀与玉的 Q 版画风协调 V6（2026-10-04）

重新对照桌面 Q版 玉.png、玉 v3.png 与玉 v3 佛陀.png。内置 image_gen 编辑独立头躯干与手臂图集，降低橙金饱和度、减弱圆珠镜面高光，改用柔和浅金与灰紫阴影；原图集尺寸与透明通道保留。生产 BuddhaChibiStyle 已切到两张 v6 图集，头部 scale .38→.323（缩小15%），关节参数与移动速度未变。旧版素材保留可回退。完整生成提示存于 LSD/Docs/evidence/2026-10-04/buddha-v6-prompts.txt。

YuBuddhaStyleV6 1791108047 完成同场新旧对比并截图；人工查看颈部和六臂连接，无明显断开。YuCarrierV6Lifecycle 1791108107 PASS：两轮乘坐/护卫/落地，乘坐约0.80–0.82秒、落地约0.816秒，落地坐标归零，recovery .2，重复请求拒绝、销毁中止通过。本轮仅为原生演出与动作生命周期验证，没有重跑完整救援战；美术最终验收和整体作品验收仍未完成。


### 男主角控制舱剧情与屋顶接续（2026-10-04）

MaleCurrentControlPodDialogue 1791108205 PASS：从本轮七层开门成果副本恢复，实际走到x2196后启动29行原剧情，三名研发人员在场。双角色举枪约1.317秒，狐狸露齿/prepare约1.25秒、75帧锚点跟随；有效演出证明保存、重读29行后不重写证明，先前表保持。已查看male-current-control-pod-fox-warning.png。

MaleCurrentRoof 1791108241 PASS：从上述对话成果通过屋顶原入口，楼梯13.15秒/724次采样，平台转向时跟随者保持安全；男主3轮、妮妮莉特4轮攀爬，二人最终落点x1700/y1070，接触/越墙/落地碰撞及recovery .2通过。恢复场景为FactoryRoof。已查看male-current-roof-route-landed.png；屋顶背景仍显空，不据此认定最终画面完成。

MaleCurrentRoofDialogue 1791108337 PASS：实际靠近x2496后11行乌云对峙，纹记锚点跟随108帧、光柱持续约1.80秒，重读及场景恢复后信标保留。与原策划dialogue-script.md第2-15/2-16段对应。以上正常路线均无保存故障注入、无进度或HP注入，前段成果采用隔离QA副本；操作为原HUD/交互事件及公开流程接口，非连续OS全程试玩。报告及只读存档摘录已归档，主存档未动。下一步为屋顶真实战斗、乌云离开与后续章节，最终作品验收仍未完成。


### 男主角屋顶实战、乌云离开与返回（2026-10-04）

MaleCurrentRoofBattle 1791108462 PASS：沿用本轮对峙成果副本进入真实屋顶战斗，17.23秒获胜。导师48生命/7命中，妮妮莉特84生命/10次模型动作/10命中/fallback 0，火技能5命中。乌云包含射击、近战和风；8次动作均完成原生动画时长，射击1.067秒、约0.50秒释放，近战/风1秒、约0.40秒释放，倒地完整1秒。正常保存、返回屋顶和战报幂等通过。截图male-current-roof-wuyun-wind.png已查看。

MaleCurrentRoofAftermath 1791108502 PASS：5行原剧情，抬臂0.85秒、漩涡1.60秒、入漩涡1.58秒且76帧飞行，完成后乌云隐藏；重读与重入保留结果，先前表保持。MaleCurrentRoofAftermathExit 1791108573 PASS：恢复不重复演出，经原返回控制舱、离开控制舱和厂区菜单回OperationRoom，乌云不再出现在厂区。

发现并修复Factory.Roof的阶段提示：对峙后提示迎战、胜利后提示交谈、乌云离开后提示返回控制舱并离厂，避免仍显示前往发射炮。最新退出测试核实实际渲染标签文本；退出存档与截图归档。以上为隔离存档的分段原HUD/技能/流程事件模拟，不是连续OS全程试玩，无HP/胜利或故障注入，主存档未修改。第二章厂区路线本轮已经接回指挥室；第三章和最终完整作品验收仍需继续。


### 男主角第三章重连、防卫与重创（2026-10-04）

依据chapter-three.md运行工作稿继续，而非宣称原历史对白已有第三章。MaleCurrentReconnection 1791108751 PASS：屋顶撤离成果副本经指挥室16行来电、实际学院走廊到研发室6行异常监测，重读、日志、往返恢复与先前表保持通过。截图发现通讯波形板盖住男主帽子，Reconnection将显示板相对marker高度140改为220，交互坐标未变；当前原生场景检查该高度并查看reconnection-panel-raised.png，普通桌面布局已核实，小屏仍未覆盖。

MaleCurrentAcademyDefense 1791108835 PASS：从重连成果恢复研发室，实际通过D/C/A走廊接近防线再开战。三阶段52.45秒获胜，导师89生命/27命中，妮妮100生命/23次模型动作/21命中，火10命中，治疗库存真实消耗1份。供电与信标均剩132，护送794距离、约9.35秒；六只小饕餮均完成死亡动画，攻击记录覆盖吹气、炸弹、挥击、冲撞、滚动，逐条完整时长检查通过。胜利证明、幂等存盘、历史战报与其它表保持通过。

MaleCurrentAcademyLoss 1791108981 PASS：接防卫真实成果靠近A区通讯点，8行重创剧情、1.40秒冲击演出、3页人员记录、妮妮当前3行对话，重读不改原凭据。损坏场景在休息室/研发室及Start恢复保留；不可出战人物与仍可出战妮妮状态相符，乌云/阿岩作为此前离场记录，双子待救援。正常路线均无故障注入、无写入胜利/HP，测试为分段隔离QA副本的HUD/菜单事件与流程接口，不是全程OS游玩。下一段继续玉到场、双子护送与新版佛陀完整救援战；整体作品验收仍未完成。

本轮查看male-current-academy-loss-scene.png另发现：A区电梯附近，电梯目的地与妮妮莉特交互菜单同时显示并重叠。该截图不能作为界面最终验收，下一轮应修复邻近交互菜单避让/选择，再继续救援。损坏墙体裂纹和碎片仍为简化表现，需要美术打磨。


### 学院门口交互避让与玉到场（2026-10-04）

修复Academy.System.lua/.yue：当玩家在门/电梯感应区且存在moveTargets时，NPC自动选择让位给通行交互；离开该区域重新检测队友。AcademyDoorCompanionPriority 1791109253 PASS：从本轮重创存档副本恢复A区，门口仅通行菜单、走开后妮妮菜单恢复、返回门口再次让位，最后原菜单实际进入C区。门口与队友恢复截图均已查看。该修复针对通行菜单与NPC菜单冲突，不代表其它终端菜单全部完成避让验收。

MaleCurrentJadeArrival 1791109303 PASS：沿A/C/D/RD实际门路前往研发室，实体阻挡把男主限制在x4468.5；12行玉到场剧情后1.22秒开路，玩家实际越过到x4674.75。双子仍标记待救援，未仅凭对话写入救援胜利。重读不改记录，恢复保留玉骑乘与新版佛陀V6护卫状态，双子idle循环存在。正常路线无故障/进度注入，先前表保持。已查看male-current-jade-arrival-restored.png，完整双子护送战正在另行验证。

首轮新版佛陀护送实战1791109379 FAIL（保留before-fix报告）：四怪已清理、双子生命100/62、保护场吸收52，但出口坐标停在5398.964/5559.380，240秒超时。前方双子进入1单位到达容差后停止，后方双子同时受160间距限制，物理步长无法收敛到自身容差。Rescue.Battle现于进入到达容差时将剩余不足1单位对齐实际停靠点，释放后方所需间距；不放宽通关距离、不跳过敌人、不改HP。目前从同一到场成果重新运行完整战斗验证。

修复后MaleCurrentTwinsRescue 1791109745 PASS：同一来源成果重新实战36.04秒完成，双子最终精确抵达5400/5560，真实移动1250/1210，最小采样间距160.42，生命100/62。导师64生命/15命中，妮妮100生命/12模型动作/10命中，火11命中，治疗库存0且没有注入补给。保护场三次吸收共52，剩108，场外双子曾实际受伤。四怪完整动作/死亡时长检查通过；佛陀V6护卫可见、三次受击脉冲、玉乘坐/落地约0.8秒及救援后机器人隐藏均通过。返回原场景的双子实际获救记录、幂等重入与先前表保持通过。证据male-current-twins-evacuation-route-native.json/save.json和buddha-v6-rescue-battle.png。本轮完整救援战是事件驱动模拟，仍不等于完整OS三章通关或最终美术验收。


### 男主角撤离窗口、最后任务与终章（2026-10-04）

MaleCurrentJadeDistance 1791109957 PASS：接本轮双子真实救援成果，8行后续对白、五位讲话者立绘/骨骼匹配、重读两段剧情不改当前目标/保护场，Start恢复及先前表保持通过。玉仍使用原立绘作为对话肖像，场景实体为原Q版骨骼，并非用立绘代替场景动画。

MaleCurrentLastPromise 1791110021 PASS：实际走近出口并确认既有移动型辅助机，临时改选后取消不覆盖历史选择；三阶段实战43.31秒获胜。载体实际移动1740至x2090，剩10生命；妮妮31.76生命、18次模型动作/13命中并到x1901.51；导师91.55生命/24命中，火18命中。三次实体掩体挡击、范围外伤害68.24、范围内恢复41.55，金粉45+30-36.79=38.21；紧急治疗配给1份但未使用，永久库存未增加。敌招与倒地完整、证明拒绝伪造、重复结算/历史记录不重写通过。

MaleCurrentFinalBetrayal 1791110173 PASS：经原研发室出口到终章，15行运行稿，通讯读数冻结但演出/UI继续运行；林睿哲实际接近330距离，攻击1秒、约0.4秒命中，男主受击0.6秒后倒地1.2秒，最后姿态保持。重读不重写证明，同进程Start恢复进入Ending记录页且不恢复学院经营场景。未据此声称冷启动/实际OS完成，结局回顾与署名仍须继续。以上均来自隔离QA链、无保存故障或进度注入，证据以male-current对应前缀归档。


### 男主角结局记录与实际鼠标验证（2026-10-04）

MaleCurrentEndingFlow 1791110352 PASS：部分阅读不标记署名完成，完整翻页后记录状态；重看终章不重复奖励，结局弹层阻断底层退出，受损学院保留双子获救与先前数据。同进程Start恢复记录页。新增MaleCurrentEndingResume验证独立入口重载已通关QA副本，所有表不变、不自动重播；不是进程冷启动测试。

随后通过CUA实际鼠标逐页浏览1至9页、完成返回标题、点击继续旅程回到第1页。1792×1136内容区域内，任务、训练统计、11位人员记录及署名无可见裁切。训练回顾6条示范、18动作/13命中、43.3秒撤离对应本轮实战。OS操作后只读比对全部数据库表与来源一致，未改主存档。证据male-current-ending-flow-native.json、male-current-ending-resume-native.json、male-current-ending-os-review.json。此验收只覆盖结局鼠标操作，不能替代三章连续OS试玩、其它设备布局、音频听验和最终包验证；整体目标继续。


### 当前运行资源暂存包 stage-e（2026-10-04）

新建/private/tmp/lsd-game0-stage-e-20261004，879文件、268091318字节，271 Lua全部语法通过；逐文件哈希验证，86 atlas/89页、22 clip/399矩形、11 model依赖和边界检查通过，全部音频完整解码通过（不等于声音听验）。包含当前佛陀V6、目标提示与救援出口修复；无Test/Tools/Docs。

StagedCurrentEnding 1791111126 PASS：清理资源缓存及包模块后，游戏搜索路径仅指向stage-e，另保留引擎标准库；通过实际init与标题继续事件恢复本轮男主通关副本的结局第1页。佛陀V6乘坐/落地，以及男女主审问捂嘴/释放/狐狸警告/打击倒地动作均完成。全部存档表与来源只读比对一致，主存档未修改。已用CUA查看结局恢复画面。证据stage-e-integrity/atlases/audio/ending-native/save-check/manifest。该包不包含引擎，测试不是冷进程或OS全程游玩；不能标记最终发行验收。


### 训练长稳内存归因诊断启动（2026-10-04）

新增TrainingMemoryDiagnostic，在原完整示范/比较/采用循环上，改为逐轮独立文件保存，不在report累计历史；每轮GC后采样对象/引用/堆，随后记录已加载模块与registry直接表条目数和最大整数键。runId1791111307，隔离lsd-training-memory-diagnostic-qa存档，至少12轮及720秒；通过Agent直接读取运行句柄确认存活，当前尚未结束，不能标记PASS。

第1轮约65.13秒完成，对象1199、LuaRefs261、CallRefs371、堆3730.55KB；registry弱值对象表最大整数键4766、261条目，回调表523条目。Training.Arena源码的UnitAction全局定义捕获self，可解释为何旧测试始终保留最近1个arena，但尚不能解释旧长稳第7→8轮132.24KB跳升。待诊断结束再判定具体来源，不在运行中更改生产动画/训练逻辑。新入口与观察工具均保存在Test/TrainingMemoryDiagnostic.lua及Tools/observe-training-memory-diagnostic.json。

运行中的只读引用观察于第4轮取得直接证据：registry回调表中7个Training.Arena回调的self上值共同指向同一个closed=true、mode=leaving的训练场（见training-retained-arena-reference.json）。这确认了保留路径；含不同actionPrefix的任务也使用相同注册实现，修复需覆盖妮妮与乌云动作以及共享战斗。弱引用修复候选已在临时目录生成并通过语法检查，尚未写入生产源码，以保持当前12轮基线不变。诊断仍运行中。


<!-- preserved-progress-end -->
