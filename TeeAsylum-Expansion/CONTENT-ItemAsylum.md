# TeeAsylum 扩展内容说明

本次扩展参考 [Item Asylum Wiki](https://itemasylum.wiki/Item_asylum) 的模式规则和装备机制，将它们适配到 DDNet 的二维移动、血量、投射物和现有网络协议。Wiki 用来核对玩法，本文件用自己的语言说明相关机制。

已集成六种模式和十二件新装备，装备总数24。下表说明参考来源与适配方向；本版实际数值和操作见配套 `README-TeeAsylum.md`。

## 游戏模式

| 模式 | Wiki 的核心规则 | DDNet 适配方向 | 来源 |
|---|---|---|---|
| FFA 自由混战 | 所有玩家各自作战，出生时取得近战、远程、特殊三个随机槽位；目标是在回合内取得更多击杀。 | 保留已有三槽随机装备、复活重抽、击杀计分，加入更多装备。 | [FFA](https://itemasylum.wiki/FFA) |
| TDM 团队死斗 | 玩家分队，队友之间不互相伤害，比较团队击杀成绩。 | 使用红蓝两队，统一结算团队得分并保护队友。 | [TDM](https://itemasylum.wiki/Tdm) |
| GG 武器升级赛 | 相同击杀进度的玩家获得相同预设装备；每次击杀推进装备阶段，最后用黄金近战完成终结。 | 使用回合预设阶段，击杀立即替换装备，最后阶段限制为近战。 | [GG](https://itemasylum.wiki/GG) |
| ELIM 淘汰赛 | 每人有限生命，失去全部生命后观战；击杀提高最大生命值，最后存活者胜。加时会进入缩小安全区。 | 采用生命次数、淘汰观战和最终存活判定；安全区以二维距离判定适配。 | [ELIM](https://itemasylum.wiki/ELIM) |
| ZS 感染生存 | 生还者与僵尸对战；生还者死亡后加入僵尸，僵尸可以继续复活。生还者坚持到计时结束获胜，全部感染则僵尸获胜。 | 使用两个阵营、死亡转换阵营、不同装备池，以及全员感染或超时结算。 | [ZS](https://itemasylum.wiki/ZS) |
| JGN 巨人讨伐 | 一名玩家成为高血量巨人，其余玩家合作讨伐；普通玩家有有限生命，巨人只有一命。 | 按参与人数调整巨人生命值，提供巨人装备，与普通玩家生命次数和观战配合。 | [JGN](https://itemasylum.wiki/JGN) |

Wiki 的 [Gamemodes](https://itemasylum.wiki/Gamemodes) 页面也列出 BOSS、MU、TC、KIT、XMAS、VIP 等模式。这些尚未加入本次扩展。

## 新装备参考

| 装备 | 类别 | 核对到的机制 | DDNet 适配方向 | 来源 |
|---|---|---|---|---|
| comically large spoon 巨大汤勺 | 近战 | 范围挥击，命中后有明显击退与倒地效果。 | 较慢的重击，用锤击反馈和较强击退表现。 | [巨大汤勺](https://itemasylum.wiki/Comically_large_spoon) |
| darkheart 黑心剑 | 近战 | 近战命中能吸血，并有冲刺与旋风能力。 | 保留吸血近战核心，能力通过现有移动与攻击反馈表现。 | [darkheart](https://itemasylum.wiki/Darkheart) |
| dying pan 平底锅 | 近战 | 下砸攻击，命中时有强烈向下击退与倒地效果。 | 使用近战判定和方向性击退区分普通球棒。 | [dying pan](https://itemasylum.wiki/Dying_pan) |
| energy sword 能量剑 | 近战 | 连续挥击的等离子剑，攻击属于电击类。 | 快速近战，使用 DDNet 的激光或锤击效果提示命中。 | [energy sword](https://itemasylum.wiki/Energy_sword) |
| america 超重狙击枪 | 远程 | 一次性高伤精准射击，强大后坐力也会把使用者推飞。原作在 BOSS 和 JGN 装备池中禁用。 | 单发重击与大后坐力，并按模式限制装备池。 | [america](https://itemasylum.wiki/America) |
| british bazooka 英式火箭筒 | 远程 | 随机发射两种效果的投射物：较低伤害带控制，或较高直接伤害。 | 随机弹型，以伤害、击退或控制区分。 | [british bazooka](https://itemasylum.wiki/British_bazooka) |
| crossbow 弩 | 远程 | 单发弩箭，装填较慢；较远距离命中具有更高伤害。 | 使用受重力影响的慢速高伤投射物。 | [crossbow](https://itemasylum.wiki/Crossbow) |
| freeze ray 冰冻射线 | 远程 | 低伤害投射物命中后短暂冻结敌人。 | 使用冻结状态、明确冷却与远程命中反馈。 | [freeze ray](https://itemasylum.wiki/Freeze_ray) |
| holy mantle 神圣斗篷 | 特殊 | 启用后抵挡一次敌人攻击，破盾后短暂无敌；随后可充能。 | 一次护盾与破盾提示，充能方式以实现为准。 | [holy mantle](https://itemasylum.wiki/Holy_mantle) |
| re-roll dice 重抽骰子 | 特殊 | 原地重新取得装备，清除旧增益和状态，但不恢复生命值。 | 在原位置重抽三槽装备，避免借重抽免费回血。 | [re-roll dice](https://itemasylum.wiki/Re-roll_dice) |
| parasol 滑翔伞 | 特殊 | 装备时减缓下落，让玩家缓慢降到地面。 | 限制竖直下降速度，适合空中移动。 | [parasol](https://itemasylum.wiki/Parasol) |
| cleave 连斩 | 特殊 | 前方区域捕获敌人后连续斩击；无目标时不消耗，成功攻击后进入冷却。 | 前方范围攻击，采用连续命中或合并伤害与控制反馈。 | [cleave](https://itemasylum.wiki/Cleave) |

## 数值与表现

原作通常采用 100 HP，当前 DDNet 基础版使用较小的生命值刻度。伤害会经过缩放与联机平衡调整，不能直接把 Wiki 数字复制到服务器。原作的三维布娃娃、爆头、肢体动画、材质、音轨和特殊界面，也需要按 DDNet 客户端的能力转化为击退、冻结、激光、投射物、声音和文字提示。

这份扩展以游戏规则与装备功能为内容来源，使用服务器现有资源完成视觉适配。具体差异：darkheart保留吸血近战；cleave合并为前方一次斩击；bazooka改为两种爆炸伤害；parasol增加主动上升；America伤害按DDNet缩放，JGN随机池禁用；holy mantle用20秒冷却抵挡一次攻击；GG最终黄金勺沿用汤勺外观。原作的Roblox模型、音轨或动画资产未导入。
