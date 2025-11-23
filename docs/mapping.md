# Prospit Mapping Format

Follows the vanilla mapping formula of "one action per sector", but wth small bits and bobs taken from MBF21 as need be. I don't know if reserved linedefs will stay reserved. I don't plan on following id24 convention either, so id Software's reserved linedefs will not apply here.

## Linedef Specials

Lindef bit layout is as follows:

* Bit 15: "This Linedef special is actually a script" flag, with one nybble reserved for general-purpouse arguments, the rest being used to indicate which script to use, with a max of 2048 unique scripts.
* Bit 14: Reserved for exclusive implemetations (or whatver I plan to use). Doesn't do anything otherwise.
* Bit 13 - 10: General purpouse argument for linedef special.
* Bit 9 - 0: Linedef Special Action (e.g Open Door, Activate Lift)

Without Bit 15 Set: [0][0][0000][0000000000]

With Bit 15 Set: [1][0000][00000000000]

Generic Door Action will open, wait for a bit, then close.
Bit Layout for Parameter Types:

* Door Parameter: [NO_DELAY|SHORT_DELAY|DEFAULT|LONG_DELAY], [SLOW|NORMAL|FAST|TURBO] 
* Lock Type: [ANY|RED|YELLOW|BLUE], [KEEP|REMOVE|THREE|SIX] (bit combos like 0110/0111 require all three/six keys and consume them on use)
* Lift Parameter: Same as Door Parameter
* Floor Target: [NEAREST|NEXT|HIGHEST|LOWEST], [NO_CHANGE|CHANGE_TEXTURE|CHANGE_SPECIAL|CHANGE_ALL]
* 

|Number|Action|Parameter|
|-|-|-|
|1|DR Door Generic|Door Parameter|
|2|D1 Door Open|Door Parameter|
|3|DR Locked Generic|Lock Type|
|4|D1 Locked Door Open|Lock Type|
|5|SR Door Generic|Door Parameter|
|6|S1 Door Open Only|Door Parameter|
|7|S1 Locked Door Open|Lock Type|
|8|GR Door Generic|Door Parameter|
|9|G1 Door Open|Door Parameter|
|10|WR Door Generic|Door Parameter|
|11|W1 Door Open|Door Parameter|
|12|W1 Door Close|Door Parameter|
|13|W1 Door Generic|Door Parameter|
|14|W1 Locked Door Open|Lock Type|
|15|SR Lift Lower/Raise|Lift Speed|
|16|WR Lift Lower/Raise|Lift Speed|
|17|S1 Start Perpetual Lift|Lift Speed|
|18|W1 Start Perpetual Lift|Lift Speed|
|19|(S1\W1) Donut|Donut Parameter|
|20|SR Floor Lower|Floor Target|
|21|S1 Floor Lower|Floor Target|
|22|WR Floor Lower|Floor Target|
|23|W1 Floor Lower|Floor Target|
|24|SR Floor Raise|Floor Target|
|25|S1 Floor Raise|Floor Target|
|26|WR Floor Raise|Floor Target|
|27|W1 Floor Raise|Floor Target|
|28|SR Light Change|Light Parameter|
|29|S1 Light Change|Light Parameter|
|30|WR Light Change|Light Parameter|
|31|W1 Light Change|Light Parameter|
|32768 - 34815|Activate Script #1 - #2048|General-Purpose Parameter|

## Linedef Flags
Don't stray too far from vanilla for this? I'll be honest, I don't know what I plan to do with this one. I'll come up with something later.

## Linedef Scripting
Should probably borrow from Hexen ACS? Or at least try not to stray too far from general ACS convention. Making someone have to compile fifteen seperate toolchains for a Doom Map isn't what one would call epic.

More info will come on that when I find the time.


## Sector Special
Sector bit layout is as follows:

* Bits 0 - 5: Sector Special
* Bits 6 - 8: Damage Type
* Bits 9 - 11: Lighting Type
* Bits 12 - 15: General Parameter

[0000][000][000][000000]

|Damage Value|Function|
|-|-|
|0|No Damage|
|1|5% Damage|
|2|10% Damage|
|3|20% Damage|
|4|Blindness Debuff|
|5|Damage Vulnerability|
|6|Instakill w/out Radsuit|
|7|Instakill|

|Lighting Value|Function|
|-|-|
|0|Normal Lighting|
|1|Blink (Randomly)|
|2|Blink (0.5s)|
|3|Blink (0.5s sync)|
|4|Blink (1s)|
|5|Blink (1s sync)|
|6|Flicker (random)|
|7|Glow (1s)|

Damage and Lighting can be set independently of sector special.

* Exit Parameter: [SECRET_EXIT], [RESET_HEALTH], [RESET_AMMO], [RESET_WEAPONS] (Pistol Start exit would be x111)
* Scroll Parameter: [0xx: Cardinal, 1xx: Diagonal], [SCROLL_ITEMS]
* Wind Parameter: [0xx: Cardinal, 1xx: Diagonal], [VARIABLE_SPEED]

|Number|Special|Parameter|
|-|-|-|
|0|Nothing (default)||
|1|Use SKYx Texture|SKY1 - SKY16|
|2|Secret Sector|Unused?|
|3|Jump Pad|Height|
|4|Exit Level|Exit Parameter|
|5|Low Friction|Friction Factor|
|6|High Friction|Friction Factor|
|7|Reverse Controls|Delay?|
|8|Slow Scroller|Scroll Parameter|
|9|Normal Scroller|Scroll Parameter|
|10|Fast Scroller|Scroll Parameter|
|11|Slow Wind|Wind Parameter|
|12|Normal Wind|Wind Parameter|
|13|Fast Wind|Wind Parameter|
|14|Door Close after (n * 2) Seconds|Time|
|15|Door Open after (n * 2) Seconds|Time|
|16|Door Generic after n Minutes|Time|
|16|Acceleration Floor|Fast Factor|
|17|Deceleration Floor|Slow Factor|
|18|Deep Liquid|Liquid 'Depth'|
|19|Custom Fog Color|Color?|
|20|End Level when h < 11%|???|
|21|Phased Light|Sequence Step|
|22|Modify Gravity|Gravity Paramter|
|23|Healing Pool|???|
|24|||
|25|||
|26|||
|27|||
|28|||
|29|||
|30|||
|31|||
|32 - 63|User-Defined Sector Special|Parameter|

## Mapthings

* Pusher/Puller Thing: Should work like Boom
* Ambient Sound Loop(s): Should work like Heretic
* Z-Aware Platform: ROTT's GADs, pretty much!
* Invisible Bridge: GADs, but invisible.

Everything in this document is subject to change.
