# 开发历史记录 · 第 10 卷

> 2026-10-05 从旧进度页归档。以下为当时记录，含已被后续结果替代的状态，不作为当前待办。请从[当前进度](progress.md)或[历史索引](progress-history.md)继续阅读。

## 原始记录

<!-- preserved-progress-start -->
### 距离选招与人物受击、倒地、起身（2026-10-05）

大饕餮在配置机动速度的正式战斗中，按最近存活人物和当前距离选择可用招式：近距拍击、身后尾击、中距扑击、远距扫射/冲撞；没有可达招式时接近。接近使用480/560的停止/启动缓冲，场地边缘停止，不重启行走循环。技能选择后锁定本次朝向和目标选择记录，攻击期间不重新选招。固定设施不作为追击目标，仍可承受范围攻击。静态专项训练保留显式零速度配置。BossDistanceNative原生PASS：从1500距离真实前进约251后在1249处选择扫射；完整三连发未因目标穿到背后而转向；近、中、远、背后、死亡目标排除、边界和缓冲均验证。

用户追加人物受击/倒下/起身动画。CombatAnimation记录各角色原生动画能力；Combat.Displacement按轻重击使用“hit”或“hit→fall→落地→standUp→prepare/idle”。阶段以AnimationEnd和实际时长推进，不能由下一轮AI或重复受击重置；起身完成后恢复输入、原显示顺序和recovery。轻受击空中等待有2.2秒上限；倒地链等待实际落地再起身，整条异常控制有8秒兜底；正常起身按资源时长完成，不沿用此前固定1.5/2.2秒直接结束受控的行为。此链已接入大饕餮的位移攻击，扫射命中使用轻受击。其他敌人/关卡的伤害入口尚需统一接入，不以本项宣称全游戏已完成。

CharacterHitRecovery原生PASS，覆盖妮妮莉特、乌云、男导师、女导师：四者hit均约0.6秒，妮妮莉特/乌云fall约0.933秒，男/女导师fall约0.5秒；起身分别约1.10/0.833/1.20/1.133秒。逐阶段检查完整播放、落地后才起身、重复击飞不打断起身、轻击不倒地、最终prepare及显示顺序恢复。BossSkills完整五技能回归PASS。地面战报增加enemyTactics=1与hitReaction=2以区分规则；这些是规则标记，尚不等于C4.5/Q距离与受控特征升级完成。


### 小饕餮受击接入与控制保护（2026-10-05）

Training.EnemyCombat的五招有效伤害统一调用Combat.Displacement。保留小饕餮原有击退/挑空数值，普通攻击和炸弹也播放轻受击；小饕餮现有力度未达到重击倒地阈值，不人为让每次轻击都倒下。吸收全部伤害、固定设施与致命命中不触发新受击链。新增各关卡人物存活回调，避免伤害函数已播放lose后又被hit覆盖。

学院防守、双子撤离、最终护送、警戒任务、虚拟合作训练的导师控制与自动跟随尊重受击保护，结束战斗清理状态。导师底层动作available也检查受控状态。跟随恢复依据实际当前动画切回行走，避免受击后旧缓存仍为fmove而出现滑行。虚拟训练的对打伤害入口仍待统一，工厂花妖也未在本轮接入，不能声称全敌人覆盖。

EnemySkills原生PASS：五种攻击完整播放、命中后真实hit完整播放、物理击退与挑空、炸弹多人命中、滚动每目标一次和城市场景完整滚动均通过。DefenseEnemyTiming原生PASS：五招各自覆盖战败和撤离，共十种情境，完整攻击/lose且失效攻击不伤人。HitReactionGuards原生PASS：真实Unit验证零伤害、固定目标、致命命中不触发受击，学院/警戒/虚拟训练的移动指令不覆盖hit，完成后恢复待机。证据位于Docs/evidence/2026-10-05的enemy-hit-skills、defense-hit-timing和hit-reaction-guards。测试未读取主存档；尚未重跑三个完整护送关卡的胜利流程，训练数据的距离/受控特征和规则迁移仍待继续。


### 虚拟对打受击与花妖规则迁移盘点（2026-10-05）

Trial.Battle对打的导师、莉耶娜有效命中新增原生hit；格挡成功、零伤害、战败后不触发受击，致命伤害保留lose。被受击实际中断的攻击记录interruptedAt/reason=hit，不再误当完整释放。damageHero统计实际扣除生命，避免过量伤害膨胀训练报告。

TrialHitRecovery使用真实VR场景、导师和莉耶娜、正式动作与弹丸：格挡保护、莉耶娜攻击被中断、双方受击后恢复、实际射击命中触发hit、受击期间拒绝移动、致命伤害保留lose均通过。服务为无数据库测试桩，不能据此宣称剧情持久化已回归。证据trial-hit-recovery-result.json/process.log，未读取主存档。

花妖尚未接入：FlowerCombat的twine波与常规impact均有明确伤害入口；Effects的pull、confuse/virus和Factory.Battle无目标自动待机可能覆盖受击。改动需同时处理这些优先级。训练规则目前记录bossScale/aimPolicy，尚无hitReaction字段；FlowerPractice、FlowerQSession应写入版本，FlowerAdoptionStore、FlowerTeamReview、FlowerAdoptionPanel应拒绝使用旧规则直接采用或部署，历史记录仍可查看及回滚。FlowerQStore/Trials必须保持旧链可读，明确新旧规则不得混用于当前比较；完成后需重新生成四场景基础/候选对照及正式工厂战斗验证，不能用原评估结果代替。


### 花妖受击及新版规则评价隔离（2026-10-05）

FlowerCombat的吸血、普通攻击和藤蔓直接伤害接入原生hit，仅有效伤害触发；牵拉继续按原技能移动，持续毒伤不反复打断角色。Effects状态施加、吟唱请求与Factory.Battle自动待机尊重受击控制，结束战斗清理受击状态。六种花妖技能专项原生回归通过，原有吸血、多人牵拉、毒/混乱、病毒真实友伤、繁殖与乌云完整吟唱保持正常。

新增Factory.Rules，当前hitReaction=2。正式战报、C4.5专项试战与Q训练/试战均记录版本；读取时要求setup与episode.versions一致。C4.5单人与联合采用、Q采用与部署要求当前规则，历史档案仍可重建及回滚。Q当前评价按明确版本选取记录，展示排除的旧规则场数；档案回读按照档案自身版本重建，旧档案不补写新版本。新的审查仍冻结全部数据库行，避免读写期间来源变化。

FlowerReactionMigration原生PASS，使用命名QA副本：旧采用#2可读、17场旧Q试战可读；旧规则直接采用/部署被ENCOUNTER_CHANGED拒绝，未改变指针；一场新版near候选自然获胜并保存；当前评价只计新版1场，保留并注明17场旧记录；伪造setup版本与日志不一致被拒绝；旧档案回滚成功且历史保留。新四场景对照、重复试战及稳定收益仍未完成，不推荐自动采用，也不把本项视为距离/受控学习特征升级完成。证据flower-reaction-migration-result.json/process.log。

补充验证：FlowerSkills新增直接命中hit阶段时长断言后再次PASS，确认状态施加没有截断受击。FlowerReviewColdRead原生PASS，三个C4.5历史采用档案仍可重建，旧确定性汇总保持一致；证据flower-hit-c45-history-result.json/process.log。文档构建通过，仅已有v-producer未列入toctree警告。


### 距离与强制动作的原始证据采集（2026-10-05）

新增Combat.Spatial v1：花妖决策快照附带人物世界坐标/速度/是否着地、Boss中心相对向量、最近存活敌人的中心距离与攻击阶段/技能、最近存活队友距离，以及hit/fall/standUp、牵拉和精力耗尽状态。距离明确为身体中心距离，尚未当作Boss身体边缘或武器有效射程。历史分类特征版本6及Q键保持原义；新字段目前为补充原始证据，尚未进入C4.5分类字段或Q状态键，后续需显式版本迁移。

人物受击阶段和花妖牵拉通过独立事件表记录来源、技能、模拟时钟、位置和当时速度，origin固定为forced。hit/fall/standUp记录实际进入阶段的时间，不伪造为玩家示范或模型决策。事件表上限4096，达到上限明确标记movementTruncated；不静默丢弃。Journal快照保存事件，CombatStore按spatial版本校验决策快照及事件时间、来源类别和数值。

FlowerReactionMigration再次原生PASS：真实获胜局保存178个决策快照及25条强制动作事件，Q存储/回读、旧17场隔离、历史采用回滚均正常。CharacterHitRecovery再次原生PASS：四名角色完整hit/fall/standUp，每阶段来源记录与严格递增模拟时钟通过，恢复后快照为free。只使用QA副本，未访问主存档。

SpatialEvidenceRead原生PASS：从QA数据库冷读上述真实178决策/25事件，用最新校验器通过；删除位置快照、负距离、把forced改成demo、负事件时间均被拒绝。证据spatial-evidence-read-result.json/process.log。


### Boss实际轮廓距离与共享枪械航程（2026-10-05）

HitGeometry新增到启用多边形并集的最近点距离，凹形部位不当作包围盒，内部/边界返回0。Spatial v2采集人物中心到Boss实际动画命中轮廓的距离/最近点/部位，以及实际枪口到命中轮廓的最短距离。复用PartCombat当帧采样缓存，未另造缩小碰撞体。记录的距离是点到Boss轮廓，不声称已经扣除人物自身碰撞体半径。

Combat.FirearmRules统一现有导师实弹与学员弹丸的速度2400、存续1秒，航程由二者相乘得到；PartAim的范围检查与记录使用同一来源，物理数值不变。withinTravel只代表最短几何距离在弹丸航程内，不代表面朝正确、指定部位可见、无地形遮挡或未来必然命中。原PartAim与实际碰撞仍负责这些条件。

SpatialGeometry纯几何测试通过：边/角最近点、内部/边界0、禁用区域、凹形和多个部位最近选择。PartAim回归通过朝向、角度、部位/地形遮挡、枪口在体内和超出2500距离的拒绝。Spatial v1历史仍可读，v2按记录版本校验，不能把v2快照标成v1。下一步仍需把距离分档接入新版C4.5/Q状态及自动站位决策，本项本身不改变策略。

原生FlowerReactionMigration与SpatialEvidenceRead均PASS：获胜局221个决策、39条强制动作、56次枪口航程观测，Boss轮廓距离显著区别于中心距离；冷读拒绝负枪口距离及spatial版本错配，旧Q档案/17场记录继续可读。测试使用命名QA副本。


### C4.5距离与站位特征进入学习（2026-10-05）

新增FlowerTacticsFeatures投影，C4.5新候选featureSchemaVersion=7，基于当时spatial v2增加六个分类输入：bossGap（未知/接触80以内/近300以内/中650以内/远）、allySpacing（无存活队友/小于160拥挤/360以内支援/孤立）、threatDistance（最近存活敌人中心距离）、threatActivity（是否处于攻击阶段）、shotReach（未知/航程内/航程外）、control（自由/空中/受击/倒地/起身/牵拉/精力耗尽）。shotReach不表示无遮挡或保证命中，威胁距离仍明确采用中心距离。

新学习只收录带spatial v2的完整示范，旧示范保留并在界面注明未混入新版学习；不足六个新示范时提示补充。原始战斗观测仍保持版本6及独立spatial版本，Q的旧状态键本轮未改。C4.5模型版本7在预测时从原始观测投影；旧版本6继续按原字段预测与重建，并拒绝偷用新版条件。FlowerEvidence增加与模型版本绑定的flower-c45-v2构建标记，版本6证据显式按v1重建，历史数据不改写。

FlowerSpatialPolicy原生测试使用命名QA副本，通过正式对练请求采集12个完整移动/等待示范，经原生C4.5构建、保存、证据重建得到版本7；旧版本6候选也成功重建，缺失距离证据的版本7预测被拒绝。测试示范由QA驱动，不等同真实玩家示范，也不是推荐采用的有效战斗策略；本轮没有采用或修改正式成果。四场景对照、Q版本迁移及自动站位仍待完成。

复验PASS：上述12个实际示范构建的树确实包含allySpacing条件；另以只改变队友间距的合成样本调用原生C4.5，得到crowded后退/isolated前进的不同预测，拟合率1只用于分类合同验证，不宣称实战收益。证据flower-spatial-policy-result.json/process.log。


### Q距离状态升级与来源链保留（2026-10-05）

FlowerQ支持featureSchemaVersion 6/7，版本7使用与C4.5一致的六项空间/受控分类，原始观测仍为版本6+spatial v2。Q实例的状态键按自身版本生成，读取压缩键时校验对应字段数及分类值，不能只改版本号挪用旧值。版本7缺少完整空间证据则拒绝预测/学习。

新的探索使用版本7。继续旧版候选探索时，新建版本7状态表从本轮轨迹学习，不将旧表数值硬填到新键；旧模型、旧来源链和采用档案保持不变，新来源以旧候选为不可变父版本，保存initial及qFeatureVersion供重建。界面明确提示升级状态及需重新评价。旧Q来源按自身版本重放；不支持降级或混合两名角色的模型版本。

Q试战setup新增qFeatureVersion。当前评价/采用需当前受击规则及状态版本7，旧评价保留但不混入新版统计；历史采用档案按归档的版本重建，旧档案继续可读与可回滚。直接探索仍不会改动已采用指针。

FlowerSpatialQ原生PASS，使用命名QA副本：从旧候选继续一场实际探索并自然获胜，妮妮莉特149次/乌云127次更新，产生候选#3；序列化重建结果与运行结果相同，父版本模型完全保留、旧采用#2可读且未替换；队友间距在v6得到同键而v7不同，改模型版本号或缺失空间证据被拒绝。该结果只证明机制和来源完整，不证明收益提升；四场景配对、重复评价和正式采用仍未完成。

FlowerSpatialQEvaluation原生PASS，独立QA副本冷读新模型后真实near试战获胜，epsilon=0、explored=0、Q表未更新、记录保存与评价读取正常。实际Q选择妮妮莉特3次/乌云2次；UNSEEN_STATE基础回退分别35/38次，合计73次，说明状态覆盖很低，不能把本次胜利归因于新Q策略。需要扩展距离/站位训练覆盖并重新做配对评价；证据flower-spatial-q-result与flower-spatial-q-evaluation-result/process。


### 新版Q四场景训练与冻结对照启动（2026-10-05，进行中）

新增FlowerSpatialQCoverage长测：命名QA副本从版本7候选#3依次探索near/far/reproduction/field，每场保存并从不可变链重建，再冻结最终候选进行四场景各一场基础/候选比较，共4场训练+8场评价。失败场次同样保留；不修改采用指针，训练场景不宣称未见泛化。当前进度写入Test/flower-spatial-q-coverage-result.json，尚在RUNNING时不能作为完成证据；近距训练已获胜并保存候选#4，远距进行中。

独立代码检查发现Ground支援乌云追击直接改x且未播放移动动画。已改为物理velocity驱动，接敌使用360/310缓冲，强力攻击威胁侧在命中范围加140以内后退，边界留25，等待/攻击恢复prepare；受击和完整刀击不被策略打断。显示使用原生fmove/bmove，预设支援策略记录origin=scripted-support，与玩家输入及学员模型区分。该改动仅完成语法检查，须在上述单实例长测结束后运行GroundPartBattle验证胜利与动作完整性，当前不作为验收通过。

支援退避补充：纯逻辑测试RescueTactics通过接敌缓冲、前方/后方威胁、冲撞、边界和退避后不重新踏入攻击范围。已修复退到阈值后立即接近造成的往返抖动，以及边界外目标触发无效刀击；等待Boss本轮攻击结束再接近。原生运动专项RescueMovementNative及GroundPartBattle回归已准备，当前仍等待单实例Q长测释放引擎，未宣称其通过。

本轮范围审计：Script/Enemy/Assets仅为原动画合同，不是敌方实例接入。当前Script/Data中小狐狸与三种英招仍只在该合同出现；大狐狸的剧情引用不能作为敌方战斗证据。大山魈Pursuit已有四招生产入口，但仍使用0.65缩放，Test/SpineTest单位定义为1.0；Enemy.Ambush手掌落点亦硬编码0.65。已更新enemy-boss-iteration状态，原尺寸、落点/镜头、正式Boss及未接入敌人的要求保持开放。


### 战斗卡顿：部位瞄准几何热点优化（2026-10-05）

用户反馈战斗明显卡顿，本轮优先进行实际原生战斗测量。此前四场景Q长测已PASS并释放引擎；本轮仅使用命名QA数据库副本，无正式存档访问。

CombatStutterProfile在花妖近距完整护甲、版本7候选评价实战中记录帧间隔及调用耗时。热点是FlowerDecisionTrace.options反复求解复杂Boss可瞄准部位。HitGeometry改为按不可变动画轮廓缓存边线参数（弱引用随姿态释放）、边线包围盒筛选、射线与包围盒区间裁剪，以及按已知最近命中跳过不可能更近的轮廓。保持原遍历顺序、遮挡优先级、端点容差和真实弹道，不调整人物移动、攻击/动画速度、Boss比例或降低轮廓精度。

同一批12个真实姿态、60次瞄准查询前后结果完全一致；主机Lua计时0.312秒→0.117秒，约2.65倍。另有2万组随机凹多边形线段和多部位最近命中严格对照，以及现有静态/移动碰撞、部位瞄准和距离测试通过。初版只有边线筛选未改善长帧，已迭代为上述组合。

原生完整战斗前/后均获胜：平均帧间隔17.64→17.07毫秒，P99 26.46→17.88毫秒，最大帧间隔576.17→267.96毫秒；options最大250.07→90.68毫秒，单次PartAim最大102.75→43.89毫秒。两局战斗轨迹和时长不同，这些整场数据是观测值，不是确定性等量基准；仍有超过33毫秒的长帧（前12/1614，后10/1849），不能宣称卡顿完全消失。后续继续定位剩余尖峰，并覆盖正式关卡HUD、手动连续瞄准和移动端。证据：LSD/Docs/evidence/2026-10-05/combat-stutter-before.json、combat-stutter-after.json、combat-stutter-poses.json、combat-stutter-parity.txt。新增可复测入口CombatStutterProfile、CombatStutterParity、CombatAimReplay。


补充验证边界：旧CombatPerformanceParity重跑在“旧SpineRegions与当前SpineRegions顶点差异”前置断言失败，该部分未被本轮修改，不能报为通过。保留失败结果；新增CombatStutterNativeParity固定同一份当前原生动画采样，专门比较本轮前后HitGeometry及PartAim，以隔离既有采样差异。既有SpineRegions差异另列待查。

CombatStutterNativeParity原生PASS：12种朝向/位置姿态、2520个顶点、648次瞄准与最近碰撞查询一致。文档构建通过（已有v-producer未入toctree警告）。


### 支援退避原生验收与无效决策开销（2026-10-05）

RescueMovementNative原生PASS：0.6秒前进85.50、后退145.50，分别使用fmove/bmove，面向Boss；停止后velocityX=0，恢复prepare且位置稳定。GroundPartBattle完整战斗PASS：导师、妮妮莉特、乌云三方均实际命中，伤害/护甲与训练记录一致，支援策略报告明确origin=scripted-support。此前标记“未原生验证”的支援运动项现已补齐；不据此宣称所有距离玩法或所有Boss完成。

FlowerDecisionTrace.request现在对明确不可用或已执行中的动作直接委托原执行器，不提前采集昂贵的部位瞄准边界；原拒绝原因、演示拒绝记录及执行器副作用保持。FlowerTraceRejected通过101次拒绝请求的副作用/原因对照，确认无虚假决策边界。HitGeometry射线区间筛选复用轴列表，减少短命表分配。首次原生复测获胜，P99=17.69毫秒，最大264.95毫秒；仍存在长帧，下一步应复用同次决策的合法部位查询，而不是跨帧缓存动画几何或降低采样精度。

四场景Q长测结果已读回：4场训练+8场冻结对照全部自然获胜，最终候选#7，未自动采用。评估仍指出重复不足、稳定收益未证实，field候选耗时更长且队伍伤害增加。不能把完成长测等同于候选优于基础策略。

最终CombatStutterProfile原生PASS且traceRebuilt=true：实际新战斗记录通过FlowerTraceReview完整重建。该次P99=23.64毫秒、最大285.44毫秒，提示不同战斗轨迹仍有明显波动，不能用上一局较好数据代替持续稳定性验收。证据combat-stutter-rejected-trace-result.json；下一轮继续降低同步部位查询尖峰。


### 同次Q决策复用部位查询（2026-10-05）

FlowerDecisionTrace.options附带返回已求解的瞄准方案；decision将合法动作、方案、观测封装为仅当前角色、当前战斗、当前帧的一次性结果。FlowerQExecutor及FlowerQSession探索路径在选择、提交和记录决策边界时复用该结果，不再重算五个部位或重算最终选中部位。过期、其他角色/战斗、已消费结果仍走实时采样。此处没有跨帧缓存，不改变实际发射后的弹道/遮挡；C4.5已有按需查询路径保持原样。

FlowerDecisionReuse纯逻辑PASS：一次提交仅求解各部位一次，选中方案和记录观测复用；已消费、前一帧、其他角色结果拒绝复用；FlowerTraceRejected仍PASS。CombatStutterProfile原生完整试战获胜，FlowerTraceReview重建成功：3287帧，P99=17.76毫秒，平均16.79毫秒，4帧超过33毫秒，最大111.84毫秒；PartAim累计0.518秒/115次。与优化前及上一轮的战斗时长/轨迹不同，不能直接按累计调用量推导固定百分比性能收益；最坏长帧仍未达到流畅性验收。证据combat-decision-reuse-performance.json、flower-decision-reuse-unit.txt。另启动真实探索训练、序列化保存/源链重建验证，完成前不宣称训练路径验收。

FlowerDecisionReuseTraining原生PASS：真实探索83.58秒后获胜，妮妮莉特170/乌云146次Q更新，保存候选#3并从源记录重建完全一致；父版本与旧采用指针保留，无自动采用。证明同次决策复用覆盖探索更新与持久化路径，不只覆盖冻结评价。证据flower-decision-reuse-training-result.json/process.log。


### 正式战斗HUD与手动瞄准性能覆盖（2026-10-05）

新增CombatHUDPerformance原生入口，经Factory.Level.openAsync加载正式场景、统一摇杆/技能HUD、生命护甲栏、音乐及结果界面；使用命名QA副本和既有基础模型。旧专项采用因规则变更被正确拒绝，显示重新评价提示，因此本测试覆盖正式界面基础回退路径，不冒充新版Q已采用路径。导师通过真实Aim.begin/release交替短按与长按，触发实际枪弹、弹道与弹壳；队友和Boss自然执行，非静态UI计时。

首次测试自然获胜：45.14秒，36次发射、35次导师命中、163帧显示瞄准预览，2582个计时帧；P99=16.68毫秒、最大34.16毫秒、1帧超过33毫秒。该次包含一次截图，不作为纯性能最终验收；随后运行不含截图的复测。截图combat-hud-performance.png已查看：Boss与角色、花妖裙摆及统一UI正常显示，同时队伍仍近距离聚集，距离/站位玩法保持未完成，不以性能通过替代玩法验收。

无截图复测CombatHUDPerformance原生PASS并自然获胜：44.22秒，35次发射/34次导师命中/165帧预览，2530个战斗计时帧，平均16.681毫秒、P99=16.675毫秒、最大27.803毫秒、超过33毫秒0帧。HUD自身统计包含准备阶段，其最大35.318毫秒不等同于暖机后战斗帧；证据combat-hud-performance-result.json/process.log。该结果限于当前机器、该基础模型正式界面场次，不能外推移动端、所有Boss或Q训练；训练路径约112毫秒峰值继续列为待优化。


### 大山魈恢复原始体型与伏击落点（2026-10-05）

Ruins.Pursuit大山魈从0.65恢复1.0，与SpineTest加载比例一致；小山魈原配置不变。附近有存活大山魈时通过镜头缩放/高度容纳原尺寸，暗影伏击继续额外拉远。天空使用原背景层后的静态补色与顶部渐变延伸，保留原路面/城市/前景比例；683×384窗口原生截图已查看，伏击模型与预警、HUD可见，上方不再露黑。

仅替换伏击常量缩放时发现朝右落点误差约52；改为下落过程中按实际手掌对齐锁定预警，命中后停止对齐以保留收招。进一步发现父物理节点移动后，其Spine子节点世界矩阵延迟失效，BigShanRelease.point先解析父变换再查询子节点，修复同帧手掌读旧位置。最终左右与群体落点误差均为0，没有放宽测试容差。

AmbushNative原生PASS（authoredScale=true）：自动选择、左右命中、移动闪避、群体、烟雾、眩晕、手动取消及结束退出，无延迟伤害，完整两段动画约2秒。BigShanComboNative PASS：砸地/拳击三击、背后范围差异、逃离/受控与退出取消。BigShanHandNative PASS：原12段动画时长不变，双向举物和真实投物命中，出手后转身不改变投物击退方向。AmbushViewNative PASS并查看截图。证据fullsize-shan-ambush/combo/hand/view-result.json及对应process.log，fullsize-shan-drop.png。当前仅证明专项和镜头；新比例的完整剧情撤离路线、正式击败Boss遭遇及部位护甲机制仍未验收完成。


### 原体型大山魈完整撤离路线与追击瞄准入口（2026-10-05）

PursuitBattle使用指定/private/tmp命名QA副本，从遗迹返程入口进入原5行剧情，经正式HUD发射实弹、施放火光/烟雾、向右撤退，20.59秒自然获胜：四名伙伴全部步行撤离且HP均100，导师HP70，三处路标完成，射击/火光各命中一次，道具完整动作各一次，剧情解锁ruins-diversion-complete，既有训练模型未变。该证据使用真实UI事件调用而非OS鼠标，不能替代人工操作难度验收；撤离也不等于正式击败Boss遭遇。

检查发现PursuitLevel原有Skill.Began直接开枪及独立J立即开枪入口。已改为Ground.Mentor.bindAim统一按住瞄准、松开发射，删除重复J映射；PursuitBattle及PursuitOutcomes更新为真实按下/松开事件，并断言按下期间未提前开枪。追击HUD仅在文字变化时重新赋值，面板/体力条仅在尺寸/状态变化时重绘，减少逐帧重复提交。完整路线在该改动下通过；专项PursuitAimHUD验证短按、长按角度与退出取消另行运行。证据fullsize-pursuit-route-result.txt/process.log。

射击入口审计发现Ground.EnergyLevel、Factory.PatrolLevel、Mission.Level、Trial.Level仍有按下立即射击绑定；前两者使用Ground.Mentor，后两者有独立执行器，需分别接入及验证，不能直接假定全关卡已经统一。PatrolLevel还承载后续潜入、救援、防守和终局，改动须覆盖其battleFactory变体。

PursuitAimHUD原生PASS：正式武器按钮短按0.06秒得到0度水平弹道，长按0.35秒得到-17.92度且弹速方向与角度一致，按下期间均不发射；退出时取消未释放瞄准。证据pursuit-aim-hud-result.json/process.log。


### 能源战斗与共用巡逻界面统一瞄准（2026-10-05）

Ground.EnergyLevel、Factory.PatrolLevel接入Ground.Mentor.bindAim，沿用教程式短按水平发射/长按扫角、松开发射及预览线，覆盖该共用界面的后续关卡。SharedMentorAimHUD分别启动能源、首轮巡逻、第二巡逻、研发人员遭遇、救援、学院防守、终局七个实际战斗工厂，均原生PASS：巡逻界面各变体准备期禁止瞄准、各场按下期间无弹、短按0度、长按约-18度且实际弹速方向一致，切后台及HUD清理取消瞄准且无新增子弹。证据shared-aim-energy/patrol/second/researcher/rescue/defense/final-result.json。

验证进一步暴露输入清理原来复用了无参数Skill.Ended，可能被解释为正常松开。UI.HUDControl现在用Skill.Ended(true)标识取消，正常释放仍无标志；Mentor与FlowerPractice按取消处理，教程System同步在取消时清理预览但不启动kinetic，原学院按键复位消费者保持兼容。HUDControl的Yue/Lua及教程的Teal/Lua均同步。HUDInputAvailability原生PASS；TutorialRegression新增取消期间不启动射击断言并PASS，随后正常短按实际命中。

RoofAimIntegration通过真实屋顶剧情存档副本进入共用PatrolLevel，原生对战获胜，导师8次命中、学员实际决策和火焰命中，对手完整攻击/倒下、注入保存失败后的重试、恢复和其他表不变均通过。仅访问命名QA存档。17个采用旧单独Skill.Began的共用巡逻回归脚本同步补充Skill.Ended短按序列，未宣称这17条整路线本轮全部重跑。Mission.Level和Trial.Level使用独立射击执行器，仍待接入，不能宣称全游戏已统一。


### 独立任务/试炼射击执行器接入瞄准（2026-10-05）

Mission.Battle新增mentorAim，使用原pistol完整动画等待与实际枪口发射，角度进入子弹速度，复用Combat.FirearmRules、FirearmVisuals和Tutorial.LightStrip，保留原每次5点伤害和冷却。Mission.Level连接统一按住/松开及取消处理。SharedMentorAimHUD的mission变体原生PASS：水平短按真实命中、长按约-18度对应弹速、后台与清理不误发。

Trial.Battle新增heroAim并接入Trial.Level；玩家射击使用同一2400速度/1秒寿命（由原1.5秒统一为枪械规则），实际枪口与角度，子弹/弹壳/教程弹道线；李叶娜仍保留原1700速度、1.5秒寿命和原动作节奏。刀击/防御入口不变。TrialAimNative合作/对打均PASS：准备期不可瞄准、按住不发射、短按真实命中、长按角度和速度一致、两次实际弹壳、取消不发射。TrialHitRecovery原生PASS，保留防御、角色受击恢复、真实子弹命中和致命倒下。

LiyenaAimRoute完整流程首次在旧脚本直接写学院方向标志处超时，尚未进入战斗；改用已存在的正式摇杆事件移动助手重跑，最终结果待回填。所有存档为指定/private/tmp命名QA副本，不读取正式lsd.db。证据shared-aim-mission、trial-aim-coop、trial-aim-duel、trial-aim-hit-recovery；本段专项不替代完整路线/奖励/保存验收。

LiyenaAimRoute最终原生PASS：正式学院门/终端进入，准备期不战斗，合作和对打两场实际获胜，双方合作出手、真实攻击事件及完整动画、事务回滚重试、完整Yarn认可对话、奖励只发一次、训练模型行不变、返回原房间均通过。已修正的新路线脚本使用正式摇杆与按下/松开事件；这是原生事件回归，不声称OS鼠标/移动端实测。证据liyena-aim-route-result.txt/process.log。


### 战斗距离与复杂轮廓查询优化（2026-10-05）

Combat.HitGeometry.distance复用当前不可变姿态的边数据，以部位/边包围盒距离下界排除不可能更近的边；包含判定优先，保持重叠部位、同距离优先顺序及边界容差。复杂轮廓包含测试增加按纵坐标分桶的边索引，仅遍历可能穿过查询水平线的边；索引随弱引用姿态缓存释放，不跨帧复用旧姿态，不简化轮廓，不改变移动、动画、枪械或命中规则。

CombatStutterParity通过20000组20/60顶点凹多边形射线及60000次距离旧实现对照；SpatialGeometry补充重复顶点、重叠同距、1e-5到1e6坐标尺度与边界容差。HitGeometry、MovingHit通过。真实捕获12姿态的固定数据基准：12000次距离查询旧2.868秒/新0.523秒，约5.48倍；60次部位瞄准旧0.365秒/新0.113秒，约3.23倍（瞄准对比包含此前几轮优化，不能全部归因于本次）。这些为宿主Lua固定数据基准，不能等同于整场帧率倍数。新增CombatDistanceReplay保留可复现入口。

CombatStutterNativeParity原生通过2520顶点/648查询。完整Q评价战斗自然获胜、源记录重建成功：1446帧，P99=23.55毫秒，最大93.29毫秒，9帧超过33毫秒；合法动作查询峰值仍78.94毫秒。中间仅距离优化的场次最大141.86毫秒，说明不同轨迹有波动，不能宣称整体卡顿已经消除。该路径仍需继续处理集中部位求解尖峰；正式HUD性能另行复测。仅使用命名QA存档副本。证据combat-distance-native-parity、combat-distance-profile。

正式HUD无截图复测PASS：44.41秒，2544战斗帧，P99=16.67毫秒，最大18.98毫秒，超过33毫秒0帧；35次实际发射、34次导师命中、169帧瞄准预览。结束采样时phase=saving，因此本次证明战斗性能和输入/命中路径，不宣称保存及结算结果已验收。证据combat-distance-hud-result.json/process.log。文档构建通过，仍仅已有v-producer未入toctree警告。


### 同姿态候选射线进一步筛选（2026-10-05）

在上一轮距离/包含索引基础上，HitGeometry为连续8条轮廓边建立范围块，射线先排除整块再做原有精确交点计算，保持边和部位顺序以及按边长缩放的容差。segment对同一不可变姿态、同一枪口坐标复用包含判定；以坐标值判断而非点对象身份，枪口改变立即重算。没有跨姿态缓存，没有缩减候选点或推迟训练决策。

新增CombatRayReplay与CombatRayBefore固定快照：相同12实际姿态、600次瞄准，上一轮1.049133秒、本轮0.825555秒，约1.27倍；逐项返回完全相同。CombatStutterParity的20000射线与60000距离对照通过，SpatialGeometry新增重复射线和原地修改枪口对象的缓存失效回归；HitGeometry/MovingHit通过。

原生CombatStutterNativeParity通过2520顶点/648查询。完整Q评价自然获胜并重建源链：1200帧，P99=22.54毫秒，最大79.67毫秒，8帧超过33毫秒；合法动作查询峰值66.22毫秒，单部位求解26.84毫秒。轨迹与上一场不同，仅固定数据基准可直接比较算法收益；训练尖峰仍未完全消除，不能据此宣称全战斗性能验收。证据combat-ray-block-native-parity、combat-ray-block-profile；现有正式HUD普通战斗无长帧证据不能代替训练路径。


### 捕获训练慢查询与减少临时碰撞结果（2026-10-05）

CombatStutterProfile现保留耗时最高的12次部位瞄准，包括当前840顶点姿态、枪口、朝向、目标部位、实际遮挡回调顺序/结果；仅在结束后序列化，不在战斗中写文件。实际慢查询多为不可达根部/侧花瓣，其中单次根部查询出现184或225次遮挡回调，属于集中候选遍历而非动画播放速度问题。保留原始捕获combat-slow-aims-captured.json及CombatSlowAimReplay，后续必须针对这些真实慢姿态验证，不能只测最初12个普通姿态。

试验连续边范围的二叉层级索引：同批120次慢查询由0.915秒变0.950秒，已撤回。最终仅保留segment命中结果的延迟构造：遍历时保存最优t/边方向，选出最终交点后再创建position/normal并计算法线，避免每次更近交点都分配三张临时表；原有夹取t、遍历顺序和精确计算不变。固定慢查询上一轮0.920347秒/本轮0.878672秒，约1.047倍；4950次遮挡回调的顺序、位置与返回值保持。该数据不包含真实物理raycast执行开销，不代表完整战斗同比收益。

20000组射线/最近命中、60000次距离对照以及HitGeometry/SpatialGeometry/MovingHit回归通过；原生对照及完整训练战斗正在复测，结果另行追加。

本轮原生复测完成：CombatStutterNativeParity通过2520顶点/648查询；CombatStutterProfile自然获胜且源链重建通过，3100帧P99=16.67毫秒，最大101.27毫秒，7帧超过33毫秒。合法动作峰值64.45毫秒。该次战斗显著更长，最大帧高于前次79.67毫秒，故不能报告整场卡顿持续单调改善；固定慢查询的等价和小幅收益已证实，剩余集中候选/遮挡开销尚未解决。证据combat-scalar-native-parity、combat-scalar-profile。


### 慢姿态区间筛选与计划状态校正（2026-10-05）

核对真实慢姿态：32个轮廓共840顶点，各轮廓没有重复顶点，不能以去重候选解释尖峰。HitGeometry射线与包围盒区间筛选改为直接x/y数值运算，移除每条候选对每个轮廓的轴名循环和动态字段访问，原容差、运算顺序、平行射线规则不变。固定120次慢查询旧0.882676秒/新0.834328秒（约1.058倍），4950次遮挡回调保持一致；20000射线与60000距离对照通过。完整原生结果另行追加，仍不得称训练卡顿完成验收。

重新读取四场景Q覆盖与支援移动证据，校正enemy-boss-iteration当前状态：Q四场训练/八场冻结对照已结束而非运行中，候选#7未自动采用，稳定收益未证实；支援物理移动已验收而非待验收。自动远程站位、其余敌人、正式击败Boss遭遇及总体体验仍开放，不将性能微优化代替下一轮完整内容目标。

原生区间筛选复测：CombatStutterNativeParity通过2520顶点/648查询；完整训练评价自然获胜，源链重建通过。2997帧P99=17.22毫秒，最大75.53毫秒，7帧超过33毫秒，合法动作峰值62.03毫秒。仍有长帧且不同轨迹不可当确定性同比；证据combat-slab-native-parity、combat-slab-profile。文档构建通过（原有v-producer的toctree警告）。


### 小英招动作姿态与技能时序（2026-10-05）

SmallYingzhaoPoseNative及SmallYingzhaoImpactPoseNative原生生成并人工查看两组姿态图。首次画布原点错误造成裁切，已修正并重新截图；最终完整20格与12格可见。原素材面向左，与SpineTest一致。jump/jump2/jump3/jump4分别0.4333/0.5667/0.3667/1.3667秒：蓄力、跃起扑出、落地、恢复。jump2的0.20秒前爪伸出；kick的0.45秒仍为前摇，0.55秒起翻，0.65秒倒身前踢，0.75秒转下，0.85秒回落，完整时长1.7333秒。

原动作稿“小英招飞扑攻击”效果文字写抢夺武器射击，与原生动画及中英招独立rob/shoot设计冲突。本轮按小英招的前爪飞扑实现方向推进，缴械/持枪反击保留给中英招，不给小英招凭空加枪械动作。新增Enemy.SmallYingzhaoTimeline独立时序：jump2=0.20、kick=0.65；所有段仍经Enemy.Sequence实际AnimationEnd推进，完整保留收招。此处是经姿态校准的动作契约，目标扫掠、移动、伤害、击退、单位AI、公开遭遇尚未接入，不能宣称敌人已制作完成。

证据small-yingzhao-poses.png、small-yingzhao-impact-poses.png及对应原生结果；左右朝向完整时序与打断专项结果另行追加。

SmallYingzhaoTimelineNative原生PASS：jump/kick各左右朝向共四例，飞扑四段全部收到完成事件后才推进，踢击完整结束，单次有效时机在配置时间后80毫秒内触发，recovery=0.2后恢复idle；各例在前摇受击取消后无延迟攻击。验证为原生动画与时序，尚未验证物理位移/真实目标命中。证据small-yingzhao-timeline-result.json/process.log。文档构建通过，仅已有v-producer未入toctree警告。


### 小英招物理单位、攻击控制器与原生交战（2026-10-05）

新增Enemy.SmallYingzhao，提供与现有PatrolBattle场景扩展一致的create/new接口；原始朝向向左、原比例1.0，独立物理单位，move接敌180，距离310内选择扑击，180内选择翻踢。扑出段给实际速度420/320，由物理重力控制，落地段停止横向推力；命中时只选择前方范围内最近且未被地形遮挡的一个存活目标。暂定扑击10伤害、翻踢12伤害，分别调用共用受击位移280/120与650/250，数值为待整场平衡的实现初值。

技能通过上一轮校准的Sequence完整播放；伤害下降触发hit并取消当前攻击，死亡取消攻击后完整lose，退出停止位移与后续命中。重用CombatAnimation的recovery=0.2与Combat.Displacement，未另造受击系统。小英招不是同行狐狸，没有改变狐狸训练限制或现有故事遭遇。

SmallYingzhaoCombatNative在原生场景中创建真实动态单位与真实导师，首轮PASS：双向翻踢各命中一次、双向扑击各命中一次；扑击位移约±165.96，翻踢命中速度±650/250；700距离扑空、起手后移开闪避不扣血、前摇受击取消无命中；0.5秒接敌移动74.92，退出取消，完整死亡通过。仅借用追击场景提供物理世界，原追击处于ready，不替换生产追击敌人。公开任务接入、整场平衡、组合波次和玩家实际输入体验仍待完成。新增背后闪避、自然接敌选扑击及攻击中死亡取消的扩展验证正在运行。

扩展SmallYingzhaoCombatNative原生PASS：新增起手后绕到背面不命中，真实接敌进入距离后自动选择并完成扑击，攻击前摇中死亡取消且完整播放lose。共八个定向攻击案例；全部阶段完成时间与单次伤害断言通过。证据small-yingzhao-combat-result.json/process.log。文档构建通过，仅原有v-producer未入toctree警告。


### 英招演练公开入口与完整战斗流程（2026-10-05）

基础训练菜单新增“英招演练”，有未处理示范/候选或正在评价时禁止离开；要求妮妮莉特与乌云已有采用模型。Training.YingzhaoPractice复用PatrolBattle/PatrolLevel、VRTraining场景与统一摇杆/按住瞄准松开发射、火焰/旋风和结算界面，实际三只原比例小英招，每只初始HP100。PatrolBattle场景/敌方asset现可由scenario配置，既有默认工厂与守卫行为保持。演练支持准备、开始、胜负/撤退、再次演练和返回基础训练；不发故事奖励，不写新学习样本或替换采用模型。它是已公开的战斗演练，不能替代后续剧情遭遇或英招专属Q/C4.5采集。

首轮完整战斗发现每次伤害都重启hit，敌人被压制至完全无法起手。现保留所有伤害，只限制受击动作：正在hit时不重播，重复受击动作间隔1.2秒，完整hit结束后0.15秒可再次行动；没有新增伤害免疫。另发现世界场景Spine的AnimationEnd会早于控制器计时约一帧，原Sequence以1毫秒门槛丢弃合法结束事件，导致停在jump。已允许提前一帧锁存结束事件，但仍等完整duration后再切段；新增确定性回归证明早到事件不会截短动作。

YingzhaoPracticeNative使用命名QA副本，从真实基础训练菜单进入并以统一UI事件战斗，自然获胜7.62秒：导师6次命中，两名采用模型各4次动作/4次命中，火焰3/旋风2，敌人5次起手且实际进入扑出段；后续击败会合法取消攻击。三名队员本局均HP100，说明该已训练队伍压制明显，尚不能据此判定平衡完成。原生事件回归不等于OS鼠标或移动端验收。重新开始、准备期撤退、返回基础训练均通过，采用模型和任务表逐行快照不变。测试首次等待重开时将过渡世界的nil控制器误认为新控制器，已修正等待存在且不同再检查，最终完整通过。

截图yingzhao-practice-active.png已查看：虚拟训练场、原角色、三只小英招与统一UI可见；单位仍存在近距离重叠，距离/队形要求继续开放。证据yingzhao-practice-result.json/process.log。现有EnemySequence、小英招物理交战和大山魈伏击回归另行追加。

共享时序改动回归完成：EnemySequenceNative原生多段结束/恢复通过，SmallYingzhaoCombatNative八个命中/闪避案例及自动接敌、退出/死亡取消通过，AmbushNative原尺寸大山魈自动选择、左右伏击、躲避、群体、烟雾/眩晕/手动与结束取消均通过。证据yingzhao-sequence-regression、yingzhao-combat-regression、yingzhao-ambush-regression。文档构建通过，仅原有v-producer未入toctree警告。


### 中英招动作核对与武器挂点派生（2026-10-05）

原生MediumYingzhaoPoseNative核对rob/rob2/rob3/rob4、shoot、punch；实际素材未含PointAttachment武器挂点，不能仅setSlot就显示枪。已找到桌面“LSD美术/怪物/英招/spine 中英招/zhongyingzhao.spine”，只读导出到Docs/artwork/yingzhao-weapon，原工程SHA256保持。原工程JSON与现有运行skel所有14动画、每动画121姿态对照2737532坐标，最大误差0.00280762，证明可用此原工程派生而不重建动作。

新增zhongyingzhao-weapon派生JSON/Spine/skel：bone52握持挂点，位置(-100,-25)、角度24，drawOrder插入近侧手之前；对原动画存在的遮挡顺序关键帧重新编码，去掉挂点后保持原slot相对顺序。使用原kineticgun/PT和0.3比例，原始左朝向武器本地Y负缩放。首版握在枪尾，已调整到握把并查看最终持枪/射击姿态图；派生前后原网格同样通过2737532坐标对照。未改原skel/atlas/png。

MediumYingzhaoWeaponNative原生PASS：gunidle/shoot两种动作各左右朝向，枪口轴指向与朝向一致，完整结束事件符合原时长。证据medium-yingzhao-poses.png、medium-yingzhao-weapon-poses.png、medium-yingzhao-weapon-result.json/process.log及medium-yingzhao-weapon-geometry.txt。当前仅补足持械美术能力；缴械实际接触、武器归还/禁射、真实射击、AI与公开遭遇仍未完成。


### 临时缴械、射击门控与武器归还（2026-10-05）

新增Combat.Disarm临时武器占用机制，限定有combatWeaponAsset/Look元数据的枪械，导师kineticgun与学员empgun保留原类型、look和比例。原枪节点仍留在原挂点，以横向缩放0临时隐藏，在中英招派生挂点显示同款枪；没有删除并复用已被引擎Cleanup的节点，也不改持久化装备。一个持有人/一个持械者只允许一个有效占用，默认6秒，支持显式归还、超时、持械者/持有人节点清理与遭遇结束。归还移除监控与Cleanup监听，重复归还幂等。中英招实际夺取命中尚未调用本机制。

Ground.Mentor和Training.Arena的射击可用性与发射事件均检查缴械状态；瞄准期间缴械自动取消，学员移动/刀击保持可用。每次成功缴械增加射击代数，已起手但尚未发射的动作即使提前归还也不能补发子弹；动作仍完成正常收招与记录关闭。学员未发射不消耗射击能量。最初将枪械元数据表放入原生Dictionary触发类型错误，已改为引擎支持的独立字符串字段后重跑，不保留失败实现。

DisarmNative原生PASS：导师瞄准取消、重复夺取拒绝、超时还回同一个原枪节点、起手后禁射、提前归还不复活旧射击、导师重新射击、遭遇结束还枪、持械者清理还枪、学员empgun禁射/不耗能、保留移动刀击、学员恢复发射、持有人清理移除敌方枪。证据disarm-result.json/process.log。完整小英招演练回归正在运行，检查无缴械时原射击和已采用策略不受影响。当前没有中英招AI、抢夺有效帧接触、持械反击弹丸或专项训练数据，仍不算中英招制作完成。

无缴械场景完整回归YingzhaoPracticeNative原生PASS：真实菜单进入、导师/两名学员射击与技能、自然获胜、结算重开及返回基础训练通过，保存的采用模型与任务表不变。证据disarm-practice-regression-result.json/process.log。文档构建通过，仅原有v-producer未入toctree警告。
<!-- preserved-progress-end -->
