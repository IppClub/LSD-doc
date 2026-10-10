# 开发历史记录 · 第 02 卷

> 2026-10-05 从旧进度页归档。以下为当时记录，含已被后续结果替代的状态，不作为当前待办。请从[当前进度](progress.md)或[历史索引](progress-history.md)继续阅读。

## 原始记录

<!-- preserved-progress-start -->
## 阿岩接引与原学院参观（2026-10-03）

上一轮五招/城市滚动与风火实战属于已验证进展，本轮继续原2-3，不降低三章目标。再次对照原对白，章节适配表现已明确列出2-1至2-17全部后续段落及重复编号的两段2-6，保留2-4合作+对打、2-5邮件(3)/阿岩身世、工厂/寻人/信标与后世界范围，不让能源子任务或邀请对白代替章节通关。

新增Story.AcademyVisit只在已实地收取能源的TrainingRoom出现。阿岩、林睿哲、李叶娜用原Spine与Figure；玩家从原学院门路进入房间，认识2600处阿岩，跟随至3100认错方向，再回2200听林睿哲安排，最后护送至935原虚拟训练终端。人物真实走路，落后420时等候，通讯和对白期间停步，恢复玩家操控后继续；各停步分别保存ayan-arrival/detour/tour三段事实。首次手机读只提示前往对应实体，不远程认识/参观；第四页可重读已记录事件。

AyanVisit1791003975最终PASS（ayan-visit-final.txt）：实际Start安全续玩已赚取能源副本，原PreparationRoom→PassageB→TrainingRoom两次实体门交互；远程Flow和Journal初次接引拒绝；三段原Yarn分别完整11/9/14行，主角姓名实际插值；阿岩实际路程超过1500，错路与纠正、停步交谈通过。故障触发器导致节点/解锁同事务回滚，人物保持busy，公开重试完成；邀请奖励只一次，6/18两份模型main/backup行字节不变。走到原左端进入基础VR仍可达，场景离开后无接引UI叠层。此前首轮漏接模块入口、第二轮world单调度被原终端覆盖均明确失败；改为独立anchor节点调度后通过。原生观察还发现Story.Display时序可能隐藏引导，改为每帧按本房间storyBusy/journalOpen刷新，最终增加可见性断言通过。

本轮暂未补原骑白虎入场、撞上/握手演出；ayan-visit-native-observation.png为引导可见性修复前的人物场景观察，不作为最终指引UI证据。训练邀请不是李叶娜两场战斗已经实现或获胜；下一阶段需独立实体合作战与对打胜负、完整动画与事件、结算及2-5实际入口。全Game0继续active。

26058正常退出确认无进程→26439后，AyanMidResume1791004131 PASS：读取真实接引首次保存时复制的自有QA安全点，经实际Start及原学院两道门，接续第二段带路，不重播首次接引；余下9/14行Yarn与实体路线完成，解锁只一次、能源仍两份、两模型字节未改，原VR入口与旧接引UI清理通过。AcademyTrainingRoute1791004190回归PASS：未获得能源的独立QA档保持原PreparationRoom→B区→TrainingRoom→VR→原路返回，统一HUD四动作/实际射击命中均通过，未让后续接引阻塞基础训练。

LiyenaAnimationCatalog PASS（liyena-authored-animations.txt）：实际原李叶娜Spine的pistol/melee/bow、三种枪、throw的攻击点与完整AnimationEnd已探测；parry/defence/comp/comm无攻击事件。它用于下一阶段按实际素材绑定合作与对打，未宣称两场战斗完成。白虎与撞上/握手仍是演出素材差距，不隐藏。

26439正常退出→26514首个完成档恢复检查发现打开通讯后旧NPC fmove仍持续，不能只清空方向键。已在接引暂停/等待/抵达时显式结束fmove/bmove并清零速度，Story.Flow.freeze同样结束场景人物的普通移动，避免玩家阅读期间滑步；保留落地等非移动动作。26514正常退出确认无进程→26627后，AyanResume1791004458最终PASS：真实Start/原学院门路，完成接引档保持三节点/一次邀请、两份能源与两模型未变；在正在带路时开通讯，NPC和玩家位置实际稳定，关闭后续行，进入VR旧UI清理、公开返回后接引阶段恢复均通过。此前1791004279为真实失败，1791004366只验证NPC暂停；最终报告额外覆盖玩家暂停。

原生截图进一步证明仅Node.visible断言不够：接引根UI未设置屏幕size，内容虽逻辑可见却在视口外。已设置随App大小更新的根size；AyanGuideFrame1791004584 PASS与ayan-guide-layout-final-native.png实际显示暗色背景内的引导文字。较早ayan-visit-guide-final-native.png也未包含这一视口修复，不作最终UI证据。此视觉测试从明确已赚取接引档进入原训练室，不冒称它再次完整通过参观或新档主线。

StoryUI1791004614回归PASS（story-ui-after-physical-pause.txt）：物理指挥室→C区/D区→资料室/研发室路线、任务门槛、原研发Yarn/手机邮件、档案保存回滚重试、重读一次和恢复操控均通过。这个UI专项的首任务胜利为明确服务fixture，不用它声称实际再打一场首任务。测试预加载改成逐个await，沿用当前原生引擎共享解析器的顺序加载防护。

本阶段继续保留2-4真实合作战/对打、原白虎出场/撞上/握手与后续全章节欠项；不标2-3完整演出或Game0完成。原用户lsd.db SHA256仍760372bda8ae788c451e95bc169ccddd6b5837cee36fe9101b330efd4f7e3d39。语法/TrainingContract27、维生场与风火纯逻辑、两仓diff检查及Sphinx通过，Sphinx仅既有v-producer未入toctree警告；未提交/推送。

入口原生截图发现阿岩与玩家停在同一点会遮住接引人，最终只调整NPC等候站位：阿岩在935原终端左侧790附近，李叶娜1250，不改终端或传送玩家。AyanGuideFrame1791004784（ayan-entrance-spacing-final.txt）与ayan-entrance-spacing-final-native.png显示实际走到入口且人物站位/指引可读；对角色Entity和同名Unit siblings的原生查询均各1，重复单位猜测已被当前证据排除。完整对话/中途重启与暂停证明由上述对应测试承担，不把这份视觉专项扩大为三章或完整新档通关。

## 小饕餮原策划再次复核（2026-10-03）

再次读取原 `monster-spine-action.md` 小饕餮技能表，确认五招为 blow/swing/butt/roll/bomb，并以现有 EnemyCombat 在原生 PID 26627 实测。EnemySkills runId=1791005475 PASS：各招完整动画和恢复、无前摇扣血、横击退/无击退/纵击飞、滚动群体各一次、炸弹实体碰撞后双目标范围无击退、城市坐标完整滚动阶段。EnemyAttackTiming runId=1791005510 PASS：两次连续 blow 的实际 attack/AnimationEnd，正面和距离判定，一次伤害；怪物 recovery=0.2 回 idle，人物完整 pistol 后 recovery 回 prepare。证据为 LSD 的 small-taotie-design-recheck.txt 和 small-taotie-recovery-recheck.txt。本轮为原生自动测试，非人工全流程试玩；正式训练/任务复用五招，开场教学仍按教学流程保留单招。EnemySkills 新增报告 runId 防止混淆旧成功；本轮未更改已接入的技能实现。

## 李叶娜两场训练与胜负安全点（2026-10-03）

上一轮小饕餮复核为实际原生证据进展。本轮继续原2-4，不缩减三章目标。TrainingRoom原935终端增加合作/对打两个选择，保留原示范训练第一项；完成阿岩参观才允许合作，合作真实获胜并听完挑战才允许对打。Trial.Battle用独立导师与李叶娜实体，不借用妮妮莉特保存模型做导师控制；三只原小饕餮五招与两人实际命中构成合作胜负，第二场为两人敌对实战。HUD/枪械槽/Skill/摇杆/VR/原结算与Yarn均复用。pistol/melee依素材attack事件结算，完整AnimationEnd后0.2恢复prepare；parry无攻击事件，只在完整动作期间防御。死亡/撤离等中断记明原因，不要求死者继续完成攻击。

LiyenaRoute1791005687首轮PASS，1791005866死亡与停场整理后再PASS。最终LiyenaRoute1791006026（liyena-public-route-final.txt）PASS：真实Start已赚取接引档的隔离副本→两道原学院门→物理终端第二项→导师与李叶娜共同三怪→原结算→完整挑战四行→真实对打→原结算→认可五行→原TrainingRoom。合作14.0346秒，两人各8命中/100生命；对打21.8628秒，导师20命中/46生命、李叶娜9命中/0生命。正常攻击事件与完整时长逐项检查；被击败的未完攻击明确记录中断。结算INSERT奖励故障使胜负/解锁回滚，原按钮重试后提交；挑战与认可各只记录一次，两份学员main/backup字节及已赚取两份能源保留。这个测试从真实赚取的中期档复制，不宣称本轮全新存档完整Game0通关。

LiyenaOutcomes1791005822（liyena-native-outcomes-final.txt）PASS：真实李叶娜子弹被parry挡住，防御无伪造攻击事件且完整结束回prepare；原摇杆实际接近后刀击，按素材事件伤害并完整结束。显式低生命失败夹具下导师被对手真实攻击击败、合作NPC被小饕餮真实攻击击败，以及公开中止训练均无对打奖励/认可、无active残留。失败夹具设1生命并摆放敌人，不将其视为正常游玩胜利。首次1791005810失败是测试在异步角色生成前取到nil，改为等待实体/落地，不改变生产战斗门槛。

26627正常退出确认无进程→27536：LiyenaResume1791005992 PASS，真实Start读已赚取合作战终态，原门路/第三终端按钮补播挑战四行再进入全生命实际对打，公开中止不发对打胜利；合作解锁一次。27536正常退出确认无进程→27649：LiyenaDuelResume1791006149 PASS，Start恢复已赚取对打胜利但未读认可的安全点，经门路和第三按钮仅播放完整认可五行，原对打attempt仍只有一个，不强迫重战。该新进程随后LiyenaCompleteResume1791006186 PASS：Start另读完整完成档，两胜/认可/通讯第五页/认可完整重读/一次奖励/6与18样本模型行与能源两份保留。它属于同一新进程分别载入两个真实中期副本，非单次全新流程。

MissionService1791006108（mission-service-after-liyena.txt）旧任务编队/模型快照/终态冲突/原子一次奖励/中断恢复/未来版本只读全部PASS，noModel分支未破坏旧任务。liyena-duel-native.png是第二轮实际对打进行中的原生观察，显示原HUD与两侧人物/物理弹，非合作截图；liyena-route-native-observation.png仅为原学院走廊途中观察，不用它证明战斗或最终入口布局。

第二章2-5阿岩身世/邮件(3)、两段2-6与2-7至2-17、第三章与Ending仍保留待实现；2-3骑白虎/撞上/握手及既有程序化效果仍需精修。原用户档不用于本轮测试，未提交或推送。全Game0保持active，未标完成。

原生入口复测发现“李叶娜合作训练/对打训练”长文案超过原固定按钮宽，缩为“李叶娜合作/李叶娜对打”。LiyenaFrame1791006297与1791006501 PASS，三项菜单/实际文本宽度/实体入口与引导视口均成立；最终入口截图liyena-terminal-final-native.png。实际鼠标第一轮进入即开打，导师仅一次命中、李叶娜12次，18秒内清怪导致参与不足失败，截图liyena-coop-mouse-native.png保留为真实体验问题，非胜利证据。

据此增加ready准备态与原InputButton“开始训练”，开始前无NPC/怪物AI、无攻击与战斗计时，玩家先读操作与合作要求，准备期可公开中止。LiyenaRoute1791006394（liyena-public-route-ready-final.txt）两场全流程再PASS，额外证明准备期间满生命/无攻击/无NPC位移、开始后实际战斗与原事务/对白/两模型保护。LiyenaOutcomes1791006471（liyena-outcomes-ready-final.txt）在新准备流程再次通过挡弹、完整防御/刀击、实际双方死亡与准备阶段公开中止不发对打/认可。LiyenaResume1791006602（liyena-ready-start-resume-final.txt）同进程实际Start恢复真实合作安全点，经门路补挑战、进入ready对打、双方入镜、明确开始后中止/返室PASS，不能将此补测称再次进程重启。

原生鼠标重试：从LiyenaFrame隔离完成档在训练终端点击合作→准备后点击开始→实际枪械按钮，两次导师命中、12次李叶娜命中，18.7508秒合作获胜，导师100/李叶娜80，实际点击原结算返回训练室。证据liyena-coop-ready-mouse-native.png与liyena-coop-real-mouse-report.json；这是真实鼠标合作回合，完整双场/剧情通关由上述自动事件回放承担。准备期第一张liyena-ready-native.png同时发现默认镜头未容纳三怪，随后把准备期也纳入同一镜头范围计算，最终截图与测试另记。

准备镜头最终修复后LiyenaReadyFrame1791006642（liyena-ready-frame-final.txt）PASS：实际训练室行走/原终端进入合作准备，两秒内双方及三怪生命未变、无动作记录或怪物攻击，五角色全部处于实际镜头范围；最终原生截图liyena-ready-final-native.png。鼠标在未开始时点击中止，原结算显示0秒/0命中/双方满生命，liyena-ready-mouse-abort.json确认数据库aborted且无active，再实际点击原结算返回TrainingRoom。准备镜头与0秒统计为最后两项专项修复，不将其冒称重新运行整条双场战斗。


## 2026-10-03 原2-5邮件、阿岩食物与故事片段

AyanAfterTrial1791007071原生PASS（ayan-aftertrial-public-first.txt）：真实赚取两场李叶娜胜利的隔离副本，经Start与原学院门路进入TrainingRoom；林睿哲/李叶娜不再留场。第三封邮件四行与明确转告三行分别记录，未转告拒绝领取。实际阿岩交互食物七行→点击聆听往事七行→共享线索八行，首次远程手机/远处往事均拒绝；人物资料解锁后完整重读。转告与故事片段INSERT故障回滚后从公开按钮重试，五次解锁各一次，两学员main/backup字节及能源两份保留；最后实际原门路到RestRoom。邀请不等于医疗新人已会面。

27649正常退出并确认无进程→28199：AyanAfterTrialMidResume1791007391 PASS（ayan-aftertrial-mid-resume-final.txt），Start读取真实食物安全点副本，经原门路只接续往事与共享，不重发食物；五解锁/两模型/能源均保留，实际返回休息室。本轮编译Start.yue的existDB清理保护，避免入口与QA双重DETACH。公开身世补足原策划占位，隐藏AI伴侣真相不提前揭露；VR成果共享仍是线索，不冒称现有模型已经可共享。食物为程序图形托盘原型，仍待美术精修。

2-6休息室医疗会面与同编号备战室剧情、2-7至2-17及第三章Ending仍须继续实现与验收，原三章目标保持active。本轮没有使用原用户档、提交或推送。

同一新进程28199另载完整真实终态：AyanAfterTrialCompleteResume1791007478 PASS（ayan-aftertrial-complete-resume-final.txt），Start恢复五段记录，通讯第六页往事完整重读，经原门路回训练室恢复stage8阿岩，食物不再出现，人物资料线索明确尚需证据，五解锁/模型/能源保留。这是同一进程分别Start两份隔离副本，不称两次进程重启。TrainingContract27、GroundLifeSupport、WindFireContract和两仓diff检查通过；网站Sphinx构建成功，仅既有v-producer未入toctree警告。用户lsd.db SHA256仍为760372bda8ae788c451e95bc169ccddd6b5837cee36fe9101b330efd4f7e3d39。

用户再次提醒小饕餮多招后，对照原monster-spine-action需求并运行EnemySkills1791007534原生PASS（small-taotie-five-skills-current.txt）：五招完整结束/真实攻击事件、前摇不扣血、挥尾横向击退/角顶纵向击飞/跳尾无击退、炸弹真实滚动投射物与双目标范围无击退、滚动双目标各一次与城市完整滚动边界、0.2恢复idle均成立。滚动由rollStart→现有卷身图集滚动→rollEnd构成，素材无roll攻击事件，不伪造事件。炸弹仍用程序图形补独立投射物，后续需美术精修。

AyanAfterTrialFrame1791007576 PASS：真实两战终态副本在原训练室物理行走到1900，阿岩2050，人物分开、原交互按钮文字容纳、食物托盘可见，引导适应实际视口，无林睿哲/李叶娜残留。ayan-aftertrial-food-native.png为原生最终布局。随后实际鼠标点击人物故事与“错过的约定”，ayan-story-locked-mouse-native.png显示未记录提示及实际步骤，无提前泄漏往事；实际点击返回漫游。该画面验收不是完整鼠标剧情通关。


## 2026-10-03 两段2-6首次运行

MedicalVisit1791007758原生PASS：真实完成2-5的隔离副本，从原Start备战室走A区左门进入休息室，医师moyu/moling实际实体，首次远处和手机拒绝；实际走近诊疗区播放完整35行/玩家姓名/中西医分工/三顾茅庐。医师解锁INSERT故障回滚→公开重试，保存真实医师安全点；通讯第七页明确读林睿哲3行材料委托，原门路回备战室与Ni/Wu实体完整15行，失败事务回滚重试，无重复同伴。已记录医师35行可从备战室手机重读，三解锁各一次，两模型/能源保留。后补Story.Recorded场景即时刷新与诊疗桌药瓶原型，最终复测另记。

MedicalFrame1791007850第一版布局PASS，但原生medical-station-native.png发现医师标题长于黑色底板；随后短为“医师姐弟/行动准备”，并为诊疗区与备战室会面更新导航提示，最终画面需另验。不能将第一版截图作为最终布局或完整鼠标剧情通过。原三章目标继续active，2-7及以后尚待实际开发。

28199正常退出、确认无进程→28499：MedicalMidResume1791007926 PASS（medical-mid-resume-final.txt），Start读取真实医师会面已完成而委托未读的安全点。医师无需重播，在备战室通讯第七页读3行委托后，场景即时出现真实Ni/Wu会面，关闭手机原地步行到中央，完整15行准备/一次解锁/模型与能源保留，无须离开再进入。这验证新增Story.Recorded场景通知的实际行为。

同一新进程28499另载完整安全终态：MedicalCompleteResume1791007963 PASS（medical-complete-resume-final.txt），Start恢复医师会面、委托和备战室准备三节点/三解锁，原Ni/Wu恢复，通讯第七页完整重读15行，两模型与能源保留。此项不是第二次进程重启。

最终场景通知/短标题/诊疗原型/导航指引更新后MedicalVisit1791007987（medical-public-route-final.txt）整条公开路线再次PASS，原35/3/15行完整性、事务故障重试、人物不重复、首次限制与已记录任意场景重读均成立。它接续真实中期2-5档，不宣称全新存档三章通关。

StoryUI1791008059（story-ui-after-medical.txt）共享Flow/Journal/Navigation旧剧情回归PASS：实际指挥室/电梯/资料室/研发室路线、暗格任务门槛、原研发Yarn与手机邮件、保存故障重试、重读不重复与输入恢复成立；其中任务胜利是明确服务夹具，不冒称这项回归实际完成警戒战斗。训练规则27项、维生场与风火规则再次PASS，网站构建仅既有v-producer未入toctree警告，两仓diff无错误。原用户lsd.db哈希仍为760372bda8ae788c451e95bc169ccddd6b5837cee36fe9101b330efd4f7e3d39。

FlowerAnimationCatalog1791008152（flower-authored-animations.txt）原生素材探测PASS。小花妖leech/pull与大花妖attack/twine完整结束，病毒/播种素材为三段，均无attack事件；xiaohuayao没有bud，花蕾需另查hualei资源。已把精确实测时长与命中校准要求记录technical-design。它只是2-7实现前置素材证据，不是歌谣/花妖战斗/材料采集已经完成的证明。

MedicalFrame1791008209（medical-frame-final.txt）最终PASS：原休息室实体、物理步行、人物间隔与菜单宽度、可见诊疗原型；medical-station-final-native.png确认短标题与诊疗区导航均可读。实际鼠标点击拜访医师，再点击推进，medical-first-dialogue-mouse-native.png确认原半夏立绘与对白姓名正确。仅首次两行由鼠标推进，其余另用引擎事件完成，不能说完整35行都是人工鼠标游玩。

医师画面验收的鼠标首两行后，引擎事件补完其余对白；medical-mixed-input-report.json确认完整35行/phase complete/RestRoom/storyBusy false/实际记录。原生测试最终停在可继续漫游的休息室隔离QA档，未触及用户档、提交或推送。


花妖机制专项FlowerSkills1791009041原生PASS（flower-six-skills-final.txt）：六招完整段落/前摇不伤害、吸血群体转实际回血且不击退、实际群体拉拽耗体力、单体藤击、五波地面缠绕/阵营混乱/持续毒素、完整乌云comm解除混乱但不解毒、6秒保护与冷却、病毒禁移动通讯/真实队友中弹/到期恢复、三原花蕾播种与实体清理、两真实投射物累计五秒伤害/系数/完整开花/0.2恢复均成立。此前错误父节点判定与开花后同名idle混合失败的三报告原样保留；最终停止隐藏主骨架旧idle后再混合启动idle，未修改引擎。独立花蕾图集探测1791008379与20姿态探测另有报告；姿态截图含重叠，非最终UI验收。

小饕餮共享Arena花妖扩展后EnemySkills1791009184再次原生PASS（small-taotie-after-flower-extension.txt），五招、真实事件、前摇零伤害、三种击退语义、炸弹范围双目标、滚动每目标一次及城市边界、完整结束与0.2idle均保留。Factory完整2-7公开任务和其后所有章节仍待实施，三章目标保持active。


小饕餮自动控制器EnemySkillCycle1791009315原生PASS（small-taotie-automatic-cycle-final.txt）：不手动调用start，实际自动按blow/swing/butt/roll/bomb依次出招，全部前摇→生效→结束有序且无重叠，怪物0.2恢复idle；重复重置不会无谓同名rest混合，静止人物的真实循环结束事件确认待机持续。首两轮失败为测试误用循环完成后会清空的Spine.current断言，非自动出招缺失，首份失败报告保留。

LearningStrategy1791009352（learning-after-rest-loop-fix.txt）共享恢复调整后原生PASS：原HUD近/中/远共18条实际示范→原生C4.5→距离退/射/进三规则→模型与基础控制器同站位各三场真实试战→公开采用保存。模型三胜、生命100、实际17次模型动作、无保底；基础三胜、平均生命93.333。该项验证共享Arena与人物恢复/训练回归，不代替完整故事或触摸设备验收。

FlowerSkills1791009448（flower-after-rest-loop-fix.txt）在共享rest同名保护之后完整六技能、原花蕾、五秒实际子弹累计、完整开花及idle/prepare恢复再次原生PASS。TrainingContract27/维生场/风火规则与两仓diff检查通过；网站构建仅既有v-producer未入toctree警告。用户lsd.db哈希仍760372bda8ae788c451e95bc169ccddd6b5837cee36fe9101b330efd4f7e3d39。2-7公开链路及三章剩余目标继续active，未提交、推送或发布。


## 2026-10-03 原2-7工厂部署与真实花妖战斗

FactoryRoute1791009802（factory-public-route-first.txt）首次原生PASS；伤后生命保留/学员目标状态/工厂提示更新后FactoryRoute1791009909（factory-public-route-final.txt）完整再PASS。实际列车出口第二项→三卡编队→原Factory→原夜光镜沼泽定位→物理步行→原五行塞壬歌声→准备/开始→双保存模型和三原花妖真实战斗→完整歌谣解除混乱→胜利保存故障回滚重试→实地材料两行→第八页明确通知医师。最终报告Ni6/Wu18样本、导师14/Ni6/Wu7命中、无保底、毒伤60/混乱4/病毒1、歌谣完整两次解除3/1人、17.286秒，三人40/64/22。起点为真实2-6完成副本直接选择列车安全点，不冒称原Start全新通关。原歌声目前字幕而非音频，贝壳/地面藤蔓为程序原型，继续精修。

FactoryOutcomes1791009977（factory-ready-abort-and-defeat.txt）专门夹具原生PASS：保留伤后HP、六角色准备入镜且无AI、公开准备撤离0秒、显式Ni低生命被真实藤蔓击败，失败/aborted事务完成，无奖励增加/active残留。factory-low-life-defeat-native.png是该低生命失败，不作胜利证据。

28499正常退出确认无进程→29547：FactoryResume1791010034（factory-completed-after-native-restart.txt）原生PASS，Start读真实工厂终态，从原备战室/A电梯/C站台/列车公开出入口再部署工厂，三记录/一份材料/医师通知/原五行完整重读/伤后生命与一次奖励保留，没有强迫重新战斗。治疗2-8仍未发生，不将伤后HP复原。

FactoryFrame1791010097（factory-ready-frame.txt）专门准备画面PASS，factory-ready-native.png实际显示六人/原HUD/歌谣与集合/伤后HP/准备开始。实际鼠标点撤回列车，再点原结算返回基地，已实际返回TrainA；factory-ready-mouse-abort.json确认aborted、0秒/0命中、无active。该鼠标验证不替代完整任务鼠标通关。最后增加字幕受伤/趁现在及探索状态背景，专项共享回归另记。P14及三章完整目标仍active，下一段2-8正式治疗/过一天/林睿哲消息/阿岩失踪。

共享Arena可选伤害路由/外部轮次新增后，EnemySkills1791010194（small-taotie-after-factory-route.txt）五招与所有群体/击退/完整动作/城市边界再PASS；LearningStrategy1791010255（learning-after-factory-routing.txt）原HUD18示范/C4.5/两控制器各三场实际试战/采用保存PASS，模型三胜生命100/零保底，基础三胜平均93.333。

FactoryOutcomes1791010329（factory-outcomes-and-mentor-virus-final.txt）在补充死亡姿态/结算存活恢复/移除两个闲置隐藏花蕾之后再PASS：真实低生命被藤蔓击败且播放原lose、准备公开0秒撤离、失败/aborted保存无增奖/active。另明确注入病毒状态专门夹具，导师实际原枪械子弹转向队友，造成15生命伤害，再撤离；该项证明新增导师病毒适配器，不冒称公开战斗自然遭病毒的整条游玩。

FlowerSkills1791010357（flower-full-melee-queued-chant-final.txt）完整六技能/花蕾/病毒友伤/歌谣恢复再原生PASS，并新增真实melee正在播放时申请歌谣，等待实际刀击AnimationEnd后才启动comm，comm也完整结束后释放。补齐先前仅已编写而未独立验收的排队窗口。

最终死亡/存活结算姿态、闲置隐藏花蕾清理与字幕更新之后，FactoryRoute1791010436（factory-public-route-after-pose-cleanup.txt）整条公开流程再次原生PASS：16.223秒/导师13/Ni9/Wu5命中、Ni6/Wu18样本/无保底、两次完整歌谣清醒3/1、毒伤60/混乱4、三人40/64/22。此轮自然战斗病毒0；先前1791009909自然病毒1与独立病毒专项分别记录，不混用。模型行保持、胜利保存故障重试、材料与医师通知一次均通过。两仓diff、27训练规则/维生场/风火规则和网站构建通过（仅既有v-producer警告），原用户档哈希未变；没有提交、推送或发布。


原2-8/2-9首轮RecoveryRoute1791011089（recovery-public-route-first.txt）原生PASS：真实工厂胜利副本经Start及实际休息室门路，原治疗18行、首次远程拒绝、治疗事务回滚重试、两医师原comp完整结束及实际离场、治疗当天不提前回血、明确翌日才恢复、明确林消息7行及六份药品库存事务回滚重试、原同伴讨论7行、实际站台路线和原出发10行。模型保持、奖励一次、重读不重复药品成立。此段新进程恢复与鼠标画面仍待验收，药品战斗使用及2-10以后未完成，全三章目标继续active。

再次按原怪物Spine需求表核对小饕餮五招：EnemySkills1791011223（small-taotie-design-latest-recheck.txt）与EnemySkillCycle1791011263（small-taotie-auto-latest-recheck.txt）原生均PASS。单体横击退blow、无击退swing、纵击飞butt、群体路径roll、碰撞范围无击退bomb全部保留，完整动画/事件命中/前摇零伤害/0.2恢复与自动AI五招无重叠通过。训练规则27项和两仓diff检查通过，网站构建仅既有v-producer警告；用户lsd.db哈希未变。

29547正常退出并确认无进程→30219：RecoveryMidResume1791011399（recovery-treated-after-native-restart.txt）从实际治疗且医师离场安全点经Start/学院门路恢复，不重播治疗、不重生医师、不提前回血，随后实际翌日2行/明确林消息7行/六份药品/同伴7行/物理站台10行接续PASS。RecoveryCompleteResume1791011465（recovery-completed-after-native-restart.txt）同一新进程加载真实全完成副本，五条记录/100生命/库存恢复，手机五段完整重读不重复动作、奖励或药品；模型保持。StoryService1791011511（story-service-after-supplies-extension.txt）旧节点/前置/回滚/重读/未来版本保护再PASS，并增加未来版本拒绝前后四表实际内容不变断言。

RecoveryFrame1791011520首次PASS，但截图recovery-clinic-native.png揭示伤后生命提示虽visible、实际未入镜：容器size=0。修复两个状态容器随屏幕尺寸更新；1791011668从源码重新运行PASS且recovery-clinic-layout-final-native.png确认生命可读，但乌云部分被镜头裁切，继续修正近距离镜头。真实鼠标点接受治疗并推进第二行，recovery-treatment-mouse-second-line-native.png显示忍冬原立绘/姓名/文字；其余行引擎事件补完，recovery-treatment-mixed-input.json确认18行/两comp完整结束/医师离场/阶段2/伤后40、64、22，非全手动对白。FactoryExploreFrame1791011731及factory-exploration-status-final-native.png确认同类Factory状态越界修复；专门已胜副本探索画面，不代替公开战斗验收。

最终诊疗区RecoveryFrame1791011876（recovery-clinic-frame-final.txt）从源码经Start及实际学院门路再PASS，增加容器屏幕尺寸与五名角色横向完整入镜断言。recovery-clinic-compact-final-native.png实际显示原镜头、五人完整入镜、无黑边、生命40/64/22与治疗按钮可读。拉远镜头试验虽不裁切人物，却暴露原背景高度外黑边（recovery-clinic-zoom-rejected-native.png），已撤回镜头/边界改动，改同伴-340/-540及半夏-170的局部站位。全段恢复与旧StoryService回归通过；27训练规则/维生场/风火规则、两仓diff和网站构建通过（既有v-producer警告），原用户档哈希未变。2-10以后及三章完整验收仍未完成，目标继续active，未提交推送。


## 2026-10-03 原2-10遗迹寻人与阿岩数据回收

RuinsActorAnimations1791012009（ruins-original-actor-animations.txt）确认vika/vivi无攻击轨，仅原移动/待机/特殊待机，ayan lose完整1秒，Ni throw完整约1.067秒、攻击事件约0.5秒。双胞胎共用vikaFigure的两个look为原UI已支持，原Q版与姓名映射复用；程序攻击补足缺失而不套别人的骨架。RuinsRoute1791012260（ruins-public-route-first.txt）原生首次PASS，范围见technical-design；含真实防护碰撞/完整动作、双胞胎实际跟随、两处写入故障重试、人物日记及实际数据流，不是全部鼠标游玩。新增日记正文标工作稿、来源为原人物身世。

初轮回收后画面ruins-after-data-recovery-native.png可见五人和红色返程方向，也发现停留后原45份金粉耗尽，补充沿路四处实际金粉采集与生命耗尽返回列车，不靠隐藏无限生命维持路线；后续专项验证真实剩余金粉。发现前锁住阿岩方向；原现场角色间距另作检查。30219正常退出确认无进程→30803新进程，正在验证真实双胞胎会面中途安全点与完成终态。

补充审计：旧RecoveryFrame1791011876虽打印PASS，但原生Group.each回调内assert报错被引擎捕获，报告不能证明镜头断言。改在回调外断言，并等待镜头跟随收敛；最后截图本身仍可见五人，新的可靠断言须独立复验。既有证据不删除，明确该层失效。

小饕餮再次对照原需求表原生复验：EnemySkills1791012987（small-taotie-current-design-recheck.txt）五招逐项PASS；EnemySkillCycle1791013036（small-taotie-current-auto-recheck.txt）正常AI自动五招PASS，无手动选招、前摇/命中/结束有序、无攻击重叠、恢复idle。保留原横击退、无击退、纵击飞、路径群体一次击退及炸弹碰撞范围无击退；27项训练规则通过。

遗迹画面审计：RuinsFrame1791012710的visible/speed断言不能证明骨架像素可见，ruins-ayan-body-native.png实际无遗体。AyanPoseCatalog原生截图ayan-original-death-fade-pose-native.png确认原lose在0.6秒跪地、0.9秒半透明、完整1秒结束全透明。修复不截断原死亡：先等待实际完整AnimationEnd，再用独立骨架采样0.6秒不透明跪地姿态作为持续现场遗体。RuinsFrame1791013097（ruins-body-frame-final.txt）及ruins-ayan-body-final-native.png确认现场实际可见阿岩、日记与五名同行者；原死亡结束/独立姿态采样均断言。该采样是遗体展示，并非战斗死亡改为只播0.6秒。公开遗迹全路线仍在复验。

最终全路线RuinsRoute1791013129（ruins-final-route-following-failure.txt）在检查阿岩入口等待超时：同伴原学院fmove/idle/turn采用2秒reaction，近距跟随出现持续过冲，四人不能同时满足45像素站位容差。只为遗迹四名实际同行者的动作实例设置reaction=0.05，保留真实移动、回收前集合和原0.2恢复；未修改全局战斗动作注册。最终全路线重新验收。

30803新进程中RuinsMidResume1791012537（ruins-twins-checkpoint-after-native-restart.txt）从真实双胞胎完成安全点接续PASS，不重复脉冲/41行，实际后续步行与发现7行/人物日记7行/回收8行及事务重试、剩余金粉/药品/模型保留。此前1791012430失败是测试脚本缺少local f，记录ruins-mid-resume-first-test-failure.txt，修复后重跑。RuinsCompleteResume1791012641（ruins-completed-after-native-restart.txt）真实完成副本从Start/原门路/编队进入，四段完整重读，不重复攻击、遗体或数据流，奖励一次。两项早于最终遗体淡出修复与跟随response修复，后续最终源另测。

RuinsRoute1791013294（ruins-public-route-final.txt）最终源公开全路线原生PASS：原Start/物理学院站台与列车门路/第三项三卡部署、未发现时夜光镜拒绝泄露阿岩方向、真实脉冲/原throw防护、41行及会面保存故障重试、双胞胎实际步行、四处沿路金粉补给、阿岩7行、实际人物信息第四项日记7行、回收8行保存失败保持遗体且无数据流、成功后1.4秒真实数据流至手边及移除遗体。四奖励各一次、原两学员模型与六份药品保留。没有引擎回调内断言吞掉的错误。RuinsOutcomes1791013410（ruins-life-support-evacuation-final.txt）明确低生命/零金粉夹具，真实维生场伤害耗尽→实际TrainA撤离，不增加剧情奖励PASS；非正常公开路线自然死亡。

诊疗镜头可靠复验：RecoveryFrame1791013431（recovery-clinic-camera-math-failure.txt）回调外断言失败，但真实截图五人均在画面。原计算世界x减camera.x忽略Platformer图层变换；改用Unit.convertToWindowSpace异步投影每人左右130本地边界，收集十个投影点且确认五人数量，再在回调外检查实际窗口范围。RecoveryFrame1791013523（recovery-clinic-projected-final.txt）原生PASS，recovery-clinic-projected-final-native.png实际五人/40、64、22伤后生命/接受治疗完整可见。投影缺回调也会超时报错，不以被吞回调错误产生PASS。遗迹Frame同样改实际投影验收。

最终源完成副本RuinsCompleteResume1791013573（ruins-completed-final-source-replay.txt）原生PASS：原Start/公开站台列车部署、四段完整重读、奖励一次/模型/六药保留，不重复攻击/遗体/数据流；实际切回原TrainingRoom检查林消息以后不再生成阿岩/旧训练后交谈终端。此次为同进程最终源复验，之前30803新进程恢复结果单独保留。RuinsFrame1791013646（ruins-body-projected-final.txt）最终真实跟随响应与12个窗口投影（五名同行者及遗体左右边界）原生PASS，ruins-body-projected-final-native.png实际六角色/日记/可用检查按钮/伤后已翌日100生命入镜。StoryService1791013675（story-service-after-ruins-final.txt）剧情前置、回滚、重读、幂等、未来版本只读保护再PASS。27训练规则/改动Lua语法/两仓diff检查通过，网站构建只有既有v-producer警告；原用户lsd.db哈希760372bda8ae788c451e95bc169ccddd6b5837cee36fe9101b330efd4f7e3d39保持。2-11/2-12及第三章、全新档全流程鼠标验收仍未完成；全三章目标active，没有提交推送。

## 2026-10-03 原辅助机分件模型与冒险动画

用户指出原素材存在，定位到 machine.md 中周大西三套透明分件原图（1200×992、1200×982、1200×622）；修正技术文档“未发现辅助机独立美术”的遗漏。原图逐字节复制到游戏 Image/Auxiliary，三份 SHA-256 与源文件、manifest 一致。新增可重建的原生 clip/model 关节和九时间轴，各机9/13/8个零件；原生遮罩只保留实际零件，剔除矩形裁切夹带的邻近分件，不修改或重绘 PNG。防御机舱盖修正为待机闭合，采集/运输时真实开合；关节层次修正避免遮罩重新挂载改变绘制顺序。

替换既有 Ground.SupportView 的简易车体，接入真实金粉、机体损伤、光学迷彩、维生场、传输粒子、火花及悬浮尾焰。终态保持最终姿态而非循环；断能/毁坏时实际 support.x 停止跟随，物理受击机体使用同一个坐标。补给时先恢复 speed 再启动，以免零速度下计算出无限恢复时长。三个型号由原列车 UI.Formation / UI.Button 选择并带入城市、能源战和遗迹；未改虚拟摇杆与技能操作。型号数值差异、完整背包、工厂维生负载和跨平台仍未完成，详见 auxiliary-machines.md。全 Game 0 目标保持 active。

AuxiliaryAnimations 最终原生 PASS：三机共27条完整时间轴、各3次采集/护盾事件、recovery=0.2。AuxiliarySupport 最终原生 PASS：实际一次采集、完整动作结束、迷彩、受损、断能停位、补給重启与摧毁终姿；不是正常游玩自然死亡证据。早期公开路线已实际鼠标选型/进入城市并完成拾取/受损，末项误在world查找HUD失败；保留 auxiliary-route-hud-lookup-failure.txt，改查实际ui3D并另做最终复验。预览曾用无size的UI节点导致画面出界，已修正bufferSize并原生重看，不能将旧逻辑PASS冒作旧截图合格。

本轮另已准备原2-11遭袭五行与2-12苏醒三十二行数据、任务与日志入口，以及原山魈动作/姿态探测；这些是数据预备，尚未接入真实追击战及桃源谷可玩流程，不能宣称2-11或2-12完成。

公开 AuxiliaryRoute1791014997 最终 PASS：已赚取列车档副本、真实门路/原编队界面、原三机预览、鼠标点击开始、装备机型号随出征进入原城市、原HUD、一次拾取事件及真实机体生命18损伤后的完整动作。鼠标切换三型号的额外原生截图检查来自前一轮，最后重跑保留装备机并鼠标开始。原生截图为临时保持显形的美术检查状态，默认游玩仍启用迷彩。

GroundBattleOutcomes1791015087 PASS：既有撤离/真实致死近战/原大饕餮实体子弹摧毁辅助机；第三例携装备机负载，型号保持、原lose完整结束并speed=0、救援锁定/无奖励/训练成果保留。EnergyOutcomes1791015106 PASS：旧双学员模型与原子编队、真实致死攻击、原炸弹摧毁悬浮机、完整lose终姿、撤离无奖励、两模型未改。终态测试采用显式低生命机体夹具，未称正常游玩自然死亡。

三种机体继续补齐移动朝向与原生遮罩随变换；悬浮机悬空高度和四足机后腿关节连接/足底位置按真实地面修正，能量核和尾焰随机体显示高度对齐。StoryService1791015195 与 MissionService1791015229 原生旧门路、事务回滚、重读一次、终态冲突及未来版本只读保护回归 PASS。TrainingContract27 / GroundLifeSupport / WindFireContract 与两仓diff检查通过；Sphinx构建仅保留已有v-producer警告。原用户lsd.db哈希仍为760372bda8ae788c451e95bc169ccddd6b5837cee36fe9101b330efd4f7e3d39，未提交/推送、未使用重置卡。


## 2026-10-03 返程追击与桃源初见

原2-11五句对白已通过实际返程入口接到追击战，旧左侧返程入口在阿岩数据回收后也进入同一流程。四名同行者为真实实体，向安全方向实际步行；导师使用原摇杆、射击按钮与原技能UI释放烟雾、火光，烟雾实际拦截投射物、火光实体碰撞使追兵暂缓。胜利要求四人撤离、三个真实路线点、射击与火光命中、烟雾及火光完整动作结束，不能对白结束即传送。原稿未指定强敌种类，原大/小山魈资源及三招参数是本轮实现选择。技能使用原throw攻击事件，怪物无原攻击事件，攻击点据原姿态目录设置；更广的六招逐帧时序及失败/故障恢复验收仍待补。药品使用服务已写，尚未声明库存故障与战斗使用验收通过。

Pursuit1791015814 PASS（pursuit-public-first.txt）：真实已赚取遗迹档副本，实际返程入口、原五句、原HUD、实体火光/射击、两工具完整动作、四实体步行与三个路线点、训练模型不变。20.56秒、导师生命51，烟雾拦下一枚投射物且阻止两次攻击。开头进入遗迹位置采用检查点加载，不称从全新开场走完；操作为引擎原UI事件与玩家输入，尚非全鼠标游玩。第一次本地误发Skill.Began未触发射击的FAIL保留。

桃源原OuterHeaven、原万薇莉、原小山魈接入；Start根据真实追击奖励继续到桃源，未把撤离学员凭空生成在谷中。原32句初见对白、完整fall/standUp、饮水/喂食comp、实际步行和骑乘表现、原探索音乐、原创合成鸟鸣流水与动态花瓣已接入。Valley1791016290 PASS：真实追击完成副本经Start进入桃源，32句与三演出完整、重读不重复物理演出且奖励一次。音频句柄成功只证明启动，尚不证明听感验收。藤蔓吊床和骑乘属于程序演出，未新增专用竹筒/紫砂杯或骑乘骨架；后续五种活动、数日后怪物交流/狐狸身世、2-13及第三章仍未实现，不宣称整段2-12完成。

实机发现并修复：空decisionTree名称不会清掉旧原生决策树，改用明确Reject叶防止漫游AI打断苏醒；原Grab容器必须保留playable原坐标；不存在MoveY调用已改为实际插值。异步对白刷新前即时锁住下一句，同时保留Command等待锁，修复动画结束与连续确认重叠时跳过原骑乘句。各失败报告独立保存，不覆盖为成功。最终画面与共享对白回归另外记录。

Valley1791016342 最终站位修订后再PASS（valley-original-encounter-final.txt），小怪在喂食后实际挪开避免被万薇莉遮挡；valley-awakening-final-native.png 已核对原桃源、两人物、友善小怪、吊床与花瓣。Start/Story/OuterHeaven 三份Yue独立编译和生成Lua语法通过；全Script/UI/Test Lua语法、27训练契约、维生规则、风火契约、两仓diff检查与网站构建通过，只有既有v-producer警告。原用户lsd.db哈希保持760372bda8ae788c451e95bc169ccddd6b5837cee36fe9101b330efd4f7e3d39；没有提交或推送。

共享对白更新后StoryUI1791016385 PASS：原学院物理路线、研究/邮件/暗格原Yarn、保存故障公开重试与重读恢复。StorySupplies1791016476 PASS：原已赚取六药独立副本实际消费、事务故障不扣、空库存拒绝、重读不补给、重新打开一致与未来版本只读。修正导师别名到原charM/charF库存键（首个失败报告保留）；此结果不冒称追击中药品回血实战已验证。


## 2026-10-03 追击结算闭环与桃源五活动

PursuitOutcomes1791017050 PASS（pursuit-six-attacks-and-outcomes-final.txt）：真实已赚取遗迹档副本、原五句完成采用显式服务夹具，真实原生大/小山魈六招完整、攻击点、前摇无伤害/投射物、同敌不重叠、0.2恢复；高生命与距离为时序测试夹具，不冒称自然通关。随后原HUD实际药品使用验证保存失败不扣不回血、成功减一并70→95、空库存不回血；低HP夹具真实投射物击败导师、公开重试、撤离事务故障公开重试、中断安全恢复，再用真实射击/火光/烟雾和摇杆赢得追击，奖励故障回滚、原结算重试一次、胜利按钮实际进入桃源。训练模型不变。修复敌人攻击后下一更新立即追击覆盖恢复姿态的问题，冷却0.65秒先保持idle；各测试夹具边界和加载等待失败报告保留。

原2-12五项活动实际接入原OuterHeaven，复用UI.Interaction、UI.Skill和原摇杆：鱼塘需靠近浮出水面的鱼抓住时间窗；三道田垄按播种/浇水/生长5秒/收获；三树驻足2.5秒后记录；两只野鸡根据玩家位置逃跑，靠近收拢入栏；语言需静心3秒并完成三次含义选择，错误清空静心时间不给奖励。地点/数值/奖励物品是改编细化，非原稿精确数值。新增原生矢量鱼、田垄、桃树、野鸡/围栏，原小怪保留、恢复已相识状态后可见并实际跟随，万薇莉真实原人物步行同行。

ValleyActivities1791017114 首次公开玩法PASS（valley-five-activities-first.txt）：真实已完成初见档副本经Start续玩，五个实际地点、原UI事件、真实步行/时间窗/生长/驻足/追逐/答题、原人物完整comp动作、语言错误不奖励、最后奖励事务失败重试、五奖励一次、实际万薇莉跟随与重新加载状态保留。该报告为首次实现，最终新增后续对白及画面修订另验。ValleyStore1791017354 PASS：真实初见副本的显式服务进度夹具验证未学语言不可休息、播种/浇水的中途持久化、未完成无奖励、进度不回退/非法状态拒绝、奖励原子回滚与幂等、未来版本只读；不替代实际活动路线。

新增原24句数日后的怪物交流/大狐狸身世与原“几天之后”显示，未混入2-13对白。语言活动完成才可回吊床休息，完整fall/standUp及昼夜切换屏幕；原dahuli实际move进场后idle，怪物/狐狸无独立Figure资源，保留原姓名文字并使用场景原骨架表现，不伪造缺失肖像。ValleyDays1791017299 首次PASS：真实五活动已赚取副本、实际吊床、完整动作/原日后文字、存盘故障重试、24句、狐狸实际移入、原日志第11页重读无重复演出/奖励。发现Yarn首条异步Command被构造器清掉等待锁，已修复Lua/Yue一致；首个失败保留。最终说话者与整段回归另记。

完整Game0目标仍active：2-13狐狸带路/食物/万薇莉跟随、第二章其余段与整个第三章、全新档全流程/最终美术声效及多平台验收仍有工作，不把本轮子段结果扩展成整部作品完成。

## 2026-10-03 原辅助机最终图稿修订

上一轮时长/状态测试通过，仍不足以证明拼装完全忠于最终图稿。用户指出局部拼接和遮挡错误，并明确装备机右侧和后侧挡板在设计图中为展开状态，游戏待机应闭合。本轮对照原整机与分件重做位置/前后层：护盾机去除重复盖片与圆灯，补履带纹理、观察窗、侧关节；装备机补连接臂/四脚并校准侧箱，把显示面与后侧壳分开；悬浮机去除重复推进器，补前壳/导管，把前端组件拆成机身后侧与前传感器。分别17/19/12组件，原PNG字节不变。

装备机两挡板采用下滑闭合常态，仅collect/carry完整开合；滑动行程属于制作细化，关闭常态遵从用户要求。四个脚掌按原关节生成位置和转角，避免独立摆动导致脱节；迷彩由完整组件清单驱动，并校准采集/受击光点。Test/AuxiliaryAssembly为同尺度原稿/游戏姿态对照，可用原输入按钮和慢放检查运动。原图参考展开姿态与游戏闭合常态分别展示，不强制把图稿展开状态当作待机。

最终源27条原生时长与各一次模型事件通过（auxiliary-reassembled-durations-final.txt）；新组件迷彩、真实采集一次、受击、断能停位、补能完整重启、摧毁终姿通过（auxiliary-reassembled-support-final.txt）。AuxiliaryJoints首轮验证两个挡板闭合待机/完整打开/结束时关闭/恢复保持关闭，以及四脚真实关节跟随，最大误差0.0845像素；最终源复验及原生鼠标/截图另补证据目录。文档构建通过，仅既有v-producer未加入toctree警告。

本轮优先处理用户纠正的辅助机质量问题，2-13原策划已核对但尚未实施；完整Game0目标保持active，未将这次模型修订当作全作品完成。

收尾复验：auxiliary-joints-final最大误差0.0845像素、两个挡板完整开合且恢复关闭；AuxiliaryRoute1791019112原生PASS，真实列车门路/鼠标选型与部署/城市实际拾取与受损/原HUD通过，未称全鼠标步行。原生对照入口的缩放按钮改用外层容器，避免原InputButton点击动画将预览按钮放大；为护盾机开盖预留画面空间，最终同屏闭合及连续慢放三帧均已保存。PNG与用户原存档哈希未改。


## 2026-10-03：原2-13狐狸带路、食物与据点侦察

前一轮辅助机挡板原生复验通过，目标保持active。本轮接入原2-13完整22条非空原文和无对白夜光镜操作，拆为四个有物理入口及持久化边界的节点；原工厂路线采用导师/狐狸/万薇莉，未把原砗磲贝任务同伴混入。桃源走近狐狸出谷、真实跟随与等候、完整comp后食物原子消耗、万薇莉由隐藏同行者实际走来、第二段实际7.5秒、原Phone第三项三秒位置收集/收集完毕、三人实际撤到开阔处和返回指挥室均接入。数量/坐标/体力/时间参数及阿岩一份预留口粮作为新增改编登记于fox-trail.md；不拿文字存档代替实际路线。

FoxTrailRoute1791020237 最终源PASS（fox-trail-route-final.txt）：从真实桃源后续档复制，出谷/食物/侦察故障逐一验证原子回滚及公开UI重试；食物失败不重复动作；全22原句、真实万薇莉登场、5–10秒第二段、原夜光镜及完成提示、原指挥室、四段跨房间日志重读、食物一次且六药保持。首轮SQL[]参数及实体延迟构造失败单独保存，不冒称首次就成功。

FoxTrailMidResume1791020291 PASS（fox-trail-mid-resume-final.txt）：复制真实休息完成时的数据库，经Start恢复工厂2600/第二段/万薇莉，重读13句无食物或登场重复，未来schema99拒绝读取该功能和写入。正常退出33966、doctor启动35141后，FoxTrailCompleteResume1791020177 PASS（fox-trail-complete-new-process.txt）：原Start恢复指挥室/狐狸/万薇莉，跨房间侦察重读不再打开地图，奖励/食物/药品/解锁不变。中途最终源为同进程切换测试；不把它误称第二次独立进程重启。

Start.lua/Yue分支一致，Yue独立编译通过；全Script/UI/Test共301份Lua语法及两仓diff检查通过，网站构建仅既有v-producer toctree警告。原用户lsd.db SHA-256保持760372bda8ae788c451e95bc169ccddd6b5837cee36fe9101b330efd4f7e3d39。狐狸显示比例及同伴距离/文字底色根据原生画面修订。完整Game0仍未完成：原2-14指挥室分工、2-15至2-17、完整第三章、全新档连续模拟游玩及最终美术/音频/多平台验收仍需推进；没有提交推送或发布。


2-13真实鼠标检查补充：首版事件驱动测试全部通过后，实际鼠标发现Story对话层遮住原行动按钮。已修复为操作Command期间收起对话、恢复原View尺度/后处理，使食物/夜光镜按钮与撤离摇杆可以实际操作；完成后恢复对白。狐狸停步在玩家标记前方300单位，第二段保持1500实际移动/7.5秒。FoxTrailRoute1791020458最终修订全流程再PASS（fox-trail-route-after-mouse-fix-final.txt），MidResume1791020524再PASS，旧StoryService1791020517全部回归PASS。正常退出35141并启动35597后，CompleteResume1791020553最终源新进程PASS（fox-trail-complete-final-new-process.txt）。最终真实鼠标操作另验，不能用首张运行时诊断截图冒称最终源通过。


FoxTrailMouse1791020573 最终原生鼠标PASS（fox-trail-mouse-final.txt）：最终代码无运行时修改，实际赚取的休息档从Start/原实体输入到据点，之后CUA鼠标实际点击行动、确认原句、打开夜光镜、第三项收集、看到“收集完毕”、关闭地图；实际收集3.0157秒，最终DB读取证明fox-trail-scout提交、食物仍只消耗一次。fox-trail-checkpoint-final-native.png与fox-trail-collected-mouse-final-native.png核对三名角色分离、统一UI、状态底色及原Phone完成提示。该过程不是新档三章全流程，2-14及后续任务仍未实现；目标保持active。


## 2026-10-03：原2-14指挥室归来与分工

上轮2-13真实路线、恢复与鼠标验收已完成，属有效进展；本轮继续原2-14，完整28句Yarn、原9个人物骨架和狐狸、实际中央集合点与统一UI接入。原姓名/原Figure映射保留，包括烛参/烛商与原moyu半夏、moling忍冬；不伪造狐狸和众人的独立肖像。最初全景镜头露出原场景外黑区，已按实机观察调整为原房间zoom1.6、跟随玩家漫游；角色沿房间分布，并非11名同屏。中央菜单抬高避免人物遮挡，未汇报时显示分工前置提示。

Game0StoryAssignments新增十项职责，汇报节点/解锁/全部职责在同一事务提交。原Phone四分类查看、日志第12页第3项重读、普通导航返回角色恢复和旧任务/编队入口保留。旧Formation骨架改为单项顺序加载，避免已知原生共享解析器并行加载风险。Story.canRead对缓存服务重新检查StoryMeta，未来版本不能继续写剧情/职责。

CommandAssembly1791021201 最终源原生PASS（command-assembly-final.txt）：真实2-13完成档副本经Start，实体走到中央、原28句/姓名、先汇报才分工、十职责事务原子回滚/原保存重试、原Phone四组、日志重读一次、旧原Formation及返回、两训练模型/药品/食物/原任务表全部不变。首次恢复测试1791021100错误请求Game0TrainingWuyun；真实表是Game0Training_wuyun，测试已改正并1791021106原生PASS。新进程及最终鼠标证据继续单列，不以本轮普通对话冒称2-15战斗完成。

原11句关于万薇莉编程的后续描述本轮保留在对白及岗位记录中；没有新增独立计算机操作室或专用编程动画，不冒称完成该岗位的工作模拟。2-15潜入、三次制服/拦截、狐狸隐蔽带路、乌云留下看守、七层金属门/开门声/原信标与发射炮争论、实际阶梯攀爬，以及2-16/2-17和完整第三章仍需继续。完整Game0目标保持active，没有提交推送或发布。


### 2-14最终画面、实际鼠标与新进程恢复

本轮先按用户要求复验装备机闭合，原生关节测试和鼠标装备舱结束闭合均通过。继续2-14时发现zoom1.6仍有背景空白；单独收缩镜头边界又露出底部空白，最终恢复原场景zoom1，中央菜单锚点200/比例0.32/横向-60，避免与原导航、人物姓名及头像重叠。实际鼠标发现首次直接挂ui3D的“先汇报”提示虽visible=true却未渲染，改为原导航同样的buffer尺寸UI容器，窗口变化重新布局，场景退出清理。最终原生截图证实提示可见、菜单位置正确，未修改原场景作者素材。

CommandAssemblyMouse1791021790最终源实际鼠标PASS：已赚取2-13副本由原Start及实体输入到中央，CUA点击未汇报分工提示、汇报、原28句确认、四类原Phone分工和关闭。最终数据库十职责/剧情/解锁已保存，其他表逐一与鼠标前快照相同；没有运行时补丁、没有全程鼠标移动或全新档通关的声明。command-assembly-prerequisite-final-native、report-final-native、duties-final-native三张截图分别保存。鼠标准备入口仅负责到中央，不自动冒称PASS；独立核对脚本随证据保存。

CommandAssembly1791021908最终菜单/提示修订后完整原生PASS，涵盖保存失败原子回滚/重试、十项职责、28原句/姓名、四分类、日志、旧Formation及返回、全部原数据保持。过程1746仍运行时被切换入口中断，未计作通过，过程说明单独保留。旧StoryService1791021692回归PASS。普通恢复1699已过；随后CUA正常退出36299（观察接口超时，pgrep实际确认进程不存在），doctor确认Native engine:no并启动36929，CommandAssemblyResume1791021982最终源新进程PASS。完整Game0目标仍active。

2-15原生素材盘点InfiltrationAssets1791022010通过六套资源加载/动画和look枚举，实机图确认shujuyuan是人物而非物资；只有fmove/idle/idle1，缺制服/受击/倒地。Factory仅室外层且无金属门动画；LoopTowerA有原坡道碰撞与openR，但不是七层控制舱，不能把原教程楼当作已完成工厂楼。charM/charF是原主角，不能直接冒称专用守卫。详细拆分和缺口追加roadmap。2-15战斗尚未实现。

最终检查：307份Script/UI/Test Lua语法通过，两仓git diff --check通过；文档网站本地Sphinx构建通过，仅既有v-producer未加入toctree警告。用户lsd.db SHA-256仍为760372bda8ae788c451e95bc169ccddd6b5837cee36fe9101b330efd4f7e3d39。网站未发布、变更未提交推送。


## 2026-10-03：首波巡逻实战与九尾狐队友纠正

PatrolGuard1791022995和PatrolBattle1791023013最终修订通过，完整攻击/倒地、物理伤害、已采用双学员模型、真实火焰与旋风均有证据，详见[工厂潜入](factory-infiltration.md)。首波仍是独立验证入口，不宣称完整2-15或用户鼠标通关。

按用户纠正，桃源谷、Factory带路、指挥室恢复与集合的队友狐狸全部改为原策划双程Q-huli.png，新增FoxCompanion，原图字节保留。没有采用xiaohuli或缩小BOSS。CommandResume1791023110完成实际Start、原Phone与日志/普通导航回归；FoxMid1791023163进一步检查Q版资源身份、实际行进动画与停步恢复、原13句重读、食物不重复和未来存档拒绝。首次检查停步等待仅.3秒失败，实际狐狸会继续到玩家前方480单位，改为等待真实停步后通过，失败记录保留。Q版目前只提供原图整体起伏，真正分件步态仍待制作。

用户lsd.db哈希保持760372bda8ae788c451e95bc169ccddd6b5837cee36fe9101b330efd4f7e3d39。完整Game0目标保持active，网站未发布。


补充最终复验：原默认VR训练PatrolArenaRegression1791023310双学员各5次真实命中/模型动作、fallback0，通过；首波准备撤离/缺协同失败PatrolOutcomes1791023255通过，未声称导师阵亡路径已通过。Q版资源断言加入后CommandResume1791023752最终复跑通过。Q分件两版使用内置image_gen制作并保留提示；裙摆开口/颈部/胳膊修订后FoxRig1791023698原生12分件/四关节/完整动作/两step事件通过（最大接缝.01735），但画面轮廓尚未足够贴合原图，仍作为candidate，不用于替换游戏队友。原画显示与分件质量验收分开记录。

文档网站本地构建通过，只有原有v-producer未加入toctree警告；首次误用全局sphinx环境缺myst_parser，改回已有lsd-doc-planning-venv成功，没有改依赖。


## 2026-10-03：工厂公开首波与Q版动画研究

公开首波 InfiltrationRoute1791024317及同进程Resume1791024382通过，三处历史失败原因与原子写入重试见[工厂潜入](factory-infiltration.md)。真实CUA鼠标1791024448也已走过公开菜单、原Phone定位、统一三技能和结算、制服对白；逐表对比已赚取源档，其他旧表不变。公开继续/返回及Start断点接入已完成，完整2-15和新进程恢复尚待继续。

按用户要求研究原Q动画，三套Spine实际轨迹和原生九动作结束已取得证据，QMotion1791024941通过。新增[九尾狐动画研究](fox-animation.md)记录脚掌约束、两骨腿、肩肘节奏和头发/裙摆跟随。独立14分件动作候选 FoxMotion1791025146通过六关节、待机固定脚端、三动作原生结束与两步伐事件；形象和比例仍在修订，尚未替换正式原Q图。完整Game0目标仍active。


Q动画候选最终1791025839加入步伐时刻/落脚姿态断言与实际200单位/秒平移：六关节最大漂移.000714，支撑脚世界位置变化.000488像素。已独立拆靴子护甲/脚掌、修正比例并按世界位移计算动画倍率。失败的相位/时钟检查保留，未放宽滑步阈值。原图正式显示保持，后发/蝴蝶结/表情及长循环继续验收。StoryService1791025855回归通过，325份Lua及两份Python语法检查通过。


最后正常退出原引擎36929（pgrep确认无进程），doctor启动40426；InfiltrationResume1791025948新进程PASS，Factory2200安全断点、原Q形态、日志重读和全部表不变。CommandResume1791025875公开旧分支/Phone/职责/日志/普通导航回归PASS。引擎仓库无修改，两仓diff检查通过，用户档哈希仍保持原值。

Q动作最终源新进程复验1791025991通过，最大关节漂移.000401、支撑脚范围.000488；直接CUA画面对照确认候选尚有头身比例/后发/蝴蝶结差异，维持不采用。当前原生入口为Test/FoxCompanionMotion.lua（40426），无存档挂载。


正式显示高度300的原生生命周期1791027311通过：动画倍率1.553333对应200单位/秒实际平移；连续13轮行进产生26次step。暂停 .4秒保持脚掌姿态且无新增动作事件，恢复继续；实际改变位移方向与fliped后四轮循环、停步固定脚底、完整prepare的AnimationEnd后recovery回idle、重新起步三轮均通过，期间实时眨眼四轮。此为独立候选生命周期，不等于已完成剧情带路接入。日志为fox-lifecycle-native.txt，事件为fox-lifecycle-events.json。当前入口Test/FoxCompanionLifecycle.lua，进程40426，无存档挂载。正式队友仍使用原Q原图；高质量验收还需护甲/裙摆细化、表情贴片色差与实际剧情画面。


2026-10-03 Q版正式分件接入：v4原稿比例/六关节/完整动作/脚底/眨眼1791027409、真实Factory候选1791027501、完整原22行狐狸路线1791027531均通过。共享FoxCompanionRig保留原稿与候选，正式FoxCompanion切到15分件v4。FoxMovement按实际速度换算倍率，并因源码recovery/speed语义补偿为实际 .2秒过渡。正式Start恢复1791027609和带原生事件/速度/停步断言的1791027636通过。实际正式行进/停步截图已查看；原来的初始相机截图狐狸在画外，未用作视觉通过。337份Lua与9份Tools Python语法通过，用户档哈希保持760372bda8ae788c451e95bc169ccddd6b5837cee36fe9101b330efd4f7e3d39。完整Game0仍active，下一步继续完整工厂潜入及后续章节；尚未做本版新进程验收。


### 2026-10-04 控制舱与完整研发人员对白

公开第二波之后已接入独立七层旋转阶梯、带门锁声的金属舱门和可步入的舱内平台。三位研发人员的原 29 行已接原 Story/Yarn、持枪动作、Q 狐狸露齿表情、原子保存/重试、日志重读、重新启动恢复，并完成从第七层开门检查点开始的真实键鼠游玩。证据与迭代失败详见[工厂潜入](factory-infiltration.md)。狐狸按用户要求只调动画速度，恢复原移动速度。接下来是 ROOF_ROUTE_PENDING：实际阶梯攀爬、玻璃罩/发射炮与 2-16/2-17；Game0 总目标仍未完成。


<!-- preserved-progress-end -->
