# 候选包与重建

更新：2026-10-10。所有历史构建产物已按要求删除，目前无可交付候选包。

最近历史候选为`2026-10-09-full-content-head-aim-candidate`：2780文件、1165运行资源、410 Script Lua、81 UI Lua，严格签名、包内加载及定向任务回归曾通过。状态始终为`PACKAGED_NOT_ACCEPTED`；后续源码优化和降级修复未进入该包。历史状态不能作为当前安装包验收。

重建使用游戏`Tools/package_game0_macos.py`，需要重新提供匹配且验证过的运行时manifest，在工程外生成独立app。`Tools/stage_game0.py`负责完整资源暂存和哈希；不能把资源暂存目录当作安装包。

运行依赖为Data、Font、Image、Music、Script、Sound、Spine、UI；生产包不包含Docs、Test、Tools与隔离存档。保留原三章、任务、角色和既有结局；不使用减内容方式收敛。

新包须验证干净目录启动、签名、资源路径、隔离存档、原始任务胜败/撤退/重试/结算返回和连续操作。完整门槛见[验收](acceptance.md)与[全内容可玩版方案](mvp-playable-plan.md)。
