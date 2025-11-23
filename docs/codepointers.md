# Derse Codepointer Suite
All vanilla codepointers, and most of what BEX does is supported. DEHExtra, or at least some form of it, is also supported, so you don't need to worry about having to knife exiting monsters/decorations/weapons just to make your stuff work. All MBF21 codepointers and below should be supported too, but some of them might have different parameters.

## Monster-Related Codepointers

|Codepointer Name        |Basic Description                                                                        |Parameters (if specified)                                  |
|------------------------|-----------------------------------------------------------------------------------------|-----------------------------------------------------------|
|A_MonsterProjectile     |Makes an enemy fire a projectile (should work like MBF21)                                |Same as the MBF21 Codepointer                              |
|A_MonsterProjectileMulti|Same as the previous codepointer, but lets them fire multiple projectiles in one pointer.|Same as above, uint projectiles, angle spread, angle offset|
|A_RunScriptAndDie       |                                                                                         |                                                           |
|                        |                                                                                         |                                                           |
|                        |                                                                                         |                                                           |
|                        |                                                                                         |                                                           |
|                        |                                                                                         |                                                           |
|                        |                                                                                         |                                                           |
|                        |                                                                                         |                                                           |
|                        |                                                                                         |                                                           |


## Weapon-Related Codepointers

|Codepointer Name  |Basic Description|Parameters (if specified)|
|------------------|-----------------|-------------------------|
|A_WeaponHitscan   |                 |                         |
|A_WeaponProjectile|                 |                         |
|A_ProjectileShield|                 |                         |
|                  |                 |                         |
|                  |                 |                         |
|                  |                 |                         |
|                  |                 |                         |
|                  |                 |                         |
|                  |                 |                         |
|                  |                 |                         |

## Jump and JumpIf States

|Codepointer Name    |Basic Description|Parameters (if specified)|
|--------------------|-----------------|-------------------------|
|A_JumpChance()      |                 |                         |
|A_JumpIfDifficulty()|                 |                         |
|A_JumpIfDistance    |                 |                         |
|A_JumpIfHeathRange  |                 |                         |
|A_JumpIfHealthAbove |                 |                         |
|A_JumpIfAfterMap    |                 |                         |
|A_JumpIfBeforeMap   |                 |                         |
|A_JumpIfMap         |                 |                         |
|A_JumpIfMapVar      |                 |                         |
|                    |                 |                         |

## Other States

|Codepointer Name|Basic Description                         |Parameters (if specified)|
|----------------|------------------------------------------|-------------------------|
|A_Accelerate    |Adds or multiplies a projectile's speed.  |bool mode, float factor  |
|A_Decelerate    |Subtracts or divides a projectile's speed.|bool mode, float factor  |
|                |                                          |                         |
|                |                                          |                         |
|                |                                          |                         |
|                |                                          |                         |
|                |                                          |                         |
|                |                                          |                         |
|                |                                          |                         |
|                |                                          |                         |


## Attributes and Other Crap
* __uint projectileDice__: Modified the damage multiplier projectiles use.
* __uint damageOffset__: After damage calculations, adds *n* points of damage.
* __uint {respawnTime|respawnLives}__: Controls respawn mechanics on Nightmare (or custom difficulty), should be similar to id24.
* __float damageFactor__: If above one, entity takes extra damage, if below one, entity takes reduced damage.

Everything in this document may be subject to change.