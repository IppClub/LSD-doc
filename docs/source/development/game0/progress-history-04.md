# 开发历史记录 · 第 04 卷

> 2026-10-05 从旧进度页归档。以下为当时记录，含已被后续结果替代的状态，不作为当前待办。请从[当前进度](progress.md)或[历史索引](progress-history.md)继续阅读。

## 原始记录

<!-- preserved-progress-start -->
### 2026-10-04：新档连续遗迹调查、伏击与谷地转场

JourneyFreshRuins 1791077190 PASS，承接本轮治疗后来源，经正式学院路线、站台、列车及三人编队进入遗迹，连续完成双胞胎41句、实际弹体与格挡、双胞胎步行护送、发现阿岩7句、日记7句、数据回收8句，故障回滚先于视觉消失。随后在同一现场走至返程入口，触发5句伏击对白并完成实际掩护撤离；烟雾/照明弹动作完整，射击与照明弹实际命中、四人步行超过1000到安全点、三处路线点经过，学员模型和既有物资保持。

原生截图发现PursuitLevel胜利结算的“再次行动/返回基地”均进入谷地，文案误导。已修正为胜利只显示居中的“继续旅程”，隐藏并禁用第二按钮；失败则显示“重试掩护/返回遗迹”。修改后重跑完整调查→伏击通过，并用CUA真实鼠标点击“继续旅程”，实际进入OuterHeaven吊床与万薇莉场景。此OS证据仅覆盖结算转场，不覆盖前面的整场战斗。

证据fresh-ruins-pursuit-native.txt、fresh-ruins-pursuit-records.json、fresh-pursuit-os-continue.json、fresh-pursuit-os-valley.tga；后续来源Test/fresh-pursuit-resume-fixture.txt。首次未改按钮的通过记录另存fresh-ruins-before-result-copy.txt。主存档未打开，失败结算新文案尚未重新进行OS画面验证。


### 2026-10-04：新档谷地初遇、五项活动与狐狸到场

JourneyFreshValley 1791077482 PASS，承接最新遗迹伏击来源，经Start直接恢复桃源谷，完整苏醒/喂水/实际骑乘/喂食、原32句对白、音乐环境与花瓣启动通过，已撤离的学员没有错误出现在谷地，重看不重复演出和奖励。

JourneyFreshValleyActivities 1791077529 PASS，正式HUD输入完成三次时机钓鱼、三垄种植浇水及实际等待生长、三处观察摘桃、两次追鸡、静心语言问答。测试已去掉旧版人物reaction=.05和直接stop/velocity写入，以正式移动响应执行；没有瞬移或预置活动完成状态。错答不奖励，最后语言奖励失败保持旧进度、重试成功，五项奖励各一次，动作完整、万薇莉实际跟随、重新进入活动状态保持通过。

JourneyFreshValleyDays 1791077665 PASS，同样使用正式HUD和移动参数，实际回吊床完成休息苏醒，保存故障重试不重复动作，再完成24句后续对白与狐狸实际入场、解锁fox-route-offered。重看不重复入场或休息，角色名称与奖励唯一性通过。

证据fresh-valley-encounter-native.txt、fresh-valley-activities-native.txt、fresh-valley-days-native.txt、fresh-valley-earned-records.json。后续狐狸路线来源Test/fresh-valley-days-resume-fixture.txt；本轮为原生HUD事件测试，不能替代全OS活动游玩与素材最终视觉验收，主存档保持。


### 2026-10-04：发现并修复狐狸带路仍使用旧模型

新档JourneyFreshFoxTrail首次1791077825在正式模型断言失败：FoxTrail、ValleyDays和Navigation的foxParty仍调用FoxCompanion.create旧整图Q模型，未接入已修正Spine，因此此前其他场景的动作修复不能证明这三处生效。现已将三处构造及相应预载改为createAnimated/loadAnimatedAsync，原立绘构造器保留给既有立绘用途。没有降低位移速度：通用Fox.walkSpeed保持240，带路原剧情节奏200和谷地2.6秒入场插值均保持，动画独立0.85倍速。

JourneyFreshFoxTrail 1791077957 PASS，从本轮谷地来源完成实际出发、走走停停、第二段5–10秒带路、食物动作及保存失败重试、万薇莉实际到场、夜光镜3秒收集与失败重试、三人走到开阔地和归队、跨房间重看。食物只扣一次，医疗物资不变。此次未注入候选模型。

JourneyFreshFoxMotion 1791078052 PASS，从刚获得的带路中点副本经Start恢复正式模型，实际HUD右行3秒，走路完整循环1.183287秒、idle完整循环1.999774秒，朝向右、动画0.85、停步恢复1倍和0.2秒recovery、待机无位移、食物不重扣通过。已查看真实场景走路/待机截图；此项不是连续全帧美术质量验收，谷地新模型的完整入场还需回归。

证据fresh-fox-old-model-failure.txt、fresh-fox-trail-native.txt、fresh-fox-motion-native.txt、fresh-fox-runtime-walk.tga、fresh-fox-runtime-idle.tga；后续主线来源Test/fresh-fox-trail-resume-fixture.txt。本轮为原生HUD事件测试，主存档保持。


### 2026-10-04：狐狸动画独立速度与新档指挥室、首场潜入

狐狸步频参数集中为Fox.walkAnimationSpeed=0.85，优先于按位移估算的步频；通用移动速度240、原带路200均保持。JourneyFreshFoxMotion 1791078679重新通过，实际带路速度200、完整走路循环1.183458秒、待机2.000082秒、停止无漂移，recovery恢复0.2秒。此为原生HUD事件测试，不是完整OS动作验收。

JourneyFreshValleyDays 1791078249重新验证修正Spine狐狸完整入场、正常待机、重看不重复演出；补足此前谷地模型替换后的回归缺口。CommandAssembly的备用创建路径及Infiltration正式狐狸创建路径也已改用修正Spine。JourneyFreshCommand 1791078299通过：正式指挥室、28句汇报、十项分工与故事原子保存失败重试、手机四组分工、重看和编队返回、已有资源模型不变。

JourneyFreshInfiltration 1791078374通过：承接刚完成的指挥室来源，实际夜光镜定位、首波巡逻战、保存失败重试、撤回与公开日记重读；战斗19.58秒，妮妮11命中、乌云9命中，导师11命中，学员模型无fallback。战斗由原生战斗命令驱动，不能视作OS完整战斗。后续来源Test/fresh-infiltration-resume-fixture.txt为本轮首战完成的中点副本。

证据fresh-valley-spine-arrival-native.txt、fresh-command-assembly-native.txt、fresh-infiltration-native.txt、fresh-fox-animation-speed-native.txt。主存档未打开或修改。审问独立立绘的FoxThreat依赖original-art节点，尚未直接替换，需独立适配和演出验收。

JourneyFreshInfiltrationPath 1791078749 PASS，承接以上首波巡逻中点副本，从Start恢复后继续原狐狸引路对白。测试使用正式HUD左右移动，删除直接key/stop/velocity控制；实际被巡逻发现退回安全点，然后按守卫方向穿越三处箱体并通过原行动按钮隐蔽。修正Spine模型、有效三处掩体记录、实走超过1500、完成保存失败重试、完成记录幂等、研发人员侦察两句通过。此项仍为原生HUD事件测试，不是OS全程潜入。证据fresh-infiltration-path-native.txt、fresh-infiltration-cover-1/2/3.tga，后续来源Test/fresh-infiltration-path-resume-fixture.txt。


### 2026-10-04：新档研发人员抓捕与修正狐狸审问演出

对照策划2-15，继续本轮实走三掩体来源。JourneyFreshResearcher首次1791078874因旧测试将已存在的Game0Researcher也列入“不能变化”表而失败；该表正是抓捕的预期写入目标，修正只排除此表并保留caught、胜利报告幂等、保存失败回滚与未来版本拒绝等断言。重跑1791078954 PASS：原接触两句、实际抓捕战、失败重试、返回Factory 4100、受控研发人员、不重复战斗和其他表保持。此为原生命令战斗，非OS输入。

InterrogationActors原先临时创建旧整图狐狸。现改用正式修正Spine和已有FoxSpineThreat嘴部锚点表情，补上1.2秒warnAsync及清理取消行为，不改变位移和行走动画参数。JourneyFreshInterrogation 1791078975 PASS，原十二句、堵嘴0.55秒/松手0.4秒、狐狸露牙约1.2003秒、女导师击晕0.9秒/实际命中约0.3331秒/研究员倒地1.35秒，完整演出证明与剧情原子保存失败重试通过。运行中逐次检查露牙组件随嘴部锚点、演出后隐藏，已查看实际警告截图；这证明本场集成，不等于所有方向逐帧动画验收。

证据fresh-researcher-old-snapshot-failure.txt、fresh-researcher-native.txt、fresh-interrogation-native.json、fresh-interrogation-fox-warning.tga；后续来源Test/fresh-interrogation-resume-fixture.txt。主存档未打开，仍需继续第二波巡逻、控制舱及后续主线与完整OS游玩。


### 2026-10-04：新档第二巡逻、七层控制舱与真实输入修复

JourneyFreshSecondPatrol 1791079115 PASS，承接本轮审问来源。乌云留守、场内无乌云实体、旋风按钮隐藏且调用返回ROLE_ABSENT；实际28.05秒胜利，妮妮16次模型动作/16命中/0fallback、导师16命中剩16生命。完整守卫攻击/败退、保存失败重试、拒绝伪造乌云参战和提前败退、回厂区留守位置恢复均通过。本轮仍是原生战斗命令，非OS全场战斗。

JourneyFreshControlPod 1791079155 PASS，同来源公开入口、三人队伍、修正狐狸Spine、逐层实际旋转阶梯六段各约8.717秒、三层保存失败重试、封闭舱门阻挡、开门旋转105度并解除碰撞、音频句柄和2.81秒时长通过。两个测试仅排除各自预期更新的Game0SecondPatrol/Game0ControlPod表，其余已有表逐行保持。

JourneyFreshControlPodMouse 1791079240 PASS，真实CUA鼠标从厂区继续行动进入控制舱，逐层点击上楼，正式方向区移动至控制台并点击开门。观察程序只读完成状态，没有替玩家发移动/技能事件。六段阶梯与2.8094秒开门均记录，门后研究员可见。此OS证明覆盖控制舱入口至七层开门，不覆盖第二巡逻战。

真实输入中E短按多次无效，而临时只读KeyDown观察确实收到E；原逐帧isKeyDown漏掉短按。ControlPod已改为独立KeyDown事件响应E/Q，保留ready及storyBusy门槛，删除轮询以免重复触发。重新加载修复版JourneyFreshControlPodKeys 1791079760，真实短按E上到二层、短按Q回一层PASS。另修正下楼过程中仍提示“上行”的文字；此文案通过语法检查，尚未重新截图。方向输入最初从摇杆中心拖动没有有效移动，改在原右方向触区操作后正常，此处未改移动速度。

证据fresh-second-patrol-native.json、fresh-control-pod-native.json、fresh-control-pod-os.json、fresh-control-pod-keys-os.json；后续剧情来源Test/fresh-control-pod-resume-fixture.txt。主存档保持，仍未宣称完整Game0通关验收完成。


### 2026-10-04：新档控制舱问话、实际屋顶入口与纹记光柱

JourneyFreshControlPodDialogue 1791079954 PASS，接续本轮七层开门来源，从Start恢复时不重放开门和楼梯，实际步行到三名研究员旁。原29句、导师和妮妮两处原生持枪到位事件、狐狸prepare露牙1.25秒及75帧嘴部跟随、失败保存回滚重试、原界面重读29句、演出证明不重复、此前数据保持通过。已查看实际露牙与持枪画面。

JourneyFreshRoof 1791080022 PASS，去掉旧测试直接Factory.Roof.openAsync入口，改从Start恢复控制舱、真实HUD走至3270附近、点击原屋顶按钮。导师和妮妮两人完整阶梯、平台转身时跟随者不离开平台、四周期攀爬/翻越/落地碰撞、保存失败重试和FactoryRoof接续通过；手部支撑误差最大约0.000122、翻越最小净空大于10。此为程序驱动原生HUD，不是全程OS攀爬。

屋顶E键也使用逐帧isKeyDown，已与控制舱一样改为KeyDown事件并保留ready/storyBusy条件。JourneyFreshRoofDialogue 1791080093由原生HUD走到乌云附近后等待真实输入；CUA短按E成功触发剧情，其余对白推进为原生按钮事件。原11句、手臂纹记绑定、1.8秒光柱、保存失败重试、重读与重入不重复剧情均通过。只把E触发记为OS证据，未把整段称为OS游玩。

证据fresh-control-pod-dialogue-native.json、fresh-control-pod-fox-warning.tga、fresh-roof-route-native.json、fresh-roof-route-entry/stair-landing/landed.tga、fresh-roof-dialogue-native.json、fresh-roof-beacon-native.tga。后续对战来源Test/fresh-roof-dialogue-resume-fixture.txt，主存档保持。


### 2026-10-04：新档屋顶战、失败撤退与乌云永久离队

JourneyFreshRoofBattle 1791080242 PASS，承接本轮屋顶对峙来源及实际采用的妮妮模型，正式HUD移动/射击/火焰完成16.18秒对战。导师7命中剩48生命，妮妮10次模型动作/10命中/0fallback剩84生命，火焰5命中。乌云原射击约1.0667秒、近战和旋风各1秒，分别约0.50/0.40秒攻击点，所有记录动作完整、败退1秒完整；保存失败重试、胜利报告幂等和屋顶接续通过。

JourneyFreshRoofAftermath 1791080327 PASS，对照原2-17五句，乌云抬臂原生事件0.85秒、纹记与1.6秒漩涡增强、完整跳起后约1.58秒进入漩涡隐藏；保存失败重试、重读和重新进入不重复离队通过，实际漩涡入场截图已查看。JourneyFreshRoofAftermathExit 1791080388 PASS，从Start恢复后原返回按钮依次经控制舱、厂区到指挥室，乌云不重新出现，原有其他表保持。后续第三章来源Test/fresh-roof-exit-resume-fixture.txt。

JourneyFreshRoofBattleFailure 1791080414 PASS，独立副本中实际承受攻击20.38秒失败，导师0生命而乌云剩80；未记胜利。重试恢复双方准备状态，射击过程中撤退等待完整射击完成再结算，返回屋顶仍须战斗，未误解锁战后剧情。

证据fresh-roof-battle-native.json、fresh-roof-aftermath-native.json、fresh-roof-aftermath-exit-native.json、fresh-roof-battle-failure-native.json及fresh-roof-vortex-entry.tga。本轮全部为原生HUD/剧情事件测试，不是OS整场战斗。主存档保持。规划P11的新建/继续分离与存档管理仍属后续交付缺口，不能因本轮第二章链路通过而宣称作品整体完成。


### 2026-10-04：新档第三章通讯、学院实走与离队限制

JourneyFreshReconnection 1791080786 PASS，承接本轮第二章撤回指挥室来源，经Start恢复、正式HUD靠近通讯台完成16句，再经指挥室左门—PassageC电梯—PassageD右门进入研发室完成6句监测，沿原门路返回指挥室。首次发现距离门槛、通讯保存失败重试、重读不重复写入、此前数据保持通过。首次1791080708在回程把已完成通讯仍当作首次发现而错误要求禁止远程重读；修正仅对未完成节点执行此断言，失败证据保留fresh-reconnection-replay-gate-failure.json。第三章对白是已有工作稿改编，不称为恢复的历史原对白。

JourneyFreshWuyunDeparture 1791080867 PASS，同一来源独立副本中，乌云18条已采用训练样本保留，saveFormation和任务开始拒绝CHARACTER_DEPARTED；休息室/站台/厂区/废城没有乌云实体，列车公开编队卡也不能把他重新加入。此项场景覆盖使用导航接口，不是这些房间全程实走，所有数据表保持。

JourneyFreshReconnectionResume 1791080910 PASS，第三章通讯和监测完成档经Start正确恢复RDRoom，不回旧工厂检查点、不自动重播通讯、乌云缺席，所有数据表保持。此为同进程重新加载，不是冷启动。证据fresh-reconnection-native.json、fresh-wuyun-departure-native.json、fresh-reconnection-resume-native.json，后续学院防卫来源Test/fresh-reconnection-resume-fixture.txt。本轮未新增OS全程游玩证据，主存档保持。


### 2026-10-04：新档学院三阶段防卫、重创与截图发现

JourneyFreshAcademyDefense 1791081037 PASS，从本轮通讯完成档经Start恢复研发室、原门与电梯途经PassageD/C到A区防线，未直接导航至战场。三阶段52.40秒胜利，导师28命中剩89生命，妮妮23模型动作/20命中剩100生命，火焰11命中；供电和信标各132耐久、实际护送794、使用治疗水1份与库存一致。六只小饕餮吹击/炸弹/横扫/滚动/头槌原生时长及败退完整，保存失败不能离开结算、重试成功、拒绝不完整证明、胜利幂等和公开记录通过。

JourneyFreshAcademyLoss 1791081164 PASS，从Start恢复防卫后A区，接近门槛、8句重创改编对白、1.416秒冲击、伤亡与演出证明原子保存失败重试、三页人员记录、重读不重写、妮妮当前3句对话、受损休息室/研发室和Start再次恢复A区通过。名单区分6名本次牺牲、双子待救援、林睿哲仍活跃、乌云此前离场、阿岩此前牺牲；不允许已牺牲/离场角色参战。

JourneyFreshAcademyDefenseRetry 1791081203 PASS，独立来源副本验证敌人攻击中撤退等待完整动作，重试保留移动/火焰/治疗按钮并恢复初始阶段，再撤退不写胜利、不扣药品。此专项直接打开原生战斗组件，不是公开入口或实际战败验证。

实际查看fresh-academy-loss-scene.tga发现右侧妮妮交互菜单与区域记录文字裁切；流程通过不代表该画面可交付。下一步应修复世界空间交互菜单的屏幕边缘布局并用真实界面重验。证据fresh-academy-defense-native.json、fresh-academy-loss-native.json、fresh-academy-defense-retry-native.json；后续玉与双子来源Test/fresh-academy-loss-resume-fixture.txt。本轮均为原生事件测试，非OS整场战斗，主存档保持。


### 2026-10-04：世界交互菜单边缘修复与真实点击

UI.KeepOnScreen按逻辑窗口宽度投影标题、按钮与提示文字，保留16像素边距；记录原始位置，离开边缘时释放修正，保持原交互发现距离。Interaction的Yue源与生成Lua同步，学院受损提示也应用同一修正。投影回调去重，避免同一测量重复结算。

InteractionBounds 1791082132 PASS，原生组件左边缘、中央、右边缘、回到中央四例均通过，中央恢复原位置。此前测试将parent.x=500误当中央，实际标题/按钮右界881.03超出880安全边界，因此1.76的位置修正是合理夹取而非残留；改为真正位于中央的0后通过，没有放宽断言。

InteractionEdges 1791082157 PASS，从本轮学院重创档独立副本恢复A区，标题、菜单和提示均在安全范围；查看实际画面并用真实鼠标点击妮妮对话成功，全部数据库表保持。仅点击有OS输入证据，边界遍历为原生组件测试。证据interaction-bounds-native.json、interaction-edges-native-os-click.json、interaction-edge-fixed.tga。主存档保持，整体Game 0仍在开发验证中。


### 2026-10-04：新档实际学院路线、玉登场与双子护送

JourneyFreshJadeArrival 1791082359 PASS，承接本轮学院重创存档，经Start恢复A区，正式HUD沿A区—C区—D区电梯与研发室房门实际进入，没有直接导航研发室。首次1791082293使用旧测试固定6秒前进，真实门口出生只走到1750，未抵达墙体，故该失败不能判定碰撞失效；改为等待到达4400后持续顶墙1秒，实际止于4468.50。12句改编对白、1.217秒通道解除、双子处于保护场、保存失败重试、重读不重写、穿过4674.75、Start重新加载及三角色idle循环通过。未把首次对话误当救援完成。

JourneyFreshTwinsEvacuation 1791082414 PASS，从上述来源Start恢复研发室，走近公开救援入口，使用原HUD实战34.89秒。双子分别实际行走1249.06/1209.48，最低间距160.42，抵达出口剩100/48生命；导师15命中剩64生命，妮妮12模型动作/10命中剩100生命，火焰11命中。保护场吸收38伤害，场外仍扣血；两段四守卫动作与败退完成、存档失败禁止退出并重试、无效证明拒绝、胜利幂等、名单当前已获救但历史伤亡记录不改写、此前表保持通过。

JourneyFreshTwinsOutcomes 1791082495 PASS，同来源独立副本验证前置锁、攻击中撤退等待吹击完成且撤退后不再扣血、重试恢复双子与护盾、再撤退不写胜利。此专项用导航进入研发室，未覆盖真实战败。

已查看玉与双子恢复和出口截图；长交互标题/按钮文字超出原底板宽度，保护场与损坏特效仍为初版，佛陀机器人仍缺运行素材，不能视作最终美术完成。上述测试均为原生HUD事件驱动，非OS全程游玩。证据fresh-jade-arrival-native.json、fresh-twins-evacuation-native.json、fresh-twins-outcomes-native.json，首轮距离失败另存；后续力量代价对话来源Test/fresh-twins-evacuation-resume-fixture.txt。主存档保持。


### 2026-10-04：交互底板随文字扩展与新档撤离窗口

修复原Interaction固定228宽标题、309宽按钮容不下第三章长文案的问题。UI.FitInteraction保留原字体与美术底板，按文字宽度加左右留白扩展标题背景、按钮背景、遮罩和实际点击区域，再按新尺寸排列菜单；Yue源和生成Lua同步。InteractionTextFit 1791082718 PASS，长短标题/按钮、左右朝向、左/中/右边缘和回中央共16例，文字位于底板内、屏幕安全边距和回位通过。已查看新档研发室截图，两个重读按钮完整承载文字。尚未补新增宽度最外侧的真实鼠标命中专项；远处世界提示文字仍有出屏，应后续按距离显示策略统一整理，不能把所有提示强行挤在同一屏边缘。

JourneyFreshJadeDistance 1791082667 PASS，从本轮双子实际获救来源Start恢复研发室，原HUD走近玉支撑点，8句力量代价工作稿、当前五位说话者肖像切换、通讯空角色清除旧肖像、保存失败重试、有限撤离窗口解锁、重读8句与初见12句不改当前状态、Start再次恢复、此前数据保持通过。使用已有插画/Spine资源，不代表肖像美术终验。后续终章来源Test/fresh-jade-distance-resume-fixture.txt。证据fresh-jade-distance-native.json、interaction-text-fit-native.json及fresh-jade-distance-restored.tga；本轮为原生事件验证，主存档保持。


### 2026-10-04：新档最后的约定与正式出口进入终章

JourneyFreshLastPromise 1791082826 PASS，从本轮玉交谈完成档Start恢复研发室，实际走近撤离出口。沿用已确认机动型辅助机，准备界面预选货运后取消不覆盖历史选择，不再沿用旧测试的“没有选择记录”假设。正式HUD三段43.30秒胜利，导师24命中剩85.55生命、妮妮18模型动作/12命中剩36.16生命，火焰18命中；机动机实际护送1740、剩10耐久、各动作循环有记录。掩体阻挡3次、场外累计伤害72.34、维生回复44.05，急救任务补给1份未使用。保存失败阻止离开、重试、证明损坏拒绝、胜利幂等、公开记录和此前表保持通过。

JourneyFreshFinalBetrayal 1791082981 PASS，从新档胜利后Start恢复，走到正式出口打开终章；攻击中返回研发室不保存未完剧情，再由出口重新进入。首次1791082924只等待旧世界移除就立即断言新场景已就绪，触发测试时序失败；修正等待研发室与出口加载后通过，失败证据保留。15句工作稿、通讯钟冻结、林睿哲实际接近330/约2.37秒、1秒完整攻击/0.4秒命中点、女导师0.6秒受击与1.133秒倒地末姿态保持通过；保存失败不能离开、重试、无效证明拒绝、重读不重写、同进程Start进入旅程回顾通过。后续回顾/署名来源Test/fresh-final-betrayal-resume-fixture.txt。

已查看护送后研发室和终章末姿态截图；独立终章按钮仍使用固定InputButton底板，长文字问题尚未由Interaction修复覆盖，需继续处理。环境损坏美术与演出节奏仍待精修。本轮均为原生事件驱动，未宣称全程OS试玩或冷启动验证。证据fresh-last-promise-native.json、fresh-final-betrayal-native.json及对应截图，主存档保持。新档链路接到结局不等于Game 0整体完成，仍有存档入口、机器人、最终美术、分发与平台验收缺口。


### 2026-10-04：独立按钮长文字修复与新档回顾署名

把按钮按文字扩展的调用移到共用UI.InputButton，XML源和Lua同步；Interaction不再重复调用，避免重复缩放底板。终章独立按钮也获得完整背景和点击范围。InputButtonMouse 1791083276 PASS，实际显示“旅程回顾与署名”，按钮从309扩展到431.2，CUA鼠标点击新增右侧区域触发原Tapped事件。InteractionTextFit 1791083317再次通过长短文案、左右朝向和四位置16例。该OS证明仅覆盖独立按钮新增区域，非结局全流程鼠标游玩。

JourneyFreshEndingFlow 1791083250 PASS，接续本轮新档终章来源，Start进入旅程回顾，中途关闭不标完成、继续读完回顾/署名、署名写入失败重试、标题页继续/探索/重放、返回受损研发室、结局回顾弹层阻止底层返回、同进程Start再次进入回顾、不重发奖励和此前表保持通过。首次1791083200把已存在的Game0EndingViews阅读记录表列入全不变断言，故在合法阅读更新后失败；修正排除该唯一预期修改表，保留阅读戳重复进入不变检查，失败证据归档。后续来源Test/fresh-ending-resume-fixture.txt。

证据fresh-ending-flow-native.json、input-button-expanded-os-click.json、input-button-layout-regression.json。主存档保持。整体尚未交付：仍需新建/继续存档入口、机器人及最终美术、完整OS通关、分发包与平台验收，不能将原生链路到署名等同作品完成。


### 2026-10-04：P11启动页与保留旧档的新旅程

init启动改为Save.Title，复用原banner和InputButton，提供继续旅程、开始新旅程、选择已有旅程。Save.Slots识别原lsd.db和独立旅程文件，新建使用时间戳加序号避免同秒覆盖；选择记录独立保存，读取前检查SQLite quick_check，拒绝非法路径/缺失/损坏文件。打开后仍交给原Start恢复剧情；直接Start的既有隔离测试入口保持。未接触主lsd.db。

SaveSlots 1791083595 PASS，在单独QA目录复制本轮通关来源作为旧档，验证连续新建互不覆盖、旧档末章存在、损坏文件拒绝且不改当前指针、已打开存档时禁止再开。启动页首次截图发现根节点未设置尺寸导致画面偏移，补上根尺寸及窗口更新后实际截图居中；CUA点击“开始新旅程”产生全新空库，旧档文件逐字节不变。SaveContinue 1791083665 PASS，从同一隔离目录的启动页继续旧旅程，经原Start进入结局回顾，全部表保持。后续将旅程标识显示为创建日期，避免向玩家显示文件名。

证据save-slots-native-os-new.json、save-continue-native.json。本轮OS仅覆盖新建入口，继续为原生按钮事件。P11仍未完成：新档经此入口完整建角与冷启动继续、多版本迁移和备份恢复、选择列表更多操作及异常写入故障注入仍待验证，不能把启动页接入视作全部存档验收。


### 2026-10-04：P11读取前快照与非覆盖恢复

Save.Slots在已有存档quick_check成功后、交给Start加载和迁移前使用SQLite VACUUM INTO生成独立一致性备份。备份失败则停止本次读取，保留原档；新建空档不先备份。选择旅程页增加“从备份恢复新旅程”，按时间与同秒序号倒序查找健康备份，恢复为独立旅程，不覆盖损坏原档；损坏的新备份不会遮蔽较早健康备份。当前备份均保留，尚未提供清理/保留数量策略。

SaveBackup 1791083850 PASS，QA目录复制已通关来源，成功加载前产生一份备份，原文件逐字节保持。随后仅在QA中损坏原文件并添加更新的坏备份，真实CUA鼠标点击恢复，跳过坏备份后创建lsd-journey独立文件，全部业务表与原来源一致，损坏原文件仍保持原样。证据save-backup-os-restore.json；没有读取或修改用户主lsd.db。随后将同秒备份排序改为数字序号，避免10排在9之前，语法通过；多份同秒备份专项仍待补。

P11继续未完成：写入/磁盘故障注入、跨版本迁移、缺失主文件时的备份发现、新入口完整建角与冷启动续玩、备份容量管理仍待补齐。本轮证明损坏文件恢复与真实入口，不代表全部存档可靠性验收。


### 2026-10-04：缺失原档的备份发现与失败重试

Save.Slots列表现在合并有效存档名及备份所对应的原旅程名并去重；原档缺失仍可在选择页找到备份，显示“原文件缺失，可从备份恢复”，不提供无效读取按钮。默认继续仅选择实际存在的原文件，避免自动选择缺失档。

SaveRecoveryEdges 1791084044 PASS，在独立QA目录仅放置两份同秒备份（序号9、10），没有原lsd.db。选择页显示恢复入口，恢复读取第10份专用标记，证明数字排序和缺失档发现；恢复后未重新创建原lsd.db。随后通过替换该实例的backup方法注入BACKUP_FAILED，确认禁止加载、解除附加数据库、原文件和选择指针字节不变，恢复方法后重试成功。故障注入是方法级失败，不称为实际磁盘满或断电测试。证据save-recovery-edges-native.json，主存档保持。

下一步按已有Game0Opening正式开场测试接入新启动页，覆盖实际建角后继续；冷启动、迁移与存档写入原子性仍需独立验证。P11不因此标记完成。


### 2026-10-04：新启动页完整建角、教程到学院与继续

SaveOpening 1791084165 PASS，在全新独立QA目录通过Save.Title真实鼠标点击开始新旅程，原Start接手新库，没有预置Config、剧情完成或战斗血量。原开场正常播放，通过CUA真实输入JourneyQA姓名，原生选项选择女性；教程原HUD移动与射击19次完成实际命中战斗，经物理出口进入PreparationRoom，原流程保存tutorialCompleted。实际学院截图已查看，角色/妮妮/摇杆/交互菜单正常。新档Test/save-opening-resume-fixture.txt指向该独立目录内的旅程。

SaveOpeningContinue 1791084400 PASS，重新加载测试环境后经同一目录Save.Title继续按钮进入原Start，恢复备战室，不重放开场或教程；姓名、女性角色、skipOP、教程完成及全部Config字段保持。此为同一引擎进程重新加载，不是冷启动；继续按钮由原生事件触发。OS范围仅新建点击和姓名输入，不将教程程序操作称为整段OS试玩。

证据save-opening-native-os-input.txt、save-opening-continue-native.json。用户主存档保持。P11的新建到学院/继续主路径获得证据，冷启动、版本迁移和断电/磁盘写入可靠性仍待独立验收。


### 2026-10-04：新旅程真正冷启动与鼠标继续

结束已完成前轮测试的原生引擎PID66526，确认进程查询为空后，通过同一debug引擎cli doctor --fix启动PID73986（1.9.3.11 macOS）。在新进程运行SaveColdContinue，使用本轮经新启动页/真实姓名输入/教程实际通关产生的独立旅程，实际CUA鼠标点击继续。1791084544 PASS：恢复PreparationRoom及导航、姓名JourneyQA/女性角色/skipOP/教程完成保持，Config表完全不变，未重放开场教程。启动页与恢复后人物/妮妮/交互/摇杆画面已查看。

证据save-cold-continue-os.json附进程替换观察。测试先在同一新进程只读检查该QA库Config、解除附加后再经标题页打开，未提前加载Config对象或Start；可证明旧进程缓存非恢复所需，但不是最终分发包的直接双击冷启动。用户主存档保持。本轮补齐macOS调试引擎下该教程检查点的冷进程恢复，其他剧情检查点、正式分发、多平台与迁移/断电可靠性仍需验证。


### 2026-10-04：旅程选择事务记录与旧选择兼容

新增Save.Selection，用独立lsd-save-catalog.db及SQLite事务保存当前旅程，替代直接覆盖lsd-current-save.txt。未有目录数据库时继续读取原文本选择；成功打开后写入事务记录，旧文本保留。事务失败解除旅程数据库附加并返回错误，不开始游戏；目录文件损坏明确提示，不悄悄重置选择。业务存档和选择目录分离。

SaveSelection 1791084749 PASS，隔离目录中验证旧文本读取、新目录优先、旧文本保持；SQLite触发器在选择INSERT时注入FAIL，原选择与原旅程字节保持、数据库别名释放，删除触发器后重试成功；损坏目录文件返回CATALOG_UNREADABLE。此为实际SQLite事务失败注入，不是断电/磁盘满测试。SaveOpeningContinue 1791084775再次从本轮建角存档通过标题页继续进入学院，Config/身份保持，证明旧选择迁移不打断恢复。

证据save-selection-transaction-native.json、save-selection-continue-regression.json。用户主存档保持，本轮未新增OS或冷进程证据。仍需完整备份容量策略、更多跨版本存档迁移、正式分发和全平台验收。

### 2026-10-04：佛陀机器人分层素材与原生动画样机

重读yu人物设定和周大西yu-buddha-d原图：多臂、白金装甲、背后光环、双手托举与保护金光是明确要求。现有游戏/下载Spine目录只找到yu人物，没有佛陀机器人运行资源。使用内置image_gen基于原图生成3×2透明部件图，初稿及修订稿保存在Docs/artwork/buddha-guard，README记录来源、提示词和限制；不把AI衍生素材归作原画师交付。

新增独立BuddhaPrototype原生样机，使用图集裁切建立六条肩—肘—腕父子链、悬浮、光环及Guard平滑切换。实际渲染发现Sprite更换textureRect不自动改显示尺寸导致拉伸，已显式设置512方格尺寸；镜像移到左右共同父节点，修正两侧动作朝同侧的问题。已查看idle/guard截图。仍存在上方肩部悬空、重复肩甲和托举手势不合格，比例也未与玉同屏终验，所以没有接入正式救援场景，也没有宣称动画完成。下一步必须修正肩根锚点/遮挡、托举动作与护盾判定同步，再进行完整循环测试。

证据buddha-prototype-idle.tga、buddha-prototype-guard.tga；运行Test/BuddhaPrototype.lua。此轮为资产与可运行样机进展，仍待制作验收。


### 2026-10-04：佛陀样机肩根、遮挡与恢复时序

修正肩根位置至躯干范围，把上中两对手臂的镜像父节点置于身体后方，下方一对保持前景。托举手掌朝内，逐帧抵消肩肘旋转保持水平，避免原先双掌随手臂下翻。实际guard截图已查看，较前轮消除上方整段悬浮和重复肩甲直接盖住主体的明显问题；手掌靠拢、最终关节轮廓与玉乘坐姿势仍需继续精修。

Guard/idle切换改为固定0.2秒smoothstep恢复，相同状态重复发射不重启过渡。BuddhaRig 1791085502 PASS，四次过渡及264帧检查通过，肩肘腕父子链保持，托掌角度累计误差最大约0.00000191度。此为节点结构与动作状态验证，不能替代贴图像素关节和完整动作美术验收；没有接入Ward或正式战斗。

证据buddha-rig-native.json、buddha-rig-idle-recovered.tga及更新的buddha-prototype-guard.tga。下一步为玉同屏比例、召唤/收回/护盾受击动作和正式保护场联动。


### 2026-10-04：佛陀机器人接入研究区保护场与撤离战斗

新增BuddhaWardView，使用运行目录Image/Rescue图集，将六臂机器人显示绑定到真实Ward：0.6秒召唤、0.4秒收回，吸收伤害时光环闪动；耗尽后重新open也不重新出现。表现层不改变容量、范围、伤害或移动速度。Arrival和Rescue.Battle均接入，机器人位于玉身后，保留现有摇杆、技能按钮及战斗逻辑。已查看玉同屏、研究区恢复和战斗截图。当前是守护表现，未实现托举玉乘坐及机器人武器攻击，关节轮廓与最终美术品质仍待验收。

BuddhaWardView 1791085688 PASS：场外不吸收、场内两次受击、容量溢出造成10点实际伤害、耗尽收回及不复活。JourneyFreshJadeArrival 1791086099 PASS：从学院损失QA档实际经A/C/D进入研究区，开启通道、保存失败重试、重读和恢复保持；恢复后机器人guard可见。JourneyFreshTwinsEvacuation 1791086184 PASS：原生HUD驱动完整两段撤离战斗，护盾两次吸收共38点，对应两次机器人受击脉冲；双子抵达出口后返回研究区，机器人正确隐藏，保存故障重试和原有数据保持通过。测试均为独立QA数据库及程序触发原生控件，本轮不称为OS全程试玩。

证据buddha-ward-view-native.json、buddha-arrival-integration-native.json、buddha-rescue-integration-native.json、buddha-rescue-battle.png。另按用户要求重新验证狐狸仅动画0.85倍、移动240保持：ControlPodFoxMotion 1791085947 PASS，实测walk循环1.183秒、idle2秒，左右移动/停止无漂移，证据fox-animation-speed-recheck-native.json。整体Game0仍有美术、完整OS试玩、跨平台与发行验收待完成。


### 2026-10-04：保护场金光、容量反馈与受击扩散

Ward表现从单线圆圈扩展为低透明度金色填充、连续三层边缘柔光和缓慢流动光点；亮度随剩余容量降低，保护半径不随强度缩小。实际吸收伤害时记录命中世界坐标，并从该处扩散短波纹。采用闭合多边形描边修正首版独立线段叠加造成的串珠接缝。重新open清除上次闪光坐标/时间，同时保留剩余容量及原0.6秒展开判定。

BuddhaWardView 1791086387 PASS，补充关闭再开后残留闪光清除、容量保持、展开期间不吸收检查，原有场外/场内、溢出伤害、耗尽隐藏保持。JourneyFreshTwinsEvacuation 1791086430 PASS，两段实际战斗、两次吸收对应两次机器人闪光、撤离后隐藏、保存失败重试均保持。已查看黑底受击预览和实际研究区战斗截图，原有角色与HUD保持可辨认；本轮为程序操作原生控件，不是OS全程试玩。

证据buddha-ward-gold-native.json、buddha-ward-gold-battle-native.json、buddha-ward-hit.png、buddha-rescue-battle-gold.png。托举乘坐与机器人攻击动画仍待制作，Game0整体完成验收未通过。


### 2026-10-04：标题页前置存档版本检查

新增只读Save.Compatibility，对现有13种Game0版本表按已实现版本1核验；版本较高、未知带版本模块或已知表缺失版本列时，Slots.attach在备份/选择记录/Start之前拒绝并释放数据库。原Config和无Game0版本表旧档仍可进入已有初始化流程，不新写全局版本、不伪造迁移。恢复备份使用相同只读检查，可跳过不兼容的新快照并恢复较早兼容快照。标题页提供较新版本/不支持结构的中文提示，保留现有旅程选择入口。训练JSON内部版本仍由Training.Store负责，本轮不声称已覆盖所有模型迁移。

SaveCompatibility 1791086733 PASS：真实已通关QA库字节不变；注入story版本999后通过标题页读取按钮拒绝，原档字节、选择记录、备份数量不变；未知模块和版本0拒绝；较新备份不掩盖旧的健康备份，恢复到新旅程；仅旧Config数据可打开。SaveOpeningContinue 1791086766 PASS，从先前真实建角/教程通关QA档经标题页继续，恢复学院，身份和全部Config保持。本轮为同进程原生控件测试，无新OS或冷启动证据。

证据save-compatibility-native.json、save-compatibility-continue-native.json。更新开发首页，移除初始盘点期过时描述，明确分段三章证据与最终验收的差别。A11/P11仍部分完成：更全面的跨版本迁移、磁盘写入故障、备份容量策略与最终发行包待验证。


### 2026-10-04：隐藏HUD和后台切换的输入释放

发现HUDMove只判断自身visible，父HUD被Story.Display隐藏时仍可能继续输出保持的虚拟摇杆方向。新增InputAvailability沿父链检查可见性，并监听引擎AppEvent后台/返回前台事件。HUDMove在隐藏或后台时清空虚拟摇杆和短按缓存；HUDControl清空待发射并发送Skill.Ended，避免恢复后补发旧按键。同步Yue和生成Lua，保留现有摇杆/技能按钮。

HUDInputAvailability 1791087001 PASS：原生HUD置于隐藏父节点时释放持续右移，隐藏期间J与摇杆事件不排队；后台事件立即释放左移、拒绝缓存射击，前台后新J仅发射一次；剧情隐藏/显示及Cleanup释放通过。此为程序触发的原生事件验证，没有真实OS失焦、移动设备后台或训练样本数量的证据。当前引擎桌面SDL失焦仅释放Controller，未向游戏发送AppEvent；桌面焦点处理、后台训练采样和暂停恢复仍是A14待验收项，不以此局部修复宣称完成。

证据hud-input-availability-native.json。

ControlPodFoxMotion 1791087026回归PASS：正式控制舱场景中原HUD左右移动/释放、狐狸完整走路和idle循环、停止无漂移及全部存档表保持通过；动画0.85与移动240不变。证据hud-input-fox-regression-native.json。


### 2026-10-04：训练示范的输入中断与恢复

Training.Level将示范输入可用性接入共享HUD可见性/后台事件检查，清除自身held方向并停止非攻击移动，隐藏时不再轮询等待/刀击和持续移动示范。Arena.request在读取状态与Recorder之前拒绝被暂停的demo请求（INPUT_SUSPENDED），不把隐藏期间输入计为成功样本或拒绝样本；试战模型执行不受该demo入口限制，不中断已经开始的攻击动画。

TrainingInputAvailability 1791087239 PASS：复制已完成协作剧情的QA档，分别打开妮妮莉特和乌云原训练界面；通过原摇杆各产生1条有效移动样本，Story.Display隐藏后速度归零，直接射击请求、Skill.Began及隐藏摇杆都不增加样本/拒绝计数；模拟后台事件时等待与射击也不记入；回前台后原等待按钮各新增1条样本。两个角色最终均2条本轮样本，已采用Game0Training整表保持不变。证据training-input-availability-native.json。

此为原生控件与AppEvent注入验证，不是移动设备后台或桌面失焦实测；不证明整个战斗后台暂停/计时和全平台输入已完成。A14保留实际平台验证缺口。


### 2026-10-04：训练界面小窗口真实鼠标验收

在TrainingInputAvailability建立的独立QA场景中，使用CUA真实拖动macOS游戏窗口，原生读取App.bufferSize确认1366×768和1280×720。1366×768下真实点击远处对练、等待技能、结束示范，样本由2变3（等待由1变2），进入review并显示样本不足提示。1280×720下点击中距对练、枪械技能和结束示范，样本变4（laser1），小饕餮HP100→80，进入review。两尺寸截图实际查看，当前状态文字、两行菜单、切换学员与底部技能控件完整，点击区域有效。随后真实拖动恢复原1792×1136渲染窗口。

证据training-1366-os.json/png、training-1280-os.json/png。OS证据范围仅本轮窗口调整与上述控件点击；前2条样本来自前轮原生测试，不称为从零全程鼠标训练，也未采用或覆盖已有成果。此轮补齐乌云训练界面两个尺寸的局部验收，候选三场长报告、其他场景与1920×1080仍需检查，1280×720桌面窗口不等于移动触摸真机通过。


### 2026-10-04：真实鼠标三场对照与结果文案修正

在前轮乌云QA训练继续使用CUA点击近距刀击、远距射击及结束示范，样本达到6条、生成候选；再实际点击三场试战，完成基础AI三场与候选三场。两者均3/3胜，候选平均生命约88、16.6秒，基础AI约93、6.5秒。6条样本中最初2条为前轮程序生成，后4条来自两轮真实鼠标，不标为从零OS训练。未采用该候选。完整实际samples/candidate/evaluation保存在training-comparison-os.json。

发现原报告固定“各有取舍”，与本轮基础AI在三个指标不劣且两个更好不符。新增ComparisonText，按胜场、生命与用时给出候选更好/基础更好/接近/各有取舍四类提示；状态消息与对照报告共用判断，生命0.5、时间0.05容差对应显示精度。报告增加半透明暗底，改善角色后景上的可读性。

TrainingComparisonLayout 1791087832 PASS，使用刚获得的真实比较数据重放报告界面，四类判断通过；1366×768实际截图已查看，报告、菜单不重叠，显示基础AI更好及补充示范建议。该布局重放不是又一次战斗胜利；候选与样本只置于隔离测试内存，未覆盖采用成果。证据training-comparison-layout-native.json、training-comparison-1366.png。窗口已恢复，其他尺寸/报告状态与全面学习体验验收仍待完成。


### 2026-10-04：训练室往返20轮与引用趋势

新增TrainingCycles，在隔离协作剧情QA副本反复通过训练室实体位置/原摇杆接近终端、终端进入VR、原等待按钮记录一次示范、原返回按钮返回训练室，连续20轮。每轮检查仅一个训练HUD和一个训练控制面板、单次输入仅1条有效样本、旧arena已closed，采集C++对象数、Lua引用、调用引用、Lua内存与弱引用保留数。该循环不是20轮完整建树/试战/采用。

1791088123 PASS：对象997–998，Lua引用恒156，调用引用恒319，每轮保留arena恒1；已采用Game0Training整表不变。Lua内存首末3638.03→3642.89KB，约4.86KB增长；额外对照清除已落盘的20条测量记录后回收约5.00KB，说明本次小幅增长由测量记录即可解释。源码中全局UnitAction定义闭包引用最近arena且同名覆盖，符合保留1个且不随轮数增长的观察；未据此声称所有资源完全释放。

证据training-20-cycles-native.json。两次20轮运行（首次1791088014用于观测，第二次加入引用上界及记录内存对照）均无崩溃。程序驱动原生控件，不是OS20轮试玩；30分钟持续运行、建模中退出、全核心循环及音频叠播仍待验证，A15未完成。


### 2026-10-04：30分钟完整训练循环长稳启动（尚未完成）

TrainingSoak运行1791088353已启动，隔离库lsd-training-soak-qa-1791088353.db。每轮通过原训练室终端进入、近中远三段各实际射击和等待（6条成功样本）、建模、基础/候选/旧模型三场对照、采用保存并重新读取Progress、返回训练室；目标同时满足至少20轮与1800秒。记录引用、对象、Lua内存、旧arena弱引用和每轮胜场，最终仍需人工审阅趋势。启动时全局赋值被引擎严格全局规则拒绝，发生在数据初始化前；改为package.loaded的测试状态句柄后重新启动成功。

本次最后观察：首轮65.2秒完成、候选与基础均3胜、保存再读成功；第2轮评估进行中，心跳约0.03秒，未完成长稳验收。运行中的权威句柄为package.loaded['_lsd_training_soak_state']，报告Test/training-soak-result.json。后续必须通过Tools/observe-training-soak.json作为cli agent command的输入读取当前句柄与心跳，不只凭报告文件判定活跃；不要cli run其他入口或重启引擎打断当前测试。只在终态或句柄消失时再决定下一步。A15仍未通过。


### 2026-10-04：新增佛陀素材来源与结局署名补齐

长稳运行1791088353期间进行独立来源核对，不重载测试。Image/Rescue/buddha-guard-source.json记录运行图集、原设计相对路径、周大西署名、原图及运行图集SHA-256、生成日期、提示词记录、衍生制作属性和未完成动作边界。运行图集与记录的parts-v2逐字节哈希一致。Ending.Credits升为版本2，保持原社区姓名分组，另加补充素材制作说明佛陀部件为基于周大西设计的AI辅助制作；没有将衍生图当作原画师交付。狐狸原图来源元数据中“关节动画待制作”的旧状态更新为原图用于立绘/参考、场景由现有Spine运行资源播放。

证据buddha-source-audit.json；Credits Lua语法通过。为避免打断长稳，本轮尚未重开结局检查新增署名的实际排版，必须在长稳结束后补验；未声称整体版权/发行资产审计通过。


### 2026-10-04：运行资源目录与干净发行暂存

长稳1791088353继续运行期间，静态发行检查发现Researcher与InterrogationActors仍从Docs/artwork加载研究员/乌云/男女导师骨骼及导师hand-fit数据。新增Tools/install_interrogation_runtime.py，将6份已导出文件逐字节同步到Spine/StoryActions，运行引用改为正式资源路径；source-manifest.json记录导出来源及哈希，--check检查拷贝/元数据过期。研究员导出工具末尾调用安装步骤，其他角色重新导出后也应运行安装工具。原Docs制作工程保留。6文件一致性及Lua语法通过，当前长稳未使用这些演出，未重载引擎，搬迁后的原生演出验收待长稳结束。

新增stage_game0.py构建不含Docs/Test/Tools/.agent/.git的独立资源暂存目录，拒绝覆盖、项目内输出及资源符号链接；扫描运行源码中的开发路径。/private/tmp/lsd-game0-stage-20261004-a已生成870文件、260454623字节，逐文件SHA-256复核全部通过。它是待验证的资源目录，不包含平台引擎、不称为可分发安装包，也不称为干净环境启动已通过。证据runtime-stage-static.json。

长稳结束后优先验证搬迁的研究员和男女导师审问演出、Credits v2实际排版，再从暂存目录验证标题/新建/继续及完整旅程。后续源码变更必须生成新的暂存目录，不将旧清单视为最新包。


### 2026-10-04：暂存资源图集完整性与全Lua语法

新增audit_runtime_atlases.py，对独立暂存目录检查Spine图集页存在性/PNG尺寸、clip图片及裁切边界、model到clip文件链接，并拒绝越出暂存根目录的资源引用。20261004-a静态检查PASS：86份atlas、89张贴图页、22份clip/399个裁切区、11份model，未发现丢失贴图或越界区域。另逐个luac检查随包269个Lua文件，全部语法通过。证据runtime-atlas-audit.json、runtime-lua-syntax.json。此检查不验证Spine骨骼语义、所有动态加载路径、音频播放或原生运行，不能替代发行包通关验收。

长稳1791088353当前已完成10轮、约682秒，第11轮评估中，实时句柄心跳约0.05秒；最近循环对象1022、Lua引用160、调用引用323保持。继续保留该引擎会话，尚未达到30分钟，不标为长稳通过。


### 2026-10-04：暂存目录隔离启动测试准备（未执行）

读取当前引擎Content实现确认：searchPaths setter清空路径缓存，默认回退为引擎assetPath，并非用户writablePath；桌面writablePath可临时切换并恢复。新增Test/StagedContinue.lua，计划在长稳结束后使用20261004-a资源目录、单独/private/tmp存档目录及既有真实建角QA副本，清除游戏模块/资源缓存，只保留暂存目录的游戏搜索路径，执行未修改的暂存init.lua，再通过标题继续到学院。检查关键资源解析到暂存目录、Docs运行资源不可用，退出测试恢复搜索路径和写入目录。

目前只完成Lua语法检查，未执行该测试，不声称隔离启动成功。调用者必须先读取长稳实时句柄确认终态，不能为了跑此入口打断长稳；入口内防护不能替代调用前检查，因为cli run可能先清理上一场景。即使该测试通过，它也只是缓存清理后的同进程原生验证，最终发行冷启动仍需另验。

### 2026-10-04：长稳失败定位与提示框遮罩修复

运行1791088353已失败：约907秒，在第15次进入训练时缺少trainingTerminal。第14次返回时UI/FitInteraction:21先抛出mask为空的异常，导致入口没有创建，因此之前14轮不能作为完整稳定性通过。原始报告归档training-soak-first-failure.json。新增InteractionGC强制回收UI子节点的Lua包装：修复前第1例即重现同一异常，原生stencil仍有效，而临时mask别名已消失。

FitInteraction改用原生ClipNode.stencil，并以原始贴图宽度计算拉伸倍率，避免反复调整时把已经扩展的底板缩回去。正反向各50次长文字标题和按钮创建、回收、尺寸/遮罩一致性检查全部通过（1791089767），证据interaction-gc-before/after.json。长稳返回阶段现在要求训练入口确实创建完成才计入循环；失败证据保留，新一轮30分钟完整循环另行运行，A15仍未通过。

### 2026-10-04：隔离资源目录继续游戏通过

重新生成包含遮罩修复的20261004-b暂存目录：870文件、260454733字节。StagedContinue首次因测试去掉引擎标准库路径而失败；修正为只保留暂存游戏路径与引擎Script/Lib，不保留开发项目路径。1791089900原生运行通过：独立QA存档目录、未修改暂存init、标题继续、原女主JourneyQA与skipOP记录恢复、到达备战室；关键资源解析到暂存目录，Docs制作文件不可用。实际截图已检查，证据staged-continue-native.json和staged-continue.png。

这是同进程清理模块和缓存后的资源隔离启动，尚不证明可分发安装包、独立冷启动或发行包完整通关。正式发行与整体作品验收继续保持未完成。

### 2026-10-04：建模退出专项准备（未执行）

长稳1791089961期间新增Test/TrainingBuildExit.lua，未重载运行场景。专项使用独立QA数据库、妮妮莉特和乌云各1500条明确标注的合成示范，直接调用真实原生C4.5；依据引擎BuildDecisionTreeAsync内部wait必然yield的实现，手动推进调用协程到building后销毁真实Arena世界，再创建下一训练会话，最后恢复旧协程，要求返回CLOSED、旧candidate为空、新会话及已采用记录未改动。随后新会话以12条样本正常建树并验证模型，避免只验证取消而未验证之后还能训练。

只完成语法检查，尚无运行结果。该专项不是真实玩家输入/操作系统退出测试；不得拿合成样本当作实际游玩证据。必须先确认长稳权威句柄终态再执行，不能覆盖当前长稳。普通返回训练室按钮在building期间仍不执行返回，专项覆盖的是场景清理后的异步回调隔离。

### 2026-10-04：暂存音频完整解码与项目说明同步

保持长稳1791089961场景运行，独立检查20261004-b资源目录。新增audit_runtime_audio.py，使用ffprobe读取音轨信息、ffmpeg完整解码并遇错误退出，记录逐文件SHA-256。13首音乐和2份WAV音效全部通过，证据runtime-audio-decode.json。只证明资源可完整解码，不证明Dora实际播放、音量、循环接缝、音频叠播或平台听感通过。

运行Lua/Yue/XML/TL未发现开发路径硬引用；文字扫描命中的StoryPortrait原画来源字段仅作出处说明，不参与加载。6份StoryActions正式运行文件与制作导出/来源清单再次逐字节一致。README更新过时的“2-8待接入”，明确三章分段证据、仍待连续试玩/美术/设备/音频/长稳/发行验收，以及QA存档和测试场景替换约束。README变更尚未重做暂存，后续最终打包必须生成新目录。

### 2026-10-04：玉乘坐动作原资源结构核对

重新核对yu.md：下方双臂应形成座椅承载玉移动，现有护盾机器人展示不满足这一项。导出原yu.skel为Docs/artwork/yu-riding/source-export/yu.json，并使用引擎同版解析器记录原区域尺寸；原skel/atlas/png均未改动，来源哈希和限制记录于source-inventory.json。原骨骼84个，仅fmove/idle/idle1，无乘坐动作。

识别两条腿链及四个IK约束；当前Spine 4.3格式将约束放在constraints，直接旋转腿骨会被IK覆盖。长裙/饰带有独立权重链，不能把原站姿整体抬高当成坐骑演出。4.3.26编辑器读取原4.3.08二进制有版本及nonessential内部网格边缺失提示，因此尚未回写运行资源或声称视觉通过。下一步需先原动作往返核对，再制作坐下/乘坐/落地和双掌接触；长稳期间没有切换场景。

### 2026-10-04：第二次长稳中途资源趋势

运行1791089961继续，无场景重启。前12轮对象1641–1642、Lua引用572、调用引用529、旧Arena弱引用保留1。第7→8轮Lua堆一次增加132.24KB，后续每轮增量中位约0.456KB；尚未确认突增来源，不能据引用稳定宣称内存验收通过。新增Tools/summarize_training_soak.py，离线汇总范围、门槛和突增，不从文件推断会话活跃，也不自动判定A15通过。中期报告training-soak-interim-trend.json。需终态后区分测试记录占用、开发运行环境开销与游戏持有对象，再作验收判断。

### 2026-10-04：玉原动画往返几何验证通过

将yu源JSON重新导出独立roundtrip-export/yu.skel，使用同版Spine原生运行库对比原二进制，三个原动画各121个时间采样、515202个顶点坐标比较通过；最大世界坐标误差0.00124359，小于0.05阈值，时长与槽位/附件匹配。证据yu-original-roundtrip.json包含输入哈希及算法来源。此结果降低导出破坏原动作的风险，但不验证纹理/绘制顺序、新坐姿或角色接触的画面，未替换游戏资源，乘坐制作仍未完成。过程不使用正在长稳的游戏场景。

### 2026-10-04：找到桌面Spine原工程，修正素材制作来源

用户指出原工程在桌面后，定位 `/Users/Jin/Desktop/LSD/LSD美术`，共88个.spine工程，涵盖Q版人物、怪物、立绘、学院/训练室/虚拟训练场等场景和PV。清单及文件哈希保存Docs/artwork/desktop-spine-sources.json。玉原工程为Q版/Q版 spine 玉/yu.spine，同目录图片存在；只读导出original-project-export/yu.json成功，84骨骼、3原动作、35网格保留内部边，原工程未改动。

后续玉动画制作改用该原工程来源，之前二进制反向导出只留排查记录。新增坐下/乘坐/起身候选制作脚本已切换来源，修正轴动画键格式后原生解析可读取；未做视觉验收、未安装到游戏。后续角色/怪物/立绘精修优先查询桌面原工程，避免丢失编辑信息。狐狸目录命中的小/大狐狸是怪物工程，不能据名称替代用户要求的Q版队友。

### 2026-10-04：Q版狐狸工程整理到桌面美术库

按用户要求，新建桌面LSD美术/Q版/Q版 spine 九尾狐 队友目录，复制现有可编辑工程为fox-chibi.spine，配套fox-images、已有export、当前runtime快照及原Q图，共31个素材/工程文件，哈希逐一验证。README说明队友与怪物狐狸区别、运行0.85动画倍率/240移动速度、剧情mouthCenter/mouthAxis安装步骤，以及手工编辑后需明确同步而非旧JSON覆盖。

在新位置用Spine CLI导出成功，无缺图提示；与既有工程导出的二进制比较405204个原生顶点坐标，误差为0。桌面原有工程及游戏运行资源均未覆盖。该归档可编辑，但不作为最终狐狸美术验收结论。

### 2026-10-04：原工程上的玉乘坐候选已可编辑导出

Tools/build_yu_riding.py改用桌面原工程导出；补齐原images副本后，riding-candidate.spine及candidate-export/riding-candidate.skel官方导入导出成功。候选保留原腿/脚四个IK和肢体比例，平移双脚目标形成屈膝坐姿，裙摆使用独立骨链偏移；新增sit/stand各0.8秒及ride两秒。编辑器检测到二维与分轴平移轨道并存，已修为统一二维轨道。原动画与原运行二进制515202坐标比较仍通过（最大0.00124359）。

这仅是待审候选。独立Test/YuRidingPreview.lua已完成语法检查，待长稳结束后检查原生画面/循环/有限动作时长与恢复；尚未执行、未安装到游戏、未证明裙摆和托掌接触正确。

### 2026-10-04：第二次长稳30分钟终态与建模退出通过

实时句柄确认1791089961为PASS/complete：28轮、1810.686秒，完整示范→建模→三组试战→采用保存→返回训练室均完成，入口未再次缺失。对象1641–1642、Lua引用572、调用引用529、旧Arena弱引用1；原始终态归档training-soak-30min-native.json，趋势training-soak-final-trend.json。Lua首末增142.47KB，其中第7→8轮突增132.24KB，原因未明。终态暂去除测量行并GC后堆下降102.81KB，但这个差值也可能包含异步运行环境回收，不可全部归因测量行，不据此消除内存风险。恢复了运行句柄的测量记录，证据training-soak-record-memory.json。A15仍是部分通过，内存突增和音频叠播尚需核查。

确认长稳终态后运行TrainingBuildExit。首次在removeFromParent后立即断言closed失败，读取Node.cpp确认Cleanup通过post异步通知，修测试等待该通知，保留首份观测。1791091920通过：两位学员各1500条合成示范启动真实原生建树，清理旧世界，建立新会话，再恢复等待协程返回CLOSED；新会话可用12条样本正常建树，已采用记录不变。证据training-build-exit-native.json。此专项为真实引擎/合成样本、协程控制，非OS退出或玩家手动示范。

### 2026-10-04：玉乘坐候选首次画面未通过

YuRidingPreview原生运行有限坐下/起身各约0.8秒、完整ride两轮通过；首轮预览坐标未转换UI3D中心，修预览位置后重新截图。实际画面yu-riding-candidate.png显示候选裙摆/腰饰明显拉扭，前后腿遮挡需继续修正，故视觉验收不通过，不接入运行游戏。需要依据原网格的顶点权重修裙摆和接触，而非统一旋转裙骨。时序报告yu-riding-candidate-native.json的PASS只指有限动作/循环断言，visualAcceptancePending保持true。

### 2026-10-04：乘坐候选腰饰与裙摆分离修订

已保存首版失败图。逐图核对原工程：item18为腰饰，item21为前裙片，二者权重链不同。撤去统一旋转裙骨方案，保留腰饰原姿态；仅在新sit/ride/stand动画中对前裙片增加加权顶点形变，通过各骨骼逆矩阵转换同一世界位移，保持腰部连接。降低抬脚量，避免膝盖高过腰部和裙面过度压扁。原动画、权重、贴图和腿部IK弯曲方向保持。

原生对照画面yu-riding-panel-deform.png显示腰饰不再扭转、前裙片随坐姿展开；有限动作及两轮ride检查继续通过。编辑工程及二进制已同步导出；原动画515202坐标对比最大误差仍0.00124359。此版本仍是候选，反向、中间帧、裙摆完整轮廓、呼吸/表情及与机器人双掌接触未完整验收，未安装到游戏。

### 2026-10-04：玉与佛陀正反向托举组合预览

新增Test/YuBuddhaMount.lua，将原六臂机器人与玉乘坐候选放在同一组，两个镜像方向并排运行。利用下方双掌的真实父子变换计算承载位置，随悬浮/Guard动作调整，而非让玉独立做另一套上下摆动。初版承载点使手掌靠近腰肘，已调到裙摆下方，原生正反向Guard截图yu-buddha-mount-guard.png已查看。手掌与裙摆的接触边缘及遮挡仍需调整；坐上/落地过程、实际移动场景均未接入。yu-buddha-mount-native.json的PASS仅证明预览运行，visualAcceptancePending保留true，不替代作品验收。


## 2026-10-04 玉 Q 版风格对齐候选 v3

重新读取桌面原始 `Q版/Q版 玉.psd`、`设计/角色设计稿/新人设/玉 v3.png` 与 `玉 v3 佛陀.png`。旧版佛陀小头长脸、饱和金色和硬高光，与玉的大头和柔和浅杏金不一致。内置 image_gen 生成 `Docs/artwork/buddha-guard-chibi-v3.png`；完整提示词、来源和工具记录见 `Docs/artwork/buddha-guard/chibi-v3-generation.json`。

`Test/YuBuddhaStyle.lua` 在原生引擎同时展示旧版和新版，复用玉实际 Spine 乘坐候选及机器人 Guard 过渡。新版素材上下排分界实际为 576，因此预览使用独立取图范围；躯干比例 .65、上移 40，光环比例 .85、上移 80。BuddhaPrototype 新增可选样式参数，默认生产素材和参数不变。

原生运行 1791093559：142 帧，加载及状态切换 PASS。证据 `Docs/evidence/2026-10-04/yu-buddha-style-v3-native.json`、`yu-buddha-style-v3-guard.png`。人工看图确认配色、圆脸和光环较前版更接近玉；肩根存在缝隙，六臂尺寸与新躯干仍需适配，托掌接触、遮挡、镜像和完整乘坐生命周期未通过视觉验收。此图是候选，未替换正式场景，不代表 Game 0 美术完成。


<!-- preserved-progress-end -->
