# welcome to map documentation for krunker

krunker map format is in JSON, with the master object having properties

### TODO

a lot lol
- ENVIRONMENT:
  - weather options
  - render options
  - light intensity
  - embient intensity
  - ambient sound
  - cloud texture
- terrain (all)
- zone
  - enabled
  - speed
  - random endpoint
  - top middle bottom color
  - style
  - height
- ocean
  - enabled
  - water color
  - opacity
  - distortion
  - wave speed
  - y offset
  - reflection resolution
  - width
  - length
- scripts (when those come out)
- gui


### format

`colors` are represented as either hex strings or decimal encoded numbers
`booleans` are either 0 or 1, not true or false
`asset` these are really just numbers, but are integrated within the krunker asset marketplace
basic JSON knowledge is reccomended for this guide

### basic properties

- `name`: name of the map
- `ambient`: ambient color of the map  (affects all) 
- `sky`: color of the sky, can be solid color (#ffffff)
  - alternatively a the `skyDome` property can be set, which allows for a gradient with the following properties:
  - `skyDomeCol0`: color of the top of the sky dome
  - `skyDomeCol1`: center color
  - `skyDomeCol2`: bottom color
  - note that when `skyDome` is set that you still need to provide a `sky` color in practice
  - TODO: add cloud texture elements of sky
- `fog`: color of the fog that shows up for objects far away
- `fogD`: distance away from the player in which the fog appears
- `light`: there is a directional light that can be colored
  - on top of this, there are two properties for changing the angle at which the light points at
  - `sunAngX`: X angle of the sun
  - `sunAngY`: Y angle of the sun
  - there is no Z angle 
- `xyz`: this relates to the `objects` property, it's a multiple of 3 list that has the scales for each object, the object of `si` of 0 would use the first 3, object of `si` 1 would use the 2nd three, etc
- `spawns`: this contains a list of lists (`[[0,0,0,0,0,0]]`) which are for spawns
  - first three numbers dictate position
  - next number dictates team, 0 is default/everyone with 1,2,3,4 being to their respective teams
  - next number is direction facing, either being 0 1 2 or 3 for the 4 possible directions
  - last number dictates team only
  - there can be multiple spawns in a singular map, example: `[[3,4,5,1,2,1], [-11,40,12,0,3,0]]`
- `objects`: this contains a list of objects, majority of properties are optional, but required for certain functions, this is a list of objects, which means it takes the form of `[{}]`, each individual object can have the following properties:
  - `p` (type: `list`): this contains a 3 point list of where it's located, position
  - `si` (type: `number`): index of the element, this and `p` are the only required properties
  - `r` (type: `list`): 3 point list of rotation in RADIANS (not degrees, even if anti-radians is turned on) maximum of 2 decimals of precision normally used, default: [0,0,0]
  - `v` (type: `boolean`): this determines if it's INVISIBLE (1 being invisible) default: 0
  - `l` (type: `boolean`): this determines whether it's non collidable, 0 being collidable and 1 being not, default: 0
  - `wj` (type: `boolean`): this determines whether you cannot wall jump off of it, 0 being you can, 1 can't, default: 0
  - `gp` (type: `boolean`): this determines whether you can not grapple onto a surface, 0 being you can, default: 0
  - `bo` (type: `boolean`): this property marks the object as border, this means that if `disable border` option in game hosting is turned on, it won't collide/show, default: 0
  - `t` (type: `number`): this dictates texture of an object: the following mapping can be used: default: 0 (note that under each are the variants, see `tv` for more info)
    - 0: stone
      - 0: default
      - 1: classic
      - 2: light
    - 1: dirt
      - 0: default
      - 1: classic
    - 2: wood
      - 0: default
      - 1: classic
    - 3: grid
    - 4: grey
    - 5: default
    - 6: roof
      - 0: default
      - 1: classic
    - 7: flag
      - 0: default
      - 1: classic
      - 2: classic alt
    - 8: grass
    - 9: check
    - 10: lines
      - 0: default
      - 1: thick
    - 11: brick
      - 0: default
      - 1: classic
      - 2: classic alt
    - 12: link
    - 13: liquid
    - 14: grain
    - 15: fabric
    - 16: tile
  - `tv` (type: `number`): texture variant, for the index of each variant, see above under each texture that has them, default: 0
  - `at` (type: `asset`): texture asset to use, default: 0
  - `tsr` (type: `boolean`): whether to streth the texture, default: 0
  - `tsm` (type: `number`): scale of the texture, default: 0 (if 0, don't scale)
  - `ft` (type: `boolean`): whether to force transparency of an object, default: 0
  - `tro` (type: `number`): in radians, how much to rotate the texture, default: 0
  - `tox` (type: `number`): from 0 to 1, how much to offset the texture on the X axis, default: 0
  - `toy` (type: `number`): from 0 to 1, how much to offset the texture on the Y axis, default: 0
  - `ts` (type: `number`): texture speed along the `td` axis, default: 0
  - `td` (type: `number`): texture direction, 0 for X and 1 for Y, default: 0
  - `fct` (type: `number`): frame count of an animated texture, default: 1
  - `fs` (type: `number`): frame speed of an animated texture, default: 0


