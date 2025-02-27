## 🎈 Entity Object API

In LLSE, "entity objects" are used to manipulate and obtain information about an entity.

### In LLSE, “Entity Objects” Are Used to Manipulate and Obtain Information About an Entity. 

#### Get From Event or API

Obtain the entity object given by BDS by registering the **event listener** function, or calling some **returning entity object** functions.
For details, see [Event listener documentation - EventAPI](/LLSEPluginDevelopment/EventAPI/Listen.md)      

#### Get All Currently Loaded Entities

This function returns an array of entity objects, each of which corresponds to a loaded entity.

`mc.getAllEntities()`

- Return value: List of entity objects
- Return value type:  `Array<Entity,Entity,...>`

#### Spawn New Creature and Get Its Entity Object

Through this function, generate a new creature at the specified location and get its corresponding entity object.

`mc.spawnMob(name,pos)`  
`mc.spawnMob(name,x,y,z,dimid)`

- Parameters: 
  - name : `String`  
    The namespace name of the creature, such as `minectaft:creeper`
  - pos : `IntPos `/ `FloatPos`  
    A coordinate object of where the mob is spawned (or use x, y, z, dimid to determine where to spawn).
- Return value: The generated entity object.
- Return value type:  `Entity`
  - If the return value is `Null` it means that the generation failed 

> Note: Do not save an entity object **long-term**.
> When the entity corresponding to the entity object is destroyed, the corresponding entity object will become invalid. Therefore, if there is a need to operate an entity for a long time, please obtain the real-time entity object through the above methods.

<br>

#### Clone A Creature and Get Its Entity Object

Through this function, generate a new creature at the specified location and get its corresponding entity object.

`mc.cloneMob(entity,pos)`  
`mc.cloneMob(entity,x,y,z,dimid)`

- Parameters: 
  - entity : `Entity`  
    Need clone entity object
  - pos : `IntPos `/ `FloatPos`  
    A coordinate object of where the mob is spawned (or use x, y, z, dimid to determine where to spawn).
- Return value: The clone entity object.
- Return value type:  `Entity`
  - If the return value is `Null` it means that the generation failed 

> Note: Do not save an entity object **long-term**.
> When the entity corresponding to the entity object is destroyed, the corresponding entity object will become invalid. Therefore, if there is a need to operate an entity for a long time, please obtain the real-time entity object through the above methods.

<br>

### Entity Object - Properties

Every entity object contains some fixed object properties. for a specific entity object `en`, has the following properties:

| Attributes               | Meaning                                                | Data Type        |
| ------------------------ | ------------------------------------------------------ | ---------------- |
| en.name                  | Entity name                                            | `String`         |
| en.type                  | Entity type name                                       | `String`         |
| en.id                    | Entity's in-game ID                                    | `Integer`        |
| en.pos                   | Entity's coordinates                                   | `FloatPos`       |
| en.blockPos              | The coordinates of the block the entity is standing on | `IntPos`         |
| en.maxHealth             | Entity's maximum health                                | `Integer`        |
| en.health                | Entity's current health                                | `Integer`        |
| en.canFly                | Can the entity fly                                     | `Boolean`        |
| en.canFreeze             | Can entity be frozen                                   | `Boolean`        |
| en.canSeeDaylight        | Can entitiy see daylight                               | `Boolean`        |
| en.canPickupItems        | Can entitiy pick up items                              | `Boolean`        |
| en.inAir                 | Whether the entity is in the air                       | `Boolean`        |
| en.inWater               | Whether the entity is in the water                     | `Boolean`        |
| en.inLava                | Whether the entity is in the lava                      | `Boolean`        |
| en.inRain                | Whether the entity is in rain                          | `Boolean`        |
| en.inSnow                | Whether the entity is in snow                          | `Boolean`        |
| en.inWall                | Whether the entity is on the wall                      | `Boolean`        |
| en.inWaterOrRain         | Whether the entity is in water or rain                 | `Boolean`        |
| en.inWorld               | Whether the entity is in the world                     | `Boolean`        |
| en.speed                 | Entity's current speed                                 | `Float`          |
| en.direction             | Entity's orientation                                   | `DirectionAngle` |
| en.uniqueId              | Entity's unique identifier                             | `String`         |
| en.isInvisible           | Whether the entity is invisible                        | `Boolean`        |
| en.isInsidePortal        | Whether the entity is inside the portal                | `Boolean`        |
| en.isTrusting            | Whether the entity is trusted                          | `Boolean`        |
| en.isTouchingDamageBlock | Whether the entity touches the damage block            | `Boolean`        |
| en.isOnFire              | Whether the entity is on fire                          | `Boolean`        |
| en.isOnGround            | Whether the entity is on the ground                    | `Boolean`        |
| en.isOnHotBlock          | Whether the entity is on a hot block (magma and etc.)  | `Boolean`        |
| en.isTrading             | Whether the entity is trading                          | `Boolean`        |
| en.isRiding              | Whether the entity is riding                           | `Boolean`        |
| en.isDancing             | Whether the entity is dancing                          | `Boolean`        |
| en.isSleeping            | Whether the entity is sleeping                         | `Boolean`        |
| en.isAngry               | Whether the entity is angry                            | `Boolean`        |

These object properties are read-only and cannot be modified.

For a detailed explanation of the **entity's current orientation** attribute, see the [Basic Game Interface Documentation](/LLSEPluginDevelopment/GameAPI/Basic.md)

<br>

### Entity Object - Function

Each entity object contains some member functions (member methods) that can be executed. for a specific entity object `en`, you can perform some operations on this entity through the following functions:

#### Teleport Entity to Specified Location

`en.teleport(pos)`  
`en.teleport(x,y,z,dimid)`

- Parameters: 
  - pos :`IntPos `/ `FloatPos`  
    Target position coordinates (or use x, y, z, dimid to determine entity position)
- Return value: Whether the teleport was successful or not.
- Return value type:  `Boolean`

<br>

#### Kill the Specified Entity  

`en.kill()`

- Return value: Whether the entity execution was successful.
- Return value type:  `Boolean`

<br>

#### Inflict Damage to Entities

`en.hurt(damage,type)`

- Parameters: 
  - damage : `Float`  
    The amount of damage to deal to the entity.
 - type : `Integer`  
    Actor Damage Cause
- Return value: Whether the damage was dealt.
- Return value type:  `Boolean`

Note that the damage dealt here is real damage and cannot be reduced by protective equipment such as armor.

| ActorDamageCause ENUM    |
| ------------------------ |
| `ActorDamageCause.Override`|
| `ActorDamageCause.Contact `   |
| `ActorDamageCause.EntityAttack` |
| `ActorDamageCause.Projectile`     |
| `ActorDamageCause.Suffocation`    |
| `ActorDamageCause.All`     |
| `ActorDamageCause.Fire`  |
| `ActorDamageCause.FireTick`    |
| `ActorDamageCause.Lava`      |
| `ActorDamageCause.Drowning `  |
| `ActorDamageCause.BlockExplosion`   |
| `ActorDamageCause.EntityExplosion`    |
| `ActorDamageCause.Void`  |
| `ActorDamageCause.Suicide`    |
| `ActorDamageCause.Magic`     |
| `ActorDamageCause.Wither`     |
| `ActorDamageCause.Starve`   |
| `ActorDamageCause.Anvil`    |
| `ActorDamageCause.Thorns`  |
| `ActorDamageCause.FallingBlock`    |
| `ActorDamageCause.Piston`     |
| `ActorDamageCause.FlyIntoWall`     |
| `ActorDamageCause.Magma`    |
| `ActorDamageCause.Fireworks`  |
| `ActorDamageCause.Lightning`    |
| `ActorDamageCause.Charging`     |
| `ActorDamageCause.Temperature`     |
| `ActorDamageCause.Freezing`  |
| `ActorDamageCause.Stalactite`    |
| `ActorDamageCause.Stalagmite`     |

<br>

#### Set the Specified Entity on Fire

`en.setOnFire(time)`

- Parameters: 
  - time : `Integer`  
    Fire time, in seconds.
- Return value: Whether the fire was set.
- Return value type:  `Boolean`

<br>

#### Determine if an Entity Object Is a Player

`en.isPlayer()`

- Return value: Whether the current entity object is a player.
- Return value type:  `Boolean`

<br>

#### Convert Entity Object to Player Object

`en.toPlayer()`

- Return value: The converted `Player` object.
- Return value type:  `Player`
  - Returns `Null` if this entity object does not point to a player, or if the transition fails.

If the current entity object points to a player, you can use this function to convert the entity object to a player object to use more player-related APIs.

<br>

#### Determine Whether an Entity Object Is a Dropped Item Entity

`en.isItemEntity()`

- Return value: Whether the current entity object is a dropped item entity.
- Return value type:  `Boolean`

<br>

#### Get the Item Object in the Drop Entity

`en.toItem()`

- Return value: The obtained `Item` object.
- Return value type:  `Item`
  - If this entity object is not a drop entity, or if the acquisition fails, return `Null`

If the current entity object is a drop entity, you can use this function to get the item object in the drop entity to use more item-related APIs.

<br>

#### Get the Block the Entity Is Currently Standing On

`en.getBlockStandingOn()`

- Return value: The block object the entity is standing on.
- Return value type:  `Block`

<br>

#### Gets the Container Object for the Mob’s Armor Slot  

`en.getArmor()`

- Return value: The container object corresponding to the armor bar of this entity.
- Return value type:  `Container`

For more usage of container objects, please refer to [Container Object API Documentation](/LLSEPluginDevelopment/GameAPI/Container.md)

<br>

#### Determines if a Mob Has a Container (Except for the Armor Slot)

`en.hasContainer()`

- Return value: Whether this biological entity has a container.
- Return value type:  `Boolean`

Such as the boxes on the alpaca, they each have their own container object.

<br>

#### Get the Container Object Owned by the Mob (Except the Armor Slot)

`en.getContainer()`

- Return value: The container object owned by this biological entity.
- Return value type:  `Container`

For more usage of container objects, please refer to [Container Object API Documentation](/LLSEPluginDevelopment/GameAPI/Container.md)

<br>

#### Refresh Creature Inventory, Armor Slot

`en.refreshItems()`

- Return value: Whether the refresh was successful.
- Return value type:  `Boolean`

After modifying the creature's items, in order to make the client take effect, it is necessary to refresh all the items of the creature.

<br>

#### Add a Tag to the Entity

`en.addTag(tag)`

- Parameters: 
  - tag: `String`  
    The tag string to be added.
- Return value: Whether the `Tag` was added successfully.
- Return value type:  `Boolean`

<br>

#### Remove a Tag From an Entity

`en.removeTag(tag)`

- Parameters: 
  - tag: `String`  
    The tag string to remove.
- Return value: Whether the tag removal was successful.
- Return value type:  `Boolean`

<br>

#### Check if an Entity Has a Tag

`en.hasTag(tag)`

- Parameters: 
  - tag: `String`  
    Tag string to check 
- Return value: Whether the entity has the tag.
- Return value type:  `Boolean`

<br>

#### Returns a List of All Tags Owned by the Entity

`en.getAllTags()`

- Return value: A list of all tag strings of the entity
- Return value type:  `Array<String,String,...>`

<br>

#### Get the Entity's NBT Object

`en.getNbt()`

- Return value: NBT object of the entity.
- Return value type:  `NbtCompound`

<br>

#### Write to the Entity's NBT Object

`en.setNbt(nbt)`

- Parameters: 
  - nbt : `NbtCompound`  
    NBT objects
- Return value: Whether the write was successful or not.
- Return value type:  `Boolean`

For more usage of NBT objects, please refer to [NBT Interface Documentation](/LLSEPluginDevelopment/NbtAPI/NBT.md)

<br>

### Other Entity Function API

The following APIs provide APIs for interacting with entities at specified locations in the game:

#### Create an Explosion at the Specified Location

`mc.explode(pos,source,power,range,isDestroy,isFire)`  
`mc.explode(x,y,z,dimid,source,power,range,isDestroy,isFire)`

- Parameters: 
  - pos : `IntPos `/ `FloatPos`  
    The coordinates of the location where the explosion occurred (or use x, y, z, dimid to determine entity location).
  - source : `Entity`  
    Set the entity object of the explosion source, which can be `Null`.
  - power : `Float`  
    The power value of the explosion, which affects the damage and damage range of the explosion.
  - range : `Float`  
    The radius of the explosion, which affects the scope of the explosion.
  - isDestroy : `Boolean`  
    Does the explosion destroy blocks.
  - isFire : `Boolean`  
    Whether there is a burning flame left after the explosion.
- Return value: Whether the explosion was successfully created.
- Return value type:  `Boolean`

<br>


#### Quick execute Molang expression

`en.quickEvalMolangScript(str)`

- Parameters:
  - str : `String`  
    Molang expression string.
- Return value: The result of the Molang expression.
- Return value type:  `Float`

For detailed usage of Molang, refer to [MOLANG Doc bedrock.dev](https://bedrock.dev/zh/docs/stable/Molang)
<br>