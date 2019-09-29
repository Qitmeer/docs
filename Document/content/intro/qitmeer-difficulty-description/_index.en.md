---
title: Qitmeer mining difficulty adjustment
weight: 1
#pre: "<b>1. </b>"
# chapter: false
---

#### Base step of difficulty adjustment

- Pick a window of N latest blocks.
- Pick a reference target or difficulty. It can be the one for the last block (all DigiShields) or the average over the last N blocks (*GravityWave, Zcash).
- Take the elapsed time between the last block and the block that's N blocks before. The block time can be taken as-is (*GravityWave), or as a median of the X previous blocks to prevent time warp attacks (Zcash, Digishield).
- Potentially apply some dampening factor (Zcash, Digishield).
- Calculate the new target as the reference target, time the calculated elapsed time, divided by the ideal elapsed time.
- Bound by how much the new target can change compared to the previous (16% down, 8% up for Digishield, 32% down, 16% up for Zcash and 1/2 and x2 for AntiGravityWave)
- Return the min target if the obtained target is higher.

#### Qitmeer difficulty adjustment process (testnet param)

- How many blocks are selected from the current block forward as a unit of calculation A = 144
- Choose how many units to weigh to get the average B = 20
- Block target limit time T = 120 (seconds)
- Three basic initial difficulty Diff1 = 0x1e00ffff, Diff2 = 1000, Diff3 = 1000
- ACTUAL_TIME= (last block out time (or theoretical next block out time) - the first block out time in a unit
- Target block time fixed value TARGET_TIME = T * A = 144 * 120 for each unit (144 blocks)
- Adjustment = ACTUAL_TIME / TARGET_TIME, a unit of difficulty adjustment index, enlarges 2 ^ 32 times for accurate calculation. Adjustment = ACTUAL_TIME / TARGET_TIME* 2 ^ 32
- All 20 units can be calculated as Adjustment 1, Adjustment 2... Adjustment 20
- According to the principle that the latest block time can best improve the computing power of the whole network, 20 blocks are weighted averaged and the average difficulty adjustment index is obtained.
- AVERAGE (Adjustment) = (Adjustment 1 * 2 ^ 20 + Adjustment 1 * 2 ^ 19 +... Adjustment 1 * 2 ^ 1) /(2 ^ 20 + 2 ^ 19 +... 2 ^ 1)
- The difficulty of the last block is the reference object oldDiff, the initial difficulty oldDiff = the basic initial difficulty
- The current difficulty value should be curDiff = oldDiff * AVERGE (Adjustment) / 2^ 32
- If the current difficulty value curDiff < oldDiff/4, curDiff = oldDiff/4
- If the current difficulty value curDiff > oldDiff * 4, curDiff = oldDiff * 4