#Prospit Mapping Format

Follows the vanilla mapping formula of "one action per sector", but wth small bits and bobs taken from MBF21 as need be. I don't know if reserved linedefs will stay reserved. I don't plan on following id24 convention either, so id Software's reserved linedefs will not apply here.

##Linedef Specials

Lindef bit layout is as follows:

* Bit 31: "This Linedef special is actually a script" flag, with two bytes reserved for general-purpouse arguments, the rest being used to indicate which script to use, with a max of 32K+ unique scripts.
* Bit 30: Reserved for exclusive implemetations (or whatver I plan to use). Doesn't do anything otherwise.
* Bit 29 - 22, and 21 - 14: General purpouse arguments for linedef special.
* Bit 13 - 0: Linedef Special Action (e.g Open Door, Activate Lift)

Without Bit 31 Set: [0][0][00000000][00000000][00000000000000]

With Bit 31 Set: [1][00000000][00000000][000000000000000]

##Linedef Flags
Don't stray too far from vanilla for this? I'll be honest, I don't know what I plan to do with this one. I'll come up with something later.

##Linedef Scripting
Should probably borrow from Hexen ACS? Or at least try not to stray too far from general ACS convention. Making someone have to compile fifteen seperate toolchains for a Doom Map isn't what one would call epic.

More info will come on that when I find the time.


##Sector Special
Sector bit layout is as follows:

* Byte 0: Special Sector actions (more info in table)
* Byte 1: Sector Lighting (Blink 0.5, Glow 1s)
* Bute 2: Sector Damage (-5, -10, -20, instakill)
* Byte 3: Sector Scrolling (Direction, Speed, Move Things)

[00000000][00000000][00000000][00000000]

I don't know if the other bytes will be in a dropdown, or if more fancy bit manipulation will be used.

|Number|Special                                         |
|------|------------------------------------------------|
|0     |Nothing (default)                               |
|1     |Use SKY2 Texture                                |
|2     |Use SKY3 Texture                                |
|3     |Use SKY4 Texture                                |
|4     |Secret Sector                                   |
|5     |Jump Pad (Damage Byte Controls Jump Height)     |
|6     |Exit Level (Damage Byte Controls Kept Inventory)|
|7     |Exit to Secret Level (Same mechanic as 6)       |
|8     |Custom COLORMAP (Use Upper Texture)             |
|9     |Lower Player/Monster Height (Deep Liquid)       |
|10    |Low Friction Sector (A Bit Slippery)            |
|11    |Very Low Friction Sector (VERY Slippery)        |
|12    |High Friction Sector (Marshy Mud)               |
|13    |Very High Friction Sector (Sticky Tar)          |
|14    |Reverse Controls                                |


##Mapthings

* Pusher/Puller Thing: Should work like Boom
* Ambient Sound Loop(s): Should work like Heretic
* Z-Aware Platform: ROTT's GADs, pretty much!
* Invisible Bridge: GADs, but invisible.

Everything in this document is subject to change.