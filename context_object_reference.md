# Wiki conversion notes
1. A few items need some researching
2. The location of the function table is not final, as such as the "about the document" section does not yet mention it.
3. Each section needs function tables created 
4. Each function reference needs a link
5. Each function needs it's own text without the "see below" type of reference from the ebook version since this is more of a reference guide approach
6. Enum references should be links (obviously the enum documentation needs to be done for that).
7. Each function or set of functions needs real world code examples, these will be taken from "additional_scenes/official_content" if nothing is available; I'll write something.


----
# Outline

Newlife is written in [Java](https://en.wikipedia.org/wiki/Java_(programming_language)) and uses [Velocity](https://velocity.apache.org) for scripting purposes.  [YAML](https://en.wikipedia.org/wiki/YAML) is used to describe Velocity scene files to the game engine.

This document assumes a general knowledge of programming, particularly with languages that used [typed](https://en.wikipedia.org/wiki/Data_type) variables.

| Extension | Format | Usage |
| :-------- | :----- | :--- |
| `yml` | YAML | Scene Description |
| `vm` | Velocity | Scene Content |  

This is a list of all methods available in the various context objects accessible in custom scenes through Velocity.

A method signature is `methodName(Parameters): returnType`. 
To call a method use `$objectname.methodname(parameters)`. See the [Velocity User Guide](https://velocity.apache.org/engine/1.7/user-guide.html) for more information or see the example scene. It's also possible to call getter methods in a shortened way by using e.g. `$w.eyeColour` instead of `$w.getEyeColour()`. See the [Velocity documentation](https://velocity.apache.org/engine/1.7/) for information on this.

**IMPORTANT:** Since the author of Newlife is based in the UK, methods and properites are usually spelled using British English.

## Types

Types used in parameters or return type are:

| Type | Description | Notes |
| :--- | :---------- | :---- |
| Object | This is an object type as defined here (e.g ClothingItem). | Sometimes abbreviated as "obj". Further methods can be called on this e.g. `$w.getLegwear().getBasicDesc()` |
| String | A text string. | Sometimes abbreviated as "str". These include both Strings intended for direct insertion into output and enumerated values.  |
| Enum | An enumerated string. | These are technically strings but valid values are from a set range.  They are usually all uppercase.  They are defined in the enum reference documentation that are intended to be tested in conditional statements. If a method takes an enum value as a parameter then it will error if provided a String that isn't a valid type for that enum. |
| Boolean |  A true/false value. | Sometimes abbreviated as "bool". |
| Void | Null | **Only in return types.** This means the method returns nothing. Typically the case for methods that change the game's state. |
| Integer | An integer (whole-number) numeric value. | Often abbreviated as "int". Newlife custom scenes do not use any floating-point numbers: only integers. |

Velocity also uses the above types and also uses lists (single dimension arrays) and maps (hashed arays).

## Contexts and Objects

| Context | Description | Notes |
| :------ | :---------- | :---- |
| `$scene` | Scene context | |
| `$gd` | Global game data context | |
| `$w` | Player character or "PC" | Sometimes referred to as a "MC" (main character). |
| `$npc` | Non-player character or "NPC" | |

**NOTES:**
- The PC is *always* female.  Depending on game options, the PC is either a transformed female or a "born female".

## Notes
- Some methods exist for both the PC and NPCs, they will *usually* work the same, however, there are exceptions to this.  

## Document Organization

This document is divided into sections:

1. Object Type
2. Actions, text getters and condition methods based on how the methods are to be used. 
3. Where an object has many methods in a category they might be divided by sub-categories where certain methods should be grouped logically, for instance relationship value modifiers.

### Actions

Actions are methods that make changes or initiate an activity. 

### Text Getters 

Text getters retrieve text that's suitable to be inserted directly into output. 

### Condition methods

Condition methods retrieve booleans, enum string values, other objects or generally any output that shouldn't be shown directly to the player but is intended to be checked in if statements.


----
# Functions

## Arousal

| Function | Type | Scope | Mechanic/Item | Change | Parameters | Returns |
| :------- | :--- | :---- | :------------ | :----- | :---- | :---- |
| [addArousalTiny](#addarousaltiny-void) | Modify | PC/NPC | Arousal | Very small Increase (1) | None  | Void |
| [addArousalSmall](#addarousalsmall-void) | Modify | PC/NPC | Arousal | Small increase (2) | None  | Void |
| [addArousalMedium](#addarousalmedium-void) | Modify | PC/NPC | Arousal | Moderate increase (4) | None  | Void |
| [addArousalLarge](#addarousallarge-void) | Modify | PC/NPC | Arousal | Large increase (6) | None  | Void |
| [addArousalHuge](#addarousalhuge-void) | Modify | PC/NPC | Arousal | Very large increase (10) | None  | Void |
| [isArousalComfort](#isarousalcomfort-void) | Condition | PC/NPC | Arousal | Is arousal at or above the "comfort" threshold? | None  | Boolean |
| [isArousalEnjoy](#isarousalenjoy-void) | Condition | PC/NPC | Arousal | Is arousal at or above the "enjoy" threshold? | None  | Boolean |
| [isArousalClose](#isarousalclose-void) | Condition | PC/NPC | Arousal | Is arousal at or above the "close" threshold? | None  | Boolean |
| [isArousalOrgasm](#isarousalorgasm-void) | Condition | PC/NPC | Arousal | Is arousal at or above the "orgasm" threshold? | None  | Boolean |
| [reduceArousalTiny](#reducearousaltiny-void) | Modify | PC/NPC | Arousal | Very small decrease (1) | None  | Void |
| [reduceArousalSmall](#reducearousalsmall-void) | Modify | PC/NPC | Arousal | Small decrease (2) | None  | Void |
| [reduceArousalMedium](#reducearousalmedium-void) | Modify | PC/NPC | Arousal | Moderate decrease (4) | None  | Void |
| [reduceArousalLarge](#reducearousallarge-void) | Modify | PC/NPC | Arousal | Large decrease (6) | None  | Void |
| [reduceArousalHuge](#reducearousalhuge-void) | Modify | PC/NPC | Arousal | Very large decrease (10) | None  | Void |
| [setArousalDiscomfort](#setarousaldiscomfort-void) | Modify | PC/NPC | Arousal | Sets arousal level to lowest "discomfort" level | None  | Void |
| [setArousalComfort](#setarousalcomfort-void) | Modify | PC/NPC | Arousal | Sets arousal level to the "comfort" threshold | None  | Void |
| [setArousalEnjoy](#setarousalenjoy-void) | Modify | PC/NPC | Arousal | Sets arousal level to the "enjoy" threshold | None  | Void |
| [setArousalClose](#setarousalclose-void) | Modify |  PC/NPC | Arousal | Sets arousal level to the "close" threshold | None  | Void |
| [setArousalOrgasm](#setarousalorgasm-void) | Modify | PC/NPC | Arousal | Sets arousal level to the "orgasm" threshold | None  | Void |

## Alcohol

| Function | Type | Scope | Mechanic/Item | Change | Parameters | Returns |
| :------- | :--- | :---- | :------------ | :----- | :---- | :---- |
| [addAlcoholSmall](#addalcoholsmall-void) | Modify | PC/NPC | Alcohol | Small increase | None  | Void |
| [addAlcoholMedium](#addalcoholmedium-void) | Modify | PC/NPC | Alcohol | Moderate increase | None  | Void |
| [addAlcoholLarge](#addalcohollarge-void) | Modify | PC/NPC | Alcohol | Significant increase | None  | Void |
| [clearAlcohol](#clearalcohol-void) | Modify | PC/NPC | Alcohol | Sets alcohol level to zero | None  | Void |
| [reduceAlcoholSmall](#reducealcoholsmall-void) | Modify | PC/NPC | Alcohol | Small decrease | None  | Void |
| [reduceAlcoholMedium](#reducealcoholmedium-void) | Modify | PC/NPC | Alcohol | Moderate decrease | None  | Void |
| [reduceAlcoholLarge](#reducealcohollarge-void) | Modify | PC/NPC | Alcohol | Significant decrease | None  | Void |

----
#  Character

Character methods are available on all character objects: player, maleNPCs and femaleNPCs.

## Actions

### Arousal modifiers

Arousal is internally tracked as a numeric value but for writing purposes you'll want to check if it's within certain ranges: see the *Arousal getters* for more information.
Arousal strongly affects *willpower* tests. It's relevant in some text as well: actions will often need to check arousal levels or have alternative descriptions for different levels, and descriptions of characters will often need to vary based on this.

**TIPS:**
- The game does not automatically handle orgasms. If your scene has them then you'll need to implement checks against arousal levels and orgasm handling yourself. I'll probably add further methods to make this easier in the future such as access to the default logic for the various orgasm actions.
- If you want to cap the arousal increase then you can wrap it in an if statement and only apply the change if arousal is below the desired level. This can be useful in makeouts for things that are a turn-on but not enough to make a character orgasm such as kissing.
- Scenes that start a scene-chain with just one male NPC should usually set him as active in the intro. This won't apply to sub-scenes though, as the arousal increase will usually have applied in the parent scene.

**NOTES**
- Starting arousal is based on a character's attraction to another person. NPCs always get this calculated vs the Player-character. The player-character's arousal will vary based on the active male NPC's attractiveness to her. Use the relevant scene method to change the active male NPC and update this value.
- Arousal will be passed down to any sub-scenes, so increases can allow a makeout to be started with one or both characters quite turned on. Be careful about how high you increase it though. If you increase arousal above the orgasm level in a scene which doesn't handle orgasms then the character will climax immediately on transfer to a sub-scene which does.
- The game currently has male NPCs being erect at all arousal levels, but this may change in the future.
- Arousal can go negative. There isn't a separate category for that, but it can make it hard for the character to get up to decent values again.

**Examples:**
- `$w.addArousalHuge()`
- `$npc.addArousalLarge()`
- `$w.setArousalDiscomfort()`
- `$npc.reduceArousalLarge()`

**Code Examples:**

```Velocity
#if(!$f.arousalEnjoy)
  $f.addArousalSmall()##
#end
#if(!$m.arousalEnjoy)
  $m.addArousalSmall()##
#end
```

```Velocity 
#if($scene.percent($fChance))
  $f.addArousalLarge()
#elseif($scene.percent($fChance))
  $f.addArousalMedium()
#else
  $f.addArousalSmall()
#end
```




#### addArousalHuge(): void

Provides a very large increase to arousal.

**NOTES:**
- The actual amount is *10*.
- Opposite of [reduceArousalHuge](#reducearousalhuge-void).
- Use this only if something is supposed to be exceptionally arousing or if your scene wants to summarise an extended makeout in one action.

#### addArousalLarge(): void

Provides a significant increase to arousal.

**NOTES:**
- The actual amount is *6*.
- Opposite of [reduceArousalLarge](#reducearousallarge-void).
- Appropriate only for things that are major turn-ons for the character.

#### addArousalMedium(): void

Provides a moderate increase to arousal. 

**NOTES:**
- The actual amount is *4*.
- Opposite of [reduceArousalMedium](#reducearousalmedium-void).
- Use this for very sexual actions that the character enjoys

#### addArousalSmall(): void

Provides a small increase to the character's arousal level.

**NOTES:**
- The actual amount is *2*.
- Opposite of [reduceArousalSmall](#reducearousalsmall-void).
- Use this for actions that are sexual but not massively so, such as light groping and so on.
- You can also use it instead of Medium for sexual actions that the character doesn't especially enjoy, although if s/he *really* isn't into them then you can reduce arousal instead.

#### addArousalTiny(): void

Provides a very small increase to the character's arousal level.

**NOTES:**
- The actual amount is *1*.
- Opposite of [reduceArousalTiny](#reducearousaltiny-void).
- Use this when something turns them on but not to a great extent, or as an additional bonus for having a relevant preference trait.

**Example:**
- A character with the `OVERACTIVE_IMAGINATION` trait could get a tiny or small arousal boost when her partner says something sexual in addition to a small boost that applies to all characters.

#### reduceArousalHuge(): void

Provides a very large decrease to arousal.

**NOTES:**
- The actual amount is *10*.
- Opposite of [addArousalHuge](#addarousalhuge-void).
- Use for situations that "kill the mood".

#### reduceArousalLarge(): void

Provides a significant decrease to arousal.

**NOTES:**
- The actual amount is *6*.
- Opposite of [addArousalLarge](#addarousallarge-void).
- Use for when a character does something significantly against their partner's preference trait.

**Example:** The PC putting a condom on a man who hates them.

#### reduceArousalMedium(): void

Provides a moderate decrease to arousal. 

**NOTES:**
- The actual amount is *4*.
- Opposite of [addArousalMedium](#addarousalmedium-void).
- Use when a character does something against their partner's preference trait.

#### reduceArousalSmall(): void

Provides a small increase to the character's decrease level.

**NOTES:**
- The actual amount is *2*.
- Opposite of [addArousalSmall](#addarousalsmall-void).
- Provides a minor reduction, suitable for when a character does something that directly opposes their partner's preference trait but not in an especially important way.

**Example:** The PC talks about how she loves oral when her partner doesn't like it.

#### reduceArousalTiny(): void

Provides a very small increase to the character's decrease level.

**NOTES:**
- The actual amount is *1*.
- Opposite of [addArousalTiny](#addarousaltiny-void).
- Use for especially minor arousal-reducing actions.

#### setArousalDiscomfort(): void

Sets the character's arousal level to the lowest, "discomfort" level, regardless of what it was before.

#### setArousalComfort(): void

Sets the character's arousal level to the "comfort" threshold, regardless of what it was before.

#### setArousalEnjoy(): void

Sets the character's arousal level to the "enjoy" threshold, regardless of what it was before.

#### setArousalClose(): void

Sets the character's arousal level to the "close" threshold, regardless of what it was before.

#### setArousalOrgasm(): void

Sets the character's arousal level to the "orgasm" threshold, regardless of what it was before.

### Alcohol modifiers

Alcohol has a number of game effects, such as modifying *willpower* checks and a 'beer goggles' effect that adds to the attractiveness of all other characters. Your writing will sometimes need to consider drunkenness levels too.

Call the methods to increase alcohol when a character drinks booze. 

**NOTES:**
- Where the PC is concerned you should check if she's known-pregnant first and block drinking. 
- Alcohol for female NPCs should be checked as well if they might be pregnant.
- It's rare you'll need to *reduce* alcohol. You could use this if they scene involves spending enough time without drinking for them to 'dry out'.
- Use `clearAlcohol` for scenes that involve sleeping overnight or similar.


#### addAlcoholLarge(): void

Provides a significant increase to the character's alcohol level, equivalent to a strong drink.

**NOTES:**
- Opposite of [reduceAlcoholLarge](#reducealcohollarge-void).

#### addAlcoholMedium(): void

Provides a moderate increase to the character's alcohol level.

**NOTES:**
- Opposite of [reduceAlcoholMedium](#reducealcoholmedium-void).

#### addAlcoholSmall(): void

Provides a small increase to the character's alcohol level, equivalent to a weak drink.

**NOTES:**
- Opposite of [reduceAlcoholSmall](#reducealcoholsmall-void).

#### reduceAlcoholLarge(): void

Reduces the character's alcohol level by a significant amount.

**NOTES:**
- Opposite of [addAlcoholLarge](#addalcohollarge-void).

#### reduceAlcoholMedium(): void

Reduces the character's alcohol level by a moderate amount.

**NOTES:**
- Opposite of [addAlcoholMedium](#addalcoholmedium-void).

#### reduceAlcoholSmall(): void

Reduces the character's alcohol level by a small amount.

**NOTES:**
- Opposite of [addAlcoholSmall](#addalcoholsmall-void).

#### clearAlcohol(): void

Sets the character's alcohol level to zero.

### Persistent Character Flags

These methods allow you to set string or integer flags for any character. 
These are stored internally as key-value pairs where the keys are strings and the values are either strings or integers. 

**NOTES:**
- Each character has separate maps of these values. 
- Use the player object `$w` for flags not related to any particular character.
- These flags are persistent and will be stored for the whole game unless removed. 

**DEVELOPER NOTES:**
- If you're writing content that you intend to submit for the game then you needn't use these, use the test values for GameFlags instead and I'll set up the correct values when I integrate the scene into the game.
- Some writers have found this very limiting when writing scenes that they don't intend to have integrated into the game. These methods were added to provide a way for them to store data across scenes.
- The main Newlife scenes do not use this functionality which means there's no chance of conflict with central game content.

#### addFlag(String key, String value): void

Adds the specified key-value pairing to the map for this character, overriding any existing values for the key.

**Code Example:**

```Velocity
#if($scene.percent(75))##
	She agrees to that.
	$scene.addFlag("SOPHISTICATED_SALES_NO_SEX")##
#else
	But she tells you she can't make any promises.
#end
```

#### getFlag(String key): String

Returns the value associated with this key, or `null` if no such key exists in the character's map.

#### setFlag(String key): void

Equivalent to calling `addFlag(key,"true")`. 

**NOTES:**
- This is intended as a quicker method for writers using flags as simple yes/no checks.

#### removeFlag(String key): void

Removes the specified key from the map.

#### hasFlag(String key): boolean

Returns `true` if the specified key exists in the map.

**NOTES:**
- Integers are stored separately from string flags, so it will *not* recognise integer values stored using the `setInt` or `addToInt` methods.


**Code Example:**
```Velocity
#set($canFlashBreasts = !$w.getTop().isAlsoLowerBody()     
          || $w.getTop().hasFlag("LOWCUT")   
          || $w.getTop().getTopType() == "HALTERTOP")##
```          
#### getInt(String key): int

Returns the integer value associated with this key. 

**NOTES:**
- This method will return `0` if no integer value has been stored using the key.

#### setInt(String key, int value): void

Stores the specified integer value using the provided key, *overwriting* any existing values.

#### addToInt(String key, int amount): void

Increments the entry by the provided amount. 

**NOTES:**
- If there was no entry for that key then a new one will be created with amount as the value.
- To decrease an entry, use a negative number for the integer parameter.

### Other Actions

#### stripNaked(): void

Removes all of the character's clothing.

#### fixClothing(): void

Puts all the character's clothing back on and fixes it to a normally-worn state.

#### setHairstyle(String style): void

Changes the character's hairstyle to the one given as a parameter. 

**Hairstyles:**
| Gender | Style |
| ------ | ----- |
| MALE | `BALD` |
| MALE | `SHORT_HAIR` |
| MALE | `SHOULDER_LENGTH_MENS_HAIR` |
| MALE | `MAN_BUN` |
| UNISEX | `AFRO` |
| UNISEX | `SHAVEN_HEADED` |
| UNISEX | `MULLET` |
| FEMALE | `SHORT_BOB` |
| FEMALE | `PIXIE_CUT` |
| FEMALE | `BUN` |
| FEMALE | `SHOULDER_BOB` |
| FEMALE | `SHOULDER_STRAIGHT` |
| FEMALE | `WAVY_SHOULDER_LENGTH` |
| FEMALE | `PONYTAIL` |
| FEMALE | `PIGTAILS` |
| FEMALE | `LONG_PONYTAIL` |
| FEMALE | `LONG_HAIR` |
| FEMALE | `WAVY_LONG` |

**NOTES:**
- The parameter must be a valid hairstyle (see the enum reference) or this method will error.

### Text Getters

Text getters retrieve text that's suitable to be inserted directly into output. 

#### getDescription(): String

Returns the character's text description as a full paragraph.

**NOTES:**
- This is the same as is output by the 'Describe Characters' button, although for NPCs it won't include the section about the PC's relationship with them.
- It's unlikely that you'll have cause to use this in your writing as it's simply restating what the character description outputs.

#### getName(): String

Returns the character's name with the first letter capitalised.

#### getEyeColour(): String

Returns the character's eye colour, lowercase with no preceding or following spaces.

**NOTES:**
- This string (like eye colour, race and skin colour) can have any value due to custom text being allowed, so it usually should not be tested in conditions. An exception is where your writing would be different if two characters have the same value, in which case you can check for equality. 

**Examples:**
- `blue`
- If both character's eyes are the same you could write "`his $m.eyeColour eyes meet yours`"
- If the eyes are different you could write "`his $m.eyeColour eyes meet your $w.eyeColour ones`".

#### getHairColour(): String

Returns the character's hair colour, lowercase with no preceding or following spaces. 

**NOTES:**
- For a player-character with dyed hair, this will return the dye colour.

**Example:** `black`

#### getRace(): String

Returns the character's race, lowercase with no preceding or following spaces. 

**NOTES:**
- Because custom races can use any string, you should usually only use this as a direct insert into text, except rarely where your writing depends on checking for two characters having the exact same string (see `getEyeColour()`). 
- Keep in mind that a player could have e.g. "Chinese" or "Japanese" as a custom string so you could get odd results if you're comparing race with "east asian" in order to write content based on them having "different" races. As a result, interracial content that depends on specific racial stereotypes is essentially impossible in Newlife. 

**Examples:** `black`, `white`, `east asian`


#### getSkinColour(): String

Returns the character's skin colour, lowercase with no preceding or following spaces. 

**NOTES:**

- See `getEyeColour` for comments on using this in conditions.

**Example:** `pale`

## Conditions



### Arousal

Arousal is stored for all characters, internally, as a number. 

The methods to check arousal levels will return `true` if the character's arousal meets *or exceeds* that particular threshold. For instance if the character's arousal is in the `CLOSE` category then `isArousalEnjoy` would return `true`, as would `isArousalClose`, but `isArousalOrgasm` would return `false`.

For writing, *arousal* should be checked against five general categories: discomfort, comfort, enjoy, close, orgasm.

| Type | Description | Notes |
| ---- | ----------- | ----- |
| Discomfort | The lowest level | This means a female character would not be comfortable having sex, even gently. |
| Comfort | Comfortable | A female character could have sex, but wouldn't want rough or vigorous intercourse except if they have specific traits that give them preferences for this. |
| Enjoy | Enoyment | The character is ready to enjoy any type of sex. |
| Close | The character is getting close to orgasm. | This should often affect descriptions for characters of both sexes. |
| Orgasm | Orgasm | Scenes that allow a character to orgasm should check every turn and trigger appropriate orgasm actions when a character's arousal exceeds this threshold. | 

**DEVELOPER NOTES:**
- Discomfort is largely ignored (for now) for male characters who are simplified as being always ready for sex. I may change this in the future so they aren't erect until comfort level. 
- Orgasm will likely be refined  in the future by exposing standard methods in custom scenes. 
- For a writer's first efforts I recommend avoiding the complex turn-based sex & makeout scenes that need to do full orgasm handling.

#### isArousalClose(): boolean

#### isArousalComfort(): boolean

#### isArousalEnjoy(): boolean

#### isArousalOrgasm(): boolean

## Other methods

### getAge(): String

Returns the character's age as an enum String. 

**Ages**:
| ENUM | Scope | Description | Notes |
| :--- | :---- | :---------- | :---- |
| `LATE_TEENS` | PC/NPCs | 18 or 19 years-old | You mustn't use text to imply she's younger. |
| `EARLY_TWENTIES` | PC/NPCs | 20 - 24 years-old | |
| `TWENTIES` | PC/NPCs | Refers to late-twenties. 25-29 years-old | |
| `THIRTIES` | PC/NPCs |  | |
| `FORTIES` | NPCs |  | Male Only |
| `FIFTIES` | NPCs |  | Male Only |
| `OLD` | NPCs | Any character 60 or older. | Male Only |

**NOTES:**
- See the enum reference for possible values.
- Note that these are `CAPITALISED` and *may* contain underscores so they are *not* suitable for direct insertion into text shown to the player.

### getId(): String

Returns the ID that this character is known as in this scene.

**Examples:** `jerk`, `m`, `f`, `gf`, `bf`

### isOlderThan(String age): boolean

Returns `true` if the character is older than the [age](enum#age) parameter. 

**Ages**:
| ENUM | Scope | Description | Notes |
| :--- | :---- | :---------- | :---- |
| `LATE_TEENS` | PC/NPCs | 18 or 19 years-old | You mustn't use text to imply she's younger. |
| `EARLY_TWENTIES` | PC/NPCs | 20 - 24 years-old | |
| `TWENTIES` | PC/NPCs | Refers to late-twenties. 25-29 years-old | |
| `THIRTIES` | PC/NPCs |  | |
| `FORTIES` | NPCs |  | Male Only |
| `FIFTIES` | NPCs |  | Male Only |
| `OLD` | NPCs | Any character 60 or older. | Male Only |

**NOTES:**
- This parameter *must* be a *valid* [age](enum#age) enum string.
- The character must be strictly older for this to return `true`. 

**Example:**
If the character is in their thirties then `isOlderThan("THIRTIES")` will return `false` but `isOlderThan("TWENTIES")` will return `true`.

### isNaked(): boolean

Returns `true` if the character is completely naked.

**NOTES:**
- Also see [isNakedExceptLegwear](Context-Objects#isnakedexceptlegwear-boolean).

### isDrunk(): boolean

Returns `true` if the character counts as drunk or higher.

**NOTES:** 
- Clear headed player-characters (`CLEAR_HEAD`) *never* count as drunk. This should be used to affect descriptive text.
- Alcohol's effect on willpower tests is handled *automatically*, you don't need to write modifiers based on it.

### isVeryDrunk(): boolean

Returns `true` if the character is very drunk.

**NOTES:**
- At this level they may need alternative paths where they slur their words, fall over, say something they shouldn't or generally make other 'boozy' mistakes.

### isMaxDrunk(): boolean

Returns `true` if the character has reached the maximum drunkenness level.

**NOTES:** 
- Newlife doesn't have characters passing out, but at this level they might need to call an end to an evening early, be helped home, or start  feeling sick. Characters who drink this much should also have a hangover the next day if your scene is one that lasts overnight.

### getStrength(): int

Returns an integer value representing the character's strength.

**NOTES:**
- For the player this is the *fitness* skill with deductions if she's drunk.
- For NPCs this is based on body-type, age and alcohol level.
- While the logic behind the number varies for different character types, the intent is that the value can be compared, e.g. if you need to test whether the PC can win an arm-wrestle with her date.
- The value can go negative and may go *above* 100 in the case of heavily-muscled men.
- This is intended to be used in text that compares characters' strength. However, if the PC is pushing an NPC around then you should add a  modifier to represent their weight: a fat character has low strength but would not be easy to move around.
- If your scene involves NPCs fighting then this should be the base value.  In that case it'd probably be best to also add a random modifier using `$scene.randomNumber`.
- Bear in mind for this that strength values can vary a lot between NPCs: e.g. a `MUSCULAR` NPC has a base of `120` while a `SKINNY` one starts at `5`. 
- Unless your random element is extremely large the stronger body-types (`TONED`, `THICKSET`, `MUSCULAR`) will have an *overwhelming advantage* over the others.

### getHairstyle(): String

Returns the character's hairstyle as an enum constant (see the enum reference for possible values). This can be used if you're writing content for a specific few hairstyles, e.g. if you wanted an action where someone grabs the PC by her pigtails, or where she makes fun of a bald man (but not one who shaves his head).

### getHairLength(): String

Returns the character's hair length.

**Hair Lengths:**
| Enum | Description | Notes |
| ---- | ----------- | ----- |
| `NONE` | Bald/shaved-head | | 
| `SHORT` | | |
| `SHOULDERS` | | |
| `LONG` | | |

**NOTES:**
- Hair length is a property of hairstyles, so a character with a particular style will always have the same length.

### getHasHair(): boolean

Returns `true` if the character has hair.

**NOTES:**
- Convenience method intended as an easier way to check if a character has hair: a fairly common check. 
- This is the equivalent to calling `getHairLength() != "NONE"`.

### getHasGrabbableHair(): boolean

Returns `true` if the character has hair that can be grabbed or pulled. 

**NOTES:**
- Usually `true` for shoulder-length (`SHOULDERS`) or longer hair (`LONG`).

### getHairCanFallInFace(): boolean

Returns `true` if the character's hair can fall into their face. 

**NOTES:**
- Used for text where a character brushes hair out of another's face.

----
# Player Character

These methods are available on the PC object. This has a context id of `w`, a holdover from the very first days of Newlife when it was just one scene with a man (or `m` for quickness of typing) and a woman (the `w` who would become the player-character).

The player-character (PC) is *always* present in custom scenes and there is only ever one of them.

## Actions

### Enjoyment

Enjoyment is a system used to track how much a character is enjoying themselves or another's company. This is then converted to relationship modifiers and stress reduction at the end of the scene-chain. This has nothing to do with the 'enjoy' arousal-level.

Enjoyment should be increased when the PC does something that makes her happy. 

**NOTES:**
- NoNpc methods principally affect stress levels.
- If the PC's enjoyment is due to an NPC, then use the appropriate methods on the NPC object to change the player's stress levels while setting them as the cause. This will usually be more appropriate than using the NoNpc methods in most scenes. The primary use of enjoyment is when a character takes an action that meets or opposes their partner's sexual preferences: the NPC methods should always be used in this case as enjoyment affects relationships.
- You do not need to add enjoyment when the PC drinks unless the experience is enjoyable for more than just the alcohol content (please note that alcohol also influences stress).
- You do not need to add enjoyment when the PC has an orgasm (an orgasm already provides a large increase to the PC's enjoyment).
- Use caution when increasing enjoyment in repeatable scene actions, especially if you scene lets the player loop through them many times: I want players to play the game as they feel their character would behave rather than grinding a certain action because of its game effects.
- It's also possible to modify stress directly in these cases: as a rule of thumb I'd use enjoy if something is pleasurable, enjoyable or boring (for negative changes) and change stress directly if something's relaxing or stressful.

#### addEnjoyTinyNoNpc(): void

Used for tiny changes.

**NOTES:**
- Feel free to toss this out quite casually.

#### addEnjoySmallNoNpc(): void

A small modifier, one that will have little effect on its own.

**NOTES:**
- This is appropriate for situations where enjoyment builds up over many small actions.

#### addEnjoyMedNoNpc(): void

A substantial effect. 

**NOTES:**
- Use only for quite significant things.

#### addEnjoyLargeNoNpc(): void 

A large increase.

**NOTES:**
- This is probably best used if you're using a single action to summarise an extended period of time such as a date, restaurant trip, visit to the cinema etc.

#### addEnjoyVLargeNoNpc(): void

A very large increase.

**NOTES:**
- This increase is the same as the PC having an orgasm.

#### reduceEnjoyTinyNoNpc(): void

Used for tiny changes.

**NOTES:**
- Reduces enjoy by the same amount `addEnjoyTinyNoNpc()` increases it. 

#### reduceEnjoySmallNoNpc(): void

**NOTES:**
- Reduces enjoy by the same amount `addEnjoySmallNoNpc()` increases it. 

#### reduceEnjoyMedNoNpc(): void

**NOTES:**
- Reduces enjoy by the same amount `addEnjoyMedNoNpc()` increases it. 

#### reduceEnjoyLargeNoNpc(): void

**NOTES:**
- Reduces enjoy by the same amount `addEnjoyLargeNoNpc()` increases it. 

#### reduceEnjoyVLargeNoNpc(): void

**NOTES:**
- Reduces enjoy by the same amount `addEnjoyVLargeNoNpc()` increases it. 

### Clothing changes

These methods modify one or more clothing slot's status. For more information on clothing statuses see the enum reference. This also lists allowable values.

These methods should be used when the PC dresses or undresses, but also if her clothes become disheveled.

Also see the Character `fixClothing()` and `stripNaked()` methods which remove or put on all of the character's clothing.

Valid clothes types are: `CASUAL`, `GOING_OUT`, `BUSINESS`, `ATHLETIC`, `NIGHTWEAR`, `SEXY_NIGHTWEAR`, `FORMAL`, `WEDDING`.

**Clothing Status Types:**
| Enum | Description | Notes |
| ---- | ----------- | ----- |
| `WORN` | The clothing item is being worn as intended. | |
| `DISHEVELED` | Generally set after the character is groped.  | *Not applicable for legwear.*  It has little in the way of gameplay effect but modifies her description. Disheveled clothing still covers whatever it was supposed to cover. |
| `EXPOSED` | The clothing has been moved aside. | *Not applicable for legwear.*  The exact description of how depends on the clothing item) and no longer covers whatever it was meant to cover. |
| `OFF` | The clothing slot is empty. | The outfit has no clothing for it or because the clothing has been removed completely. |

**NOTES:**
- `DISHEVELED` is spelt with one "l", which is the US-English spelling. Using the "dishevelled" spelling will result in an error.

**WARNING:** Be careful about setting clothing statuses. 
If an outfit did not include, say, a bra but you call `setBraStatus("WORN")` then they'll be described as wearing a "braless" and descriptive text will get muddled indeed. As a rule of thumb it's fine to *un*dress a character, but it's safest to use `fixClothing` if you need to put clothes back on.

#### hasOtherOutfitOfType(ClothesType type,): boolean

Returns `true` if the PC has an outfit of the specified type in her wardrobe, *not* including the one she's currently wearing. 

**NOTES:**
- To change outfits, use a transition to the outfit change scene (see yml guide for information on scene transitions).

#### attemptRemoveFromWardrobe(ClothingItem item): boolean

This is a very specific method that most writers will not need to use.

It does three things:
1. It takes off the specified clothing item.
2. It removes the clothing from her outfit so it won't be put back on if `fixClothing()` is called.
3. It attempts to *permanently* remove it from the PC's wardrobe.

**NOTES:**
- The clothing item must be one of the things the PC is wearing (i.e. the output of a method like `$w.getBra()`). Otherwise the method will return `false` and do nothing.
- Assuming this condition is met, the first two steps will always take place. Removal from the PC's wardrobe can fail however. 
- This will happen if the clothing item appears in every one of the PC's created outfits of a critical type (currently nightwear, business, casual). 
- Removing a clothing item un-creates every outfit it's a part of.
- The player **must** always have at least one outfit of each critical type defined or the game could encounter serious problems, so scenes are not allowed to violate this.
- The method will return `true` if the clothing item was successfully removed from the PC's wardrobe.

#### putOnLegwear(): void

Sets the character's legwear to `WORN`.

#### removeLegwear(): void

Sets the character's legwear to `OFF`.

#### setBottomStatus(String status): void

Sets lower-body clothing to the supplied status.

**NOTES:**
- For dresses and other items that cover multiple slots, setting the status in any one slot to `OFF` will remove them in both slots. However, setting status to `EXPOSED` or `DISHEVELED` will *not* affect the other slot: you can have a dress that's been pulled up (lower body status `EXPOSED`) but still covers her breasts properly (upper body status `WORN`).

#### setBraStatus(String status): void

Sets bra clothing to the supplied status.

#### setPantiesStatus(String status): void

Sets panties to the supplied status.

#### setTopStatus(String status): void

Sets upper-body clothing to the supplied status.

#### stripExceptLegwear(): void

Like stripNaked but will not remove any worn legwear.

### Other action methods

#### addTrait(String): void

Adds the Trait defined by the input parameter, which *must* be a *valid* PC trait.

**Notes:**
- There may be a few potential issues where a trait's effects apply at character creation and are not updated if the traits change.
- As a method intended for testing, this does *not* check for opposing traits. It's possible to create invalid trait combinations like `SHY` and `OUTGOING`. This would likely create bugs or bizarre text output so should be avoided even in testing.

**DEVELOPER'S NOTES:**
- This is intended for testing use only in the current version and should not generally be used in submitted scenes, unless you've discussed the specific case with me in advance.

#### addTempTrait(String trait, int time): void

Adds the specified trait as a temporary trait effect, which *must* be a *valid* PC trait. 

**NOTES:**
- This will last the number of weeks specified in the time parameter, which will start counting down from the start of the following week.
- Temporary trait effects will count as traits until it expires.
- This is intended for "mad science" side-effects, hypnosis or similar unnatural changes.

**DEVELOPER'S NOTES**
For example, if you add `BABY_CRAZY` as a temporary trait then `$w.hasTrait("BABY_CRAZY")` will return `true` until the temporary trait expires.

If you apply a temporary trait that's opposed to one of the PC's non-temporary traits then it will suppress that trait until the temporary effect wears off. For example, applying `RELAXED` as a temp trait will cause `$w.hasTrait("AMBITIOUS")` to return `false` even if the PC has the underlying trait.

If you have two or more temporary traits that are opposed to each-other then the first to be applied will count. So, applying first `REFINED` and then `SULTRY` will cause `$w.hasTrait("REFINED")` to return `true` and `$w.hasTrait("SULTRY")` to return `false`. However, the second temporary trait is still there and will start to apply if the first one wears off while it's still in effect. In addition, both traits will still suppress non-temporary opposing traits. 
In the above example `$w.hasTrait("SULTRY")` is `false` but so is `$w.hasTrait("SHY")` because the shy trait is suppressed by the opposing sultry temporary-trait.

Adding a temp trait will check if the PC is baby-crazy and stop her taking the pill if she is. If you're assigning baby-crazy as a temp trait and want special text to handle the situation where she was on the pill before then you need to make sure the check for this text is made *before* the temp trait gets assigned and changes the value.


#### changeAnxiety(int): void

Changes the character's anxiety by the parameter, which can be negative. 

**NOTES:**
- Use this very sparingly as anxiety should usually be 'spent' by cancelling skill increases and gained by having high stress at week end.
- It can be used to represent events so stressful or relaxing that they should have effects beyond even the normal stress system. For example, ambitious characters lose anxiety when promoted.

#### changeMoney(int): void

Modifies the player's money by the parameter. This can be negative.

**NOTES:**
- It's possible for the player to have negative money which would represent an overdraft, but it's usually preferable to check the PC's money before reducing it and block actions that involve spending if she doesn't have enough.

#### changeStress(int): void

Changes stress by the provided parameter. 

**NOTES:**
- Stress is usually changed in five-point increments, but you can use other values if it's appropriate.
- It's often better to reduce stress indirectly by changing enjoy & alcohol levels as appropriate. However, if an action is specifically relaxing rather than enjoyable then a stress reduction may be appropriate.
- Stress should be increased if the character does something that will stress her out (obviously!). 
- This can also be used as a 'cost' for the player going against their character's personality. 

**DEVELOPER'S NOTES:**
- I didn't want to block naked weddings for shy characters because the idea of a shy PC being embarrassed by getting wed in the nude is one many players would probably be interested in exploring. Instead, I allowed them to agree to a nude wedding but doing so causes an increase in stress.

#### clearStress(): void

Reduces the PC's stress to zero.

#### haveOrgasmNoNpc(): void

Causes the PC to have an orgasm, with no NPC listed as the cause.

**NOTES:**
- Orgasms modify enjoyment and stress processing. 
- Use this if the PC comes from solo enjoyment or due to a non-NPC character that isn't significant enough to be stored as a proper NPC.

#### removeTrait(String): void

Removes the Trait defined by the input parameter, which *must* be a *valid* PC trait.

**NOTES:**
- Does nothing if the PC doesn't have the trait.
- This is intended for testing use only. See the `addTrait` method for further information.

#### setOnPill(Boolean): void

Forces the PC to start or stop using the pill.

#### skillIncrease(String skill, int amount): void

Modifies the skill represented by the skill parameter by the integer amount. 

**NOTES:**
- The string *must* represent a *valid* skill as defined in the enum guide.
- This can be negative but Newlife usually does not reduce skills so this should only be done if you have very strong cause. 
- Use this sparingly and only with good reason. Skill training should be rare in scenes and usually done only in single point increments.
- This method will *not* increase a skill above its maximum. You may want to cap skill increases at lower levels in some cases: you can do this by wrapping the statement in an if statement.

### Text Getters

#### getEyeAdj(): String

Returns a single, lowercase adjective for the PC's eyes.

**NOTES:**
- There are a number of choices based on her traits and one will be chosen at random from the available ones.
- The method will *always* return a valid adjective. 
- This method will not always return the same value, although there's less than two-dozen adjectives in total so any one character will usually have at most a handful of posssible adjectives.
- The default is "`wide`" if the character doesn't meet the conditions for any others.
- Typically you would use this in sentences like: "`You look at $m.name with your $w.eyeAdj $w.eyeColour eyes.`" which would return something like "`You look at John with your sparkling blue eyes`".


#### getBreastsDesc(): String

Returns a string describing the PC's breasts. 

**Example:** `full breasts`

**NOTES:**
- String is lowercase with no preceding or trailing spaces.
- See the enum section on Breasts for the descriptions of each breast-size.
- Size will increase by one level in the late stages of pregnancy, returning to normal after birth.
- Female NPCs have this [method](Context-Objects#getbreastsdesc-string-1) as well.

#### getFigureDesc(): String

Returns a phrase describing the PC's figure that can be inserted into an appropriate sentence.

**Strings:**
- "fit and toned body with a feminine curve to your hips"
- "slender body with thin legs and slim, but still feminine, hips"
- "slim but curvy body with wide child-bearing hips"

**NOTES:**
- For general checks on the PC's figure use the `getFigure()` method described under condition methods.
- There is *no* equivalent to this method for female NPCs. For them you'll need to use an if-statement checking `getFigure` and write your own text.

#### getStomachDesc(): String

Returns a short phrase describing the PC's stomach. 

**Example:** `heavily pregnant belly`

**NOTES:**
- Descriptions of the PC's stomach may also need to check the `isStomachExposed()` method to see if it's bare or not.

#### getGirlOrWoman(): String

Returns either `girl` or `woman`.  This is a helper method that is sometimes useful in writing NPC's descriptions of the PC. It will return "girl" if the PC's age category is `LATE_TEENS` or `EARLY_TWENTIES`, or if it's `TWENTIES` and she has the `CUTE` trait.

**NOTES:**
- Be careful when writing adjectives preceding this method call. In particular "young woman" has a very different meaning to "young girl"!
- This method therefore won't fit every sentence, and sometimes it'll be better to just write out your own logic.

## Condition methods

### Clothing conditions & getters

#### Appearance

Clothing can be seen as "sexy", "elegant", "casual" or "cute".
- There are two axes: Elegant/Casual and Cute/Sexy.
- It's possible for the PC's outfit to be *neither* especially cute nor especially sexy.
- It's possible for the PC's outfit to be *neither* especially elegant nor especially casual.
- It's possible for the PC's outfit to be *both* sexy and elegant at the same time.
- It is *not* possible for the PC's outfit to be both cute *and* sexy at the same time.
- It is *not* possible for the PC's outfit to be both elegant *and* casual at the same time.

**Clothing Status Types:**
| Enum | Description | Notes |
| ---- | ----------- | ----- |
| `WORN` | The clothing item is being worn as intended. | |
| `DISHEVELED` | Generally set after the character is groped.  | *Not applicable for legwear.*  It has little in the way of gameplay effect but modifies her description. Disheveled clothing still covers whatever it was supposed to cover. |
| `EXPOSED` | The clothing has been moved aside. | *Not applicable for legwear.*  The exact description of how depends on the clothing item) and no longer covers whatever it was meant to cover. |
| `OFF` | The clothing slot is empty. | The outfit has no clothing for it or because the clothing has been removed completely. |

**NOTES:**
- `DISHEVELED` is spelt with one "l", which is the US-English spelling. Using the "dishevelled" spelling will result in an error.

#### getBra(): ClothingItem

Returns the PC's bra clothing item object.

**NOTES:**
- You should check `getBraStatus()` first to make sure that she's actually wearing one.

#### getBottom(): Lower Body Clothing

Returns the PC's lower body clothing.

**NOTES:**
- You should check `getBottomStatus()` first to make sure that she's actually wearing some.

#### getTop(): Upper Body Clothing

Returns the PC's upper-body clothing. 

**NOTES:**
- You should check `getTopStatus()` first to make sure that she's actually wearing some.

**Code Examples:**
```Velocity
#if (!$w.getTop().isAlsoLowerBody())##
You lift your $w.getTop().getBasicDesc() and let the crowd look at your $w.getBra().getBasicDesc(). ##
#elseif ($w.getTop().hasFlag("LOWCUT"))##
You pull down the top of your $w.getTop().getBasicDesc() and let the crowd look at your $w.getBra().getBasicDesc().
#elseif ($w.getTop().getTopType() == "HALTERTOP")##
You grab the sides of your $w.getTop().getBasicDesc() and pull them together, letting the crowd look at your $w.getBra().getBasicDesc().##
#else##
You flash your $w.getBra().getBasicDesc() at the crowd on the patio. ##
#end##
```

#### getLegwear(): Legwear

Returns the PC's legwear.

**NOTES:**
- You should check `isLegwearWorn()` first to make sure that she's actually wearing some.

#### getPanties(): ClothingItem

Returns the PC's panties clothing item object.

**NOTES:**
- You should check `getPantiesStatus()` first to make sure that she's actually wearing some.

#### getBottomStatus(): String

Returns the lower-body clothing status.

#### getBraStatus(): String

Returns the bra clothing status.

#### getPantiesStatus(): String

Returns the panties clothing status.

#### getTopStatus(): String

Returns the upper-body clothing status.

#### isLegwearWorn(): boolean

Returns `true` if the legwear status is `WORN`. Otherwise, it indicates that the legwear is `OFF` as the other two statuses are not available for legwear.

#### isPussyExposed(): boolean

Returns `true` if the PC's pussy is exposed allowing her to be penetrated, touched or whatever. 

**NOTES:**
- This checks clothing statuses and the length of her lower-body clothing if it's a skirt. 
- Typically you'd use this in your writing rather than checking bottom and panties statuses.

#### isBreastsExposed(): boolean

Returns `true` if the PC's breasts are uncovered.

#### isStomachExposed(): boolean

Returns `true` if the PC's stomach is bare, either due to her top being `OFF` or `EXPOSED` or due to it having the `SHOWS_TUMMY` flag.

#### isClothesDisarrayed(): boolean

Returns `true` if *any* of the PC's outfit has been disarrayed in any way.

**NOTES:**
- If any item has a clothing status other than `WORN` or, in the case of clothing slots where the outfit has no clothing item, `OFF`.

#### isNakedExceptLegwear(): boolean

Returns `true` if the PC is completely naked *or* if she's only wearing legwear.

**NOTES:**
- Also see [isNaked](Context-Objects#isnaked-boolean).

#### isOutfitCute(): boolean

Returns `true` if the PC's outfit is noticeably cute. 

**NOTES:**
- This includes any bonus from the fashion skill but does *not* include any base cuteness value the player themselves has (e.g. from the cute trait).
- Undressing the player does *not* affect their underlying outfit stats and will *not* change what this method returns.
- It's possible for the PC's outfit to be *neither* especially cute nor especially sexy.
- It is *not* possible for the PC's outfit to be both cute *and* sexy at the same time.
- "Cute" requires >= 5 (as of Newlife 0.4.30)) but the exact internal numbers may change in the future.

#### isOutfitSexy(): boolean

Similar to `getOutfitCute` but checks for "sexiness" (i.e. negative cuteness).

#### isOutfitElegant(): boolean

Similar to `getOutfitCute` but checks for elegance. 

**NOTES:**
- The Elegant/Casual axis is tracked separately from the Cute/Sexy one, so it's possible to be e.g. both sexy and elegant at the same time.

#### isOutfitCasual(): boolean

Similar to `getOutfitCute` but tracks Casualness. 

**NOTES:**
- Casualness is opposed to Elegance. An outfit can be casual, elegant or neither; but it can never be both at once.

### Stress

| Level | Threshold | Notes |
| ----- | --------- | ----- |
| 0 | Low | |
| 50 | High | The PC is on the edge and possible make poor decisions or lose her temper. |
| 80 | Extreme | 
| ?  | Maximum |

#### isAnxious(): boolean

Returns `true` if the PC's anxiety is greater than zero. 

**NOTES:**
- On rare occasions it's worth restricting certain stressful/high-pressure actions in this case, as an additional penalty to having anxiety. For example, breaking up with her partner unless her personality means this is something she'd enjoy (e.g. bitchy).

#### isHighStress(): boolean

Returns `true` if the PC's stress level is over the 'high' threshold.

**NOTES:**
- This can be used to restrict actions that imply the PC is especially calm, or to have her make bad decisions like losing her temper and snapping at someone due to stress.
- This can be used to gate content where other characters try to comfort her or calm her down.

#### isExtremeStress(): boolean

Returns `true` if the PC is over the 'extreme' stress threshold. `isStressHigh` is more usually checked in writing so this will probably be used quite rarely.

#### isMaxStress(): boolean

Returns `true` if the PC has reached the maximum stress level. It's unusual that you'd need to check this in your writing: `hasAnxiety` and `isHighStress` are the main ones you're likely to need to check.

### Willpower

These run a willpower test that is not related to a specific NPC. For willpower tests where there's a relevant NPC (e.g. checking if she's too turned on to stop having sex or whatever) you should use the NPC `testWill` methods instead as they will include additional modifiers based on that NPC.

Willpower should be used to block access to actions. It shouldn't be used to access special content as that would then be unavailable to `IRON_WILL` characters.

Willpower tests are *primarily* based on *arousal*, but with additional modifiers on alcohol, traits, relationships and so on. There's also a random element.

Willpower methods have an optional integer modifier. This affects the difficulty of the willpower test. If there are specific traits or whatever that would affect the PC's willpower test in your specific action but not in general then you should check for them and vary the modifier appropriately. 

**USAGE:**
For instance if the willpower test is to enable the ability to ask him to wear a condom then it should get an additional penalty if the PC has the `LIKES_BARE` trait.

**NOTES:**
- Because willpower tests are based on arousal, it's important to consider the context of your scene. If it's a sex scene that expects to push arousal right up to orgasm levels then you'll generally want medium-difficult tests that'll fail when the PC gets close to orgasm.
- Makeout scenes will have harder tests for many of their actions as they aren't supposed to only start failing when the PC's about to come. The key question is: "how turned on would an average PC have to be to fail this test?"
- In some occasions willpower tests won't be applicable. In particular, during orgasm processing as the PC's arousal will always be at the orgasm threshold. In these cases you should just use direct checks for the willpower traits e.g. having separate paths for iron-will/high willpower vs normal/low.

#### Modifiers

Modifiers should usually be multiples of 5 or 10 as arousal is internally on a 100-point scale so single point modifiers are fairly insignificant. 
Generally a small bonus/penalty would be +/- 5, a moderate one +/-10, a major one +/-20 and a massive one +/- 30. 
You should avoid having a total modifier of more than 30 or less than -30 if possible and even these are quite extreme values.


#### testWillEasy(int modifier): boolean

A very easy willpower test that an average character wouldn't be likely to fail unless she was actually at the orgasm level of arousal. 

**NOTES:**
- Rarely used in writing, but an option if you want tests that will only be failed by characters with low willpower, bad luck or additional negative modifiers.

#### testWillNormal(int modifier): boolean

A willpower test that with a modifier of 0 will be failed by an average character at around the `CLOSE` arousal state. 

**NOTES:**
- The main one to use in sex scenes.

#### testWillHard(int modifier): boolean

A willpower test that with a modifier of 0 will be failed by an average character at around the `ENJOY` arousal state. 

**NOTES:**
- A common test in makeout scenes or similar ones that don't expect to push the PC all the way to orgasm.

#### testWillVeryHard(int modifier): boolean

A willpower test that with a modifier of 0 will be failed by an average character at around the `COMFORT` arousal state. 

**NOTES:**
- Probably won't be commonly used due to its excessive difficulty: comfort is a very low threshold to use for disabling player actions. 
- You could use it for very negative actions though that imply the PC is disgusted with her partner. Of course if she's with a partner then you should be using the maleNpc willpower method instead...

### Other Condition methods

#### getFigure(): String

Returns the PC's figure as an enum string value.

**FEMALE FIGURE TYPES:**
| Enum | Description | Notes |
| ---- | ----------- | ----- |
| `SLIM` | A slender and delicate figure.  | Initially the weakest figure but this can change if the PC trains fitness so should not be assumed. |
| `TONED` | A healthy fit physique, slim with lean muscles. |  |
| `WOMANLY` | An hourglass body with pronounced feminine curves. | This one can be a bit tricky to write for as words like "curvy" are often used for "BBW" body-types. I tend to use "curvaceous" or "hourglass" instead. |

#### getBreasts(): String

Returns the PC's breast size as a string enum. 

**BREAST TYPES:**
| ENUM | Scope | Description | Notes |
| :--- | :---- | :---------- | :---- |
| `SMALL` | PC/NPCs | small but perky tits | |
| `MEDIUM_SMALL` | PC/NPCs | pert tits | |
| `MEDIUM_LARGE` | PC/NPCs| full breasts | |
| `LARGE` | PC/NPCs | heavy breasts | |

**NOTES:**
- This isn't suitable to be inserted into text shown to the player, use `getBreastsDesc` for that. See the enum reference for possible values.


#### getMoney(): int

Returns how much money the PC has.

**NOTES:**
- Usually used to check she has enough to pay for something before enabling an action to buy it.

#### getSkill(String skill): int

Returns the numeric skill value for the skill set as a parameter. 

**NOTES:**
- See enum reference for information on the different skills.

#### hasStuff(String stuff): boolean

Returns `true` if the PC has the Stuff item passed in as a parameter.

**NOTES:**
- See the enum reference for valid values. 
- Mostly used to gate actions behind the PC having the required items e.g. a kettle for "drink tea" actions.
-- It's sometimes worth giving the player a nod towards having acquired items in your writing too. For instance if the PC has the giant teddy bear then there's a line about having to move it out of her bed to make room for a bloke when he sleeps over.
- Of some note for sexual content are the condoms, which are relevant if an NPC refuses to rubber-up because he doesn't have one with him.

#### getPregnancyStage(): String

Returns the character's pregnancy stage.

**PREGNANCY STAGES:**
| Stage | Description | Notes |
| ----- | ----------- | ----- |
| `FLAT` | Flat stomach | Either she isn't pregnant or she's in the first trimester. |
| `BUMP` | Small baby bump | Second trimester. |
| `BIG` | Pregnant belly | First half of the third trimester. |
| `HUGE` | Heavily pregnant belly | Second half of the third trimester. |

**NOTES:**
- This should not be used to check if she's pregnant or not as `FLAT` will be returned for **both** first-trimester pregnancies and when she isn't pregnant.
- Use `isKnownPregnant` to check for pregnancy and `getStomachDesc` if you need text to directly insert into a description.

#### getOrgasms(): int

Returns the number of orgasms the PC has had in this scene chain.

#### hasTrait(String trait): boolean

Returns `true` if the PC has the provided trait.

**NOTES:**
- This is a key method that you'll need to use a lot in almost any Newlife writing.
- See the enum reference guide for a list of traits and discussion of how they're used.

#### isKnownPregnant(): boolean

Returns `true` if the PC is pregnant **and** knows it.

**NOTES:**
- A character who isn't knowingly pregnant will always have a FLAT pregnancy stage. The PC always discovers her pregnancy before it starts to show. As such, if `isKnownPregnant` returns `false` you can assume the PC has a flat stomach.
- Scenes should treat a PC who's pregnant but *doesn't* know it exactly  the same as if she wasn't pregnant, so this is the method you should use to gate pregnancy text.

#### isLactating(): boolean

Returns `true` if the PC is lactating.

**NOTES:**
- Lactation is something which may be worth mentioning in descriptions or in text based around her breasts.
- You shouldn't make assumptions about pregnancy from this trait. It's possible to not be lactating despite being heavily pregnant (if lactation is disabled in the game options) and it's possible to be lactating despite never having been pregnant due to the milky trait.
- Female NPCs have a [method](Context-Objects#islactating-boolean-1) that uses the same name.


#### isMum(): boolean

Returns `true` if the PC has at least one child.

#### getBabies(): Collection `<Baby>`

Returns a collection of Baby objects which may be empty but will not be null.

**NOTES:**
- See the "Baby" section for more details.

#### isOnPill(): boolean

Returns `true` if the PC is on the contraceptive pill.

#### isRisky(): boolean

Returns `true` if this counts as a risky day.

**NOTES:**
- This is when the "you are likely to get pregnant" warning is shown in the character description.
- The method will return `false` if the PC is **knowingly pregnant** or on the pill.
- It can still return true if she has the infertile trait however, as this assumes the PC doesn't necessarily know that she can't conceive without assistance.

#### isSafe(): boolean

Returns `true` if this counts as a 'safe day' when the PC is unlikely to get pregnant.

**NOTES:**
- This happens if the PC is on the pill or if it's a safe time in her monthly cycle.
- Many days will be neither risky nor safe, so your writing shouldn't assume those are the only options.
- When writing safe/risky text it's usually best to have further checks before these two methods.

**DEVELOPER TIPS:**
Typically I'd write an if-else statement with the following checks each with their own text:
1. Is the PC knowingly pregnant already?
2. Is she on the pill?
3. Is it a safe day?
4. Is it a risky day?
5. A default text section for the not-safe but not her most fertile time either weeks.

Within these text sections I'd generally take further things into account.

For instance:
- is the pc trying for a baby with her partner?
- Does she have the maternal trait? The baby-crazy one?
- Does she already have children?
- Is she in a relationship with the man? 
- How does she feel about him, with special attention to love or disliked?

Then if the text covers the man's behaviour similar checks need to be made for him.
1. Does he have either the `WANTS_KIDS` or `DOESNT_WANT_KIDS` traits? Neither?
2. Does he like or love the PC?
3. Is she in a relationship with him?
4. What about Impregnator? An impregnator who doesn't want kids might try to fertilise the PC if she's a random hookup but be less keen if she's his girlfriend and he might have to stick around and raise the child.

#### isSingle(): boolean

Returns `true` if the PC does not have a partner (i.e. a boyfriend, fiancé or husband).

#### isMarried(): boolean

Returns `true` if the PC is married (i.e. she has a partner and their relationship level is `MARRIED`).

**NOTES:**
- If you need more details about her husband (e.g. his name) then you should include him as an NPC in your scene: a hidden one if he isn't actually present.
- This will return `true` if the PC is married, but it doesn't necessarily mean she's married to the specific NPCs present in your scene. To check if she's married to a particular person use the NPC `getRelationship` method.

#### isLivingWithPartner(): boolean

Returns `true` if the PC lives with her partner, `false` if she's single or not living with them.

**NOTES:**
- This currently only returns `true` when the PC is married. This is unlikely to change in future releases but it's been added separately from `isMarried` just in case.

#### isSkillMaxed(String): boolean

Returns `true` if the skill represented by the enum parameter is maxed out.

**NOTES:**
- You probably won't have much cause to use this in your writing.

**DEVELOPER'S NOTES:**
- There may be times when you will need it however, for example, if your scene involves a 'skill training' path then it might be good to have alternative text if the PC is so good they can't improve further.

#### isVirgin(): boolean

Returns `true` if the character is a virgin. 

**NOTES:**
- Virginity is removed at the end of a vaginal sex scene.

**DEVELOPER COMMENTS:**
- I personally tend to write a lot of alternative "first time" text.

#### isAnalVirgin(): boolean

Returns `true` if the character hasn't had anal sex to completion.

#### IsLesbianVirgin(): boolean

Returns `true` if the PC has not had lesbian sex.

#### likesFigure(String maleFigure): boolean

Returns `true` if the PC likes the male figure passed in as the String parameter.

**NOTES:**
- The parameter *must* match a *valid* male body type enum value.
- You can use this to check if she likes an NPC's body with e.g. `$w.likesFigure($m.figure)`.
- This checks the PC's body-type preferences set in character creation.
- Note that both this and `dislikesFigure()` will return `false` if the PC is *neutral* towards the body-type.

#### dislikesFigure(String maleFigure): boolean

Returns `true` if the PC dislikes the male figure represented by the parameter.

**NOTES:**
- Both this and `likesFigure` will return `false` if the PC is *neutral* towards the body-type.

#### isAllowedMoreFriends(): boolean

Returns `true` if the PC has not yet reached their maximum number of close friends.

----
# NPC

These methods are available on *both* male and female NPCs.

In some cases they modify the relationship between the pc and that NPC, or trigger changes on the PC that are caused by the NPC.

## Actions

### Enjoyment:

These methods modify enjoyment for the specified NPC.

Enjoyment is a system used to track how much a character is enjoying themselves or another's company. This is then converted to relationship modifiers and stress reduction at the end of the scene-chain. This has nothing to do with the 'enjoy' arousal-level.

Enjoyment should be increased when the NPC does something that makes them happy. 

**USAGE:**

Enjoyment is for when they specifically meet preference traits or do something that stands out as being particularly preferable to the other person. 
Often this will be combined with a larger arousal benefit. Enjoyment reduction can be used in the opposite situation. 

**TIPS:**
- For **enjoyment** increases to the PC that *aren't* caused by a particular NPC use the methods under the player-character object.
- Typically **enjoyment** should be increased when one character does something to meet another's sexual preferences. It shouldn't be applied for every erotic action: use arousal for that.

**Examples:**
- An NPC talks dirty to a PC with the `OVERACTIVE_IMAGINATION` trait.
- The PC puts a condom on an NPC with the `CONSCIENTIOUS` trait.
- The PC acts in a cute/innocent way towards an NPC with the `LIKES_CUTE` trait.
- The PC initiates or encourages sexual activity when the NPC is horny and fancies her.
- The PC does something romantic towards an NPC with a romantic personality and a *love* status of `SOME` or higher. Or, the other way around with a PC who has the romantic trait.


#### addEnjoyTiny(): void

#### addEnjoySmall(): void

#### addEnjoyMedium(): void

#### addEnjoyLarge(): void

#### addEnjoyVLarge(): void

#### reduceEnjoyLarge(): void

#### reduceEnjoyMedium(): void

#### reduceEnjoySmall(): void

#### reduceEnjoyTiny(): void

#### reduceEnjoyVLarge(): void

#### addWEnjoyTiny(): void

#### addWEnjoySmall(): void

#### addWEnjoyMedium(): void

#### addWEnjoyLarge(): void

#### addWEnjoyVLarge(): void

#### reduceWEnjoyLarge(): void

#### reduceWEnjoyMedium(): void

#### reduceWEnjoySmall(): void

#### reduceWEnjoyTiny(): void

#### reduceWEnjoyVLarge(): void

### Relationship facet modifiers

These methods modify the relationship facets Liking and Love.

There are methods to modify both how the PC views the NPC and how the NPC considers the PC. The former use `w` as the shortcut for the PC so `addWLikingTiny()` increases the player-character's liking of the NPC while `addNpcLikingTiny()` changes how the NPC views the player-character.

See the relationship getters section below for more discussion on how Love and Liking should be used in writing and scene structure.

These methods aren't processed until the **end** of the scene-chain. As such you can't modify relationships and then expect to see the effects immediately reflected in the underlying data.

Smaller modifiers have a total cap across the scene-chain to stop extreme changes if many small modifiers build up over the course of a date. There are uncapped methods that don't apply this cap, and the largest increases (massive and gigantic) are never capped as even a single modifier of this level would exceed the cap.

**Liking and Love Levels:**
| Level | Description | Example | Notes |
| ----- | ----------- | ------- | ----- |
| Tiny | Suitable for small modifiers, such as individual lines of dialogue. | A compliment or rude comment. | |
| Small | Individual dialogue lines, but only when they're particularly liked or disliked. | | Double a tiny modifier. |
| Medium | Long-duration actions | Having dinner together. Seeing a movie. | Double small. |
| Large | One character is especially moved or offended. | | Triple small. |
| Very-Large | A major event | |  Comes in basic and uncapped versions. |
| Massive | Very big change from a single action | Breakups. | |
| Gigantic | A huge change. | Bad breakups and the like. | Three of these would drop a character from the highest possible liking value all the way down to Disliked. |


**TIPS:**
- Actions that are sexually pleasurable but don't particularly meet special preference traits or involve a character making a sacrifice for their partner should increase *arousal* **only**.
- Sexual actions that meet preference traits or involve a character going out of their way for their partner should increase both *arousal* and *enjoyment*, but **not** relationship facets directly.
- Actions or situations that involve characters spending pleasant time together or becoming closer as people should increase *Liking*.
- Actions or situations where one character shows qualities that the other finds admirable should increase **both** *Liking* and *Love*.
- Actions where a character annoys, upsets or insults another character should reduce *Liking* and often (but not always, depending on context) *Love*.
- If a character does something that implies they particularly liked or hated something the other character did, then relationship facets should be modified appropriately, or *enjoyment* if it's in asexual context.
- Major actions that should have a dramatic effect on a relationship should be given major modifiers. 
- When adding a penalty to the PC's liking, it's worth considering if you should also add *bastard* points. See `addBastard` for more information on this.
- Some actions will have much larger effects on one facet than on the other.

**Examples**
- If an NPC says something rude and you give the PC actions to forgive him or be angry, then the PC should have a larger relationship reduction if the player chooses the angry action.
- If the PC tells her boyfriend that she fancies his friend more, and then goes off to sleep with said friend then he should get a major reduction to Liking and Love towards her.
- If an NPC makes romantic overtures to the PC but she's rude to him then he should get a large *Liking* reduction but a small (or no) *Love* modifier, potentially leading to a situation where he's obsessed with winning her over despite not actually liking her as a person.
- If the PC realises that a man she fell for isn't actually someone whose character she admires. This would drop *Love* massively but might have a much smaller effect on *liking*, especially if the reason she's falling out of love with him is one that doesn't make him dislike him as a person (such as an ambitious character discovering he lacks drive).

#### addNpcLikingTiny(): void

#### addNpcLikingSmall(): void

#### addNpcLikingMedium(): void

#### addNpcLikingLarge(): void

#### addNpcLikingVLarge(): void

#### addNpcLikingVLargeUncapped(): void

#### addNpcLikingMassive(): void

#### addNpcLikingGigantic(): void

#### addNpcLoveTiny(): void

#### addNpcLoveSmall(): void

#### addNpcLoveMedium(): void

#### addNpcLoveLarge(): void

#### addNpcLoveVLarge(): void

#### addNpcLoveVLargeUncapped(): void

#### addNpcLoveMassive(): void

#### addNpcLoveGigantic(): void

#### addWLikingTiny(): void

#### addWLikingSmall(): void

#### addWLikingMedium(): void

#### addWLikingLarge(): void

#### addWLikingVLarge(): void

#### addWLikingVLargeUncapped(): void

#### addWLikingMassive(): void

#### addWLikingGigantic(): void

#### addWLoveTiny(): void

#### addWLoveSmall(): void

#### addWLoveMedium(): void

#### addWLoveLarge(): void

#### addWLoveVLarge(): void

#### addWLoveVLargeUncapped(): void

#### addWLoveMassive(): void

#### addWLoveGigantic(): void

#### reduceNpcLikingTiny(): void

#### reduceNpcLikingSmall(): void

#### reduceNpcLikingMedium(): void

#### reduceNpcLikingLarge(): void

#### reduceNpcLikingVLarge(): void

#### reduceNpcLikingVLargeUncapped(): void

#### reduceNpcLikingMassive(): void

#### reduceNpcLikingGigantic(): void

#### reduceNpcLoveTiny(): void

#### reduceNpcLoveSmall(): void

#### reduceNpcLoveMedium(): void

#### reduceNpcLoveLarge(): void

#### reduceNpcLoveVLarge(): void

#### reduceNpcLoveVLargeUncapped(): void

#### reduceNpcLoveMassive(): void

#### reduceNpcLoveGigantic(): void

#### reduceWLikingTiny(): void

#### reduceWLikingSmall(): void

#### reduceWLikingMedium(): void

#### reduceWLikingLarge(): void

#### reduceWLikingVLarge(): void

#### reduceWLikingVLargeUncapped(): void

#### reduceWLikingMassive(): void

#### reduceWLikingGigantic(): void

#### reduceWLoveTiny(): void

#### reduceWLoveSmall(): void

#### reduceWLoveMedium(): void

#### reduceWLoveLarge(): void

#### reduceWLoveVLarge(): void

#### reduceWLoveVLargeUncapped(): void

#### reduceWLoveMassive(): void

#### reduceWLoveGigantic(): void

### Other Actions

#### addBastard(int amount): void

Adds the specified amount of *bastard* points to the NPC.

Once bastard points reach or exceed 100 there'll be a decision scene at the start of the week where the player decides how their character will react. Some decisions will stop the character from accumulating further points but this is handled internally and you don't need to check for it. Characters already flagged as bastards don't get the scene but will get a passive loss of liking points if they reach the cap again.

Bastard points have no effect for Female NPCs currently, but this may change in the future so it's preferable to call this method when relevant.

Some special NPCs are automatically flagged as bastards – such as the lowlives and the perverted sales client. It isn't necessary to add bastard points when writing scenes for these NPCs.

**USAGE:**
- Points should be added when the character does something that shows them to be an awful person. This won't always apply to liking loss in general – a refined character might take offence at public improprieties or a romantic one might be upset by unromantic behaviour, but these should not give bastard points.
- Directly insulting the PC should give 10 points unless there's a good and justifiable reason for it. 
- More serious actions should give more.
- Atthe highest extreme, catching the NPC sabotaging the PC's pills gives 100.
- Actions the PC doesn't know about (e.g. successfully sabotaging her pills without getting caught) should *not* give bastard points.


#### addTrait(String trait): void

Adds the specified trait to the NPC.

**NOTES:**
- To be used very sparingly – typically for adding the handful of traits that represent things that happen in-game such as `TROUNCED`. Most scenes will not need to call this.
- Does *not* check for opposite traits first. You need to do this manually before calling the method.
- This also won't check if it's a valid trait for their gender – you need to check that too. Wrong-gender traits typically won't cause bugs the same way opposite ones would, but it's still something that needs to be handled before submitting a scene.

#### addRelationshipFlag(String flag): void

Adds a relationship flag to the NPC. 

**NOTES:**
- Also see `removeRelationshipFlag`
- This has considerable overlap with NPC traits, as is discussed in the `hasRelationshipFlag` method description.
- You can add a relationship flag to represent some persistent change in the characters' relationship: use the testing flag as a placeholder and make sure to include a comment with the actual value you want this to be replaced with when your scene is integrated in the game.
- Relationship flags do *not* appear in the character browser. For that you need to use an NPC trait.

#### addSexualActivity(String activity, boolean canCountAsCheating): void

Sets the specified sexual activity as having taken place, which may count as cheating if the boolean parameter is set to `true`.  See the enum reference for a list of SexualActivity values and when they should be set.

**NOTES:**
- If your scene is a sub-scene then you should check for the scene flag `NOT_CHEATING` (case sensitive). This can also be set before calling transition to a makeout or other existing Newlife scene, and will stop it from counting any sexual content as being cheating. This should be done if the PC's actions are with the knowledge & consent of her partner.
- Additionally, it shouldn't count as cheating if something happens that the PC hasn't welcomed or initiated – for example if a guy just walks up and grabs her tits. However, if she's been flirting with him first then it should anger her SO and therefore should count as cheating.
- This method should be called when the PC engages in any relevant SexualActivity with an NPC.
- Currently `ANAL` is *not* a valid call for female NPCs, and will cause an error if used as the activity parameter with them.  
- Calling this method with "SEX" as the activity will also set the PC to no longer be a virgin (or lesbian virgin as appropriate) if she was one before.

#### causePlayerOrgasm(): void

Triggers the player to have an orgasm caused by this NPC. 

**NOTES:**
- This will modify the appropriate values (arousal, enjoyment, relationship settings, `ALL_ORGASMS` stat etc). 
- If your scene is one where an orgasm should cause other effects (such as incrementing `ANAL_ORGASMS` or `SEX_ORGASMS`) then you need to call the appropriate methods in addition to this one.
- This will be flagged as cheating (moderate severity) if the PC has a partner who isn't this character.

#### causePlayerOrgasmNotCheating(): void

Same as causePlayerOrgasm except that it won't count as cheating if the PC is in a relationship with someone else.

**NOTES:**
- Use this instead of the above method if the orgasm shouldn't count as an unfaithful one (e.g if she's watching the man with another girl rather than being intimate with him directly) or if she's with another man with the approval of her partner.

#### haveOrgasm(): void

Sets the NPC as having had an orgasm. This has fairly few game-effects other than modifying the NPC's arousal back down to a low value.

**SPECIAL NOTE FOR MALE NPCs:**
For male NPCs this should be checked before accessing sex scenes. To avoid excessive repetition of the sex scenes in a single playthrough they shouldn't be excessively repeatable within a single scene chain. Even so, it's possible for the player to see the sex scenes dozens or in extreme cases hundreds of times in a game.
 
As such, the general rule is *one* orgasm per male NPC per scene chain. Exceptions can be made if a scene-chain lasts a lot of in-game time e.g. when the PC spends the night with someone.

If the PC is involved consider the `haveOrgasmFromPc` method which does the same as this one but also adds *enjoyment* based on their *attraction* to the PC.


#### haveOrgasmFromPc(): void

Like the `haveOrgasm` method in the NPC superclass but also gives the NPC a boost in *enjoyment* based on their *attraction* to the PC.

#### informVirgin(): void

Informs the NPC that the PC is a virgin. 

**NOTES:**
- Also see `informNotVirgin`
- This should only be called if she actually is one.

#### informNotVirgin(): void

Informs the NPC that the PC is not a virgin.

**NOTES:**
- Also see `informVirgin`
- Should not be called if she is, although NPCs do start off assuming the PC isn't one.

#### removeRelationshipFlag(String flag): void

Removes the specified relationship flag.

**NOTES:**
- Also see `addRelationshipFlag`
- If the flag is not set, this method will have no effect.
- If the flag is not set and this is called will *not* throw an error, so you don't need to first check that the flag is set before calling this.

#### breakup(boolean npcDecision): void

Ends any serious relationship between the PC and the NPC. 

The parameter is a boolean which sets whether the breakup was the NPC's decision or not. 

**NOTES:**
- Does *not* modify *Love* & *Liking* as it's possible that a breakup could be amicable.
- Has no effect if they aren't a proper couple (i.e. if `isPartner` would return `false`).
- You will usually need to add *Like* and *Love* modifiers in addition to calling this.
- If a breakup is triggered by the NPC then he deletes the PC's phone number and will be less likely to try to get together: PC-initiated breakups will often lead to the NPC quite quickly trying to win her back.


#### makeFriend(): void

Makes this NPC the PC's friend. 

**NOTES:**
- This doesn't necessarily mean they like each other, just that they'll be staying in regular contact.
- The method does nothing if the NPC is already the PC's friend, or if the PC has the maximum number of friends already.

#### endFriendship(): void

Unfriends the NPC. 

**NOTES:**
- This will also drop the NPC's liking towards the PC somewhat. 
- If the unfriend condition requires the PC to pay money then this will be deducted from her funds.
- The method does nothing if the NPC is not a friend of the PCs.

#### changeRelationshipStatus(String): void

Sets the PC and this NPC's relationship to the provided status, which *must* match a *valid* one defined in the enum reference document.

**RELATIONSHIPS:**
| Status | Description | Notes |
| ------ | ----------- | ----- |
| `STRANGER` | Starting level. | Automatically moves to `ACQUAINTANCE` when *knowledge* reaches a certain level. |
| `ACQUAINTANCE` | At this level NPCs will appear in the *NPC Browser*. | | 
| `DATE` | Set when the PC goes out with an NPC. | | 
| `COUPLE` | Boyfriend/girlfriend. Counts as being the PC's partner. | | 
| `ENGAGED` | Engaged to be married. |  |
| `MARRIED` | The PC is married to this NPC. | Implemented in 0.4.16 |

**NOTES:**
- This is a somewhat dangerous method because it does not check if the PC is in a relationship with anyone else. 
- You should be careful not to give the PC multiple boyfriends as this would introduce bugs. Make sure to check `$w.isSingle()` before setting status to `COUPLE`, `ENGAGED` or `MARRIED`.
- You should also be careful setting lower values: it would be possible to accidentally "dump" her BF by setting status to `DATE` or lower. Use the `breakup` method to end relationships, not this one.
- You don't need to set acquaintance level for strangers: just increase knowledge enough and it'll automatically be set.

**DEVELOPER NOTES:**
- You won't often need to call this method. Relationship transitions are normally handled by core content. The main use would be if you're writing a date scene and want to set status to `DATE` (make sure to check it isn't higher first though!) or if your scene involves the PC getting serious with someone and making them her boyfriend.

#### increaseKnowledge(int amount, int cap): void

Increases the PC's knowledge by the supplied amount up to the cap set in the second parameter.

**NOTES**:
- This affects the information shown about this NPC in the character browser.
- The psychic cheat gives the PC maximum knowledge for all NPCs.
- Once knowledge reaches a total of 4 or *higher* the NPC's relationship status will switch from `STRANGER` to `ACQUAINTANCE`, unless it was already higher.
- The game automatically increases the cap based on relationship levels – you don't need to do this.
- You also don't need to handle the `PERCEPTIVE` trait: this is dealt with when knowledge is checked, not when it's awarded.
- Knowledge should never be decreased.

**DEVELOPER TIPS:**
- Amounts should usually be quite low: a point or two at a time unless the PC is doing some serious research on them.
- For casual conversation and the like use a cap of 20 and an amount of 1. 
- For actions that involve some level of deeper knowledge & intimacy (like spending a night together) use a cap of 50.
- For actions specifically intended to increase knowledge use a cap of 60. 
- Amounts should not exceed 5, and that only for fairly significant actions: snooping in his phone while he's in the shower is (5,60).
- Really high caps above should usually be avoided. 
- One purpose behind the knowledge system is to limit how well a PC can know her partners by their relationship level. Ideally getting all the way up to the max of 100 would only happen after marriage, meaning some hidden traits might still surprise her after they've tied the knot.


#### removeTrait(String): void

Removes the trait defined by the input parameter, which *must* be a *valid* NPC trait. 

**NOTES:**
- Does nothing if the NPC doesn't have the trait.
- Some traits are used for start-of-game setup and removing them may not have the expected effects. For example, removing the `MISANTHROPE` trait will *not* change the character's cap on NPC liking.

#### setContactable(): void

Sets the NPC as contactable.

**NOTES:**
- This is like swapping phone numbers with the PC.
- This will let them start asking her out on dates. Mostly just relevant for male NPCs.

#### setUnContactable(): void

Sets the NPC as un-contactable.

**NOTES:**
- Use this if your scene involves them deleting her number.
- This will stop the NPC from asking the PC out.

#### setPcBehaviour(String): void

Sets the PC's behaviour towards this NPC to the behaviour matching the parameter, which *must* be a *valid* behaviour.

**NOTES:**
- See the enum reference for the list of behaviours.
- Note that PC behaviours are *not* the same as NPC ones and use a different enum.
- It will usually be best to let the player choose a behaviour instead of directly setting it yourself (*see the YAML guide on how to access the behaviour-choice methods*).

#### clearCheating(): void

Clears all cheating history for this NPC.

**NOTES:**
- This should be called when the PC's partner discovers her cheating to stop her getting found out twice for the same thing.
- The cheating confrontation scene already calls this so you only need to call the method yourself on paths that don't transition to that one.

### Text Getters

#### getAgeDesc(): String

Gets a short piece of text describing the NPC's age.

**Example:** `man in his forties`

**NOTES:**
- Typically used when introducing characters to build up sentences like "He's a white man in his forties with brown hair and blue eyes".

#### getRelationshipNpcDesc(): String

Returns a short description of the NPC's role in the relationship.

**Example:** `boyfriend`

**NOTES:**
- See the Relationship Status enum reference for details.
- This is generally used when the NPC is the PC's partner.

**RELATIONSHIPS:**
| Status | Description | Notes |
| ------ | ----------- | ----- |
| `STRANGER` | Starting level. | Automatically moves to `ACQUAINTANCE` when *knowledge* reaches a certain level. |
| `ACQUAINTANCE` | At this level NPCs will appear in the *NPC Browser*. | | 
| `DATE` | Set when the PC goes out with an NPC. | | 
| `COUPLE` | Boyfriend/girlfriend. Counts as being the PC's partner. | | 
| `ENGAGED` | Engaged to be married. |  |
| `MARRIED` | The PC is married to this NPC. | Implemented in 0.4.16 |


#### getRelationshipWDesc(): String

Returns a short description of the PC's role in the relationship.

**NOTES:**
- See the Relationship Status enum reference for details.
- Equivalent to `getRelationshipNpcDesc`.

**Example:** `girlfriend`

**RELATIONSHIPS:**
| Status | Description | Notes |
| ------ | ----------- | ----- |
| `STRANGER` | Starting level. | Automatically moves to `ACQUAINTANCE` when *knowledge* reaches a certain level. |
| `ACQUAINTANCE` | At this level NPCs will appear in the *NPC Browser*. | | 
| `DATE` | Set when the PC goes out with an NPC. | | 
| `COUPLE` | Boyfriend/girlfriend. Counts as being the PC's partner. | | 
| `ENGAGED` | Engaged to be married. |  |
| `MARRIED` | The PC is married to this NPC. | Implemented in 0.4.16 |

### Pronoun Getters

These return a simple lowercase string for the NPC's pronoun.

#### getHeShe(): String

Returns "he" for male NPCs and "she" for female ones.

#### getHimHer(): String

Returns "him" for male NPCs and "her" for female ones.

#### getHisHer(): String

Returns "his" for male NPCs and "her" for female ones.

#### getHisHers(): String

Returns "his" for male NPCs and "hers" for female ones.

## Condition methods

### Relationship facets

The PC has a relationship with each NPC consisting of three bi-directional facets: *Liking*, *Love* and *Attraction*. 
The methods are separated into NPC and PC ("`W`") sections.

**NOTES:**
- Attraction is handled separately in `MaleNpc` because lesbian content isn't broadly implemented in Newlife.
- These get that person's love/liking for the other one. This is not necessarily the same: it's possible the NPC really likes the PC but the PC despises them. Or vice-versa.
- You can often guess the reasons based on traits (e.g. using "bore" if he has the dull trait or "bastard" otherwise) but there isn't a way of knowing for certain.
- All of these methods will return `true` if the relationship facet is at the relevant level *or higher*.

**DEVELOPER TIPS:**
- Bear in mind that you won't know from these *why* the values are what they are.
- It's often better to use NPC Behaviour to check how they'll act towards the PC rather than checking like/love directly, but there are some situations where it might still be beneficial to do so.
- It's important to check either behaviour or love & liking first if you want one character to be horrid to another.
- It is important to note that dislike-level *liking* could mean that an NPC is `DULL` and the PC find them annoying to spend time with, or that they're an asshole who's done bad things to her, or just that they have a personality clash and don't get on. 

**Example:** `isWLikingLike` will return `true` if the PC's liking for the NPC is at `LIKE` or `CLOSE` levels, whereas `isWLikingClose` will only return `true` at `CLOSE`.

#### Like

Liking determines how much one character likes another. 

**NOTES:**
- This is capped (at "`OK`" level) for `MISANTHROPE` trait characters. 
- The lowest level is "disliked" and can be checked with `isWLikingNeutral` and `isNpcLikingNeutral`: if this returns `false` then that person dislikes the other one.

**LEVELS:**

| Level | Description | Notes |
| ----- | ----------- | ----- |
| Disliked | The character dislikes the other and may treat them badly. | This will depend on personality (use behaviour to check this). This may be useful for text where e.g. the PC feels bad about sleeping with an NPC not because they aren't attractive but because she dislikes them as a person. |
| Neutral | The character is neutral towards the other | |
| Ok | The character thinks the other is an ok person. | |
| Like | The character properly likes the other. | This is the most common threshold for "good relationship" checks. |
| Close | The character feels close to the other one. | The highest level of liking, this often has special content where e.g. even a jerk will help the PC out because she's someone they like so much. |

#### Love

Love increases based on how much a character loves the other and cannot go negative: the lowest value is zero for "no love at all".

**NOTES:**
- `AROMANTIC` PCs and `COLD_HEARTED` NPCs *cannot* increase love above **zero**.
- Love will only increase if a total based on *attraction* & *liking* reaches a certain threshold.
- The threshold where love begins *varies* based on traits & personality.
- It's possible (though rare) for love to be high even if a character dislikes the other. This can be worth writing special text for.

**LEVELS:**

| Level | Description | Notes |
| ----- | ----------- | ----- |
| None | The character feels no love towards the other one. | Check `isNpcLoveSome`/`isWLoveSome` for this: if it returns false then the love
level is None. |
| Some | The character has some fondness for the other, but not enough for it to be a big deal.|  Romantic characters/NPCs may need special content for this. For instance they adore big romantic gestures from anyone they have even small feelings towards, but might feel it's too much if they feel no love whatsoever. |
| Confused | The character is beginning to fall for the other person but they maybe haven't really accepted it yet, so their feelings are confused on the matter. | |
| Crush | The character has a crush on the other person. | This is usually the level to check for love-based text. |
| Love | The character is deeply in love with the other person. | This is the level to check for very dramatic romantic actions such as proposing marriage. | 

#### isNpcLikingClose(): boolean

#### isNpcLikingLike(): boolean

#### isNpcLikingOk(): boolean

#### isNpcLikingNeutral(): boolean

#### isNpcLoveLove(): boolean

#### isNpcLoveCrush(): boolean

#### isNpcLoveConfused(): boolean

#### isNpcLoveSome(): boolean

#### isWLikingClose(): boolean

#### isWLikingLike(): boolean

#### isWLikingOk(): boolean

#### isWLikingNeutral(): boolean

#### isWLoveLove(): boolean

#### isWLoveCrush(): boolean

#### isWLoveConfused(): boolean

#### isWLoveSome(): boolean

### Attraction

These methods check attraction from the NPC to the player or from the player to the NPC.

**NOTES:**
- This is the *modified* attraction value including effects from clothing, alcohol etc.
- The methods will return `true` if the value is *above* the relevant threshold, even if it falls into a higher category.
- An NPC with attraction below the level of "Ok" should *not* try to sleep with the PC.


**LEVELS:**

| Level | Description | Notes |
| ----- | ----------- | ----- |
| Disgust | The lowest category. | The character is disgusted by the thought of being intimate with the other person. |
| Unattracted | The character is not attracted and doesn't want to sleep with the other person. | |
| Ok | The character thinks the other person is OK to look at. | Nothing to be especially excited about, but "good enough" to sleep with. |
| Attracted | The character is strongly attracted to the other person. | |
| Lust | The character finds the other person extraordinarily sexy. | |


#### isNpcAttractionUnattracted(): boolean

#### isNpcAttractionOk(): boolean

#### isNpcAttractionAttracted(): boolean

#### isNpcAttractionLust(): boolean

#### isWAttractionUnattracted(): boolean

#### isWAttractionOk(): boolean

#### isWAttractionAttracted(): boolean

#### isWAttractionLust(): boolean

### Willpower

See the player-character section on willpower for discussion of how it works.

**NOTES:**
- These willpower methods include default modifiers based on the PC's relationship with this NPC.
- They should be used when the willpower test is being caused by an NPC, which is most of the time.
- The levels and usage is otherwise the *same* as the player-character ones.

#### testWillEasy(int modifier): boolean

#### testWillNormal(int modifier): boolean

#### testWillHard(int modifier): boolean

#### testWillVeryHard(int modifier): boolean

### Other condition methods

#### getHadSex(): boolean

Returns `true` if this NPC has had penetrative (PIV) sex with the player-character.

#### getHadAnalSex(): boolean

Returns `true` if this NPC has had anal sex with the player-character.

#### getBehaviour(): String

Returns the NPC's behaviour, allowing faking.

**NOTES:**
- See the enum reference for more information on NPC behaviour.

#### getBehaviourNoFaking(): String

Returns the NPC's behaviour with faking disallowed.

**NOTES:**
- See the enum reference for more information on NPC behaviour.

#### getPcBehaviour(): String

Returns the PC's behaviour to this NPC, or null if no behaviour has been set.

**NOTES:**
- PC behaviours are *not* the same as NPC behaviours. See the enum guide for details.

#### getPersonality(): String

Returns the NPC's personality.

#### getHadChild(): boolean

Returns `true` if this NPC and the PC have a child together.

#### getRelationship(): String

Gets the relationship status between this NPC and the PC.

**RELATIONSHIPS:**
| Status | Description | Notes |
| ------ | ----------- | ----- |
| `STRANGER` | Starting level. | Automatically moves to `ACQUAINTANCE` when *knowledge* reaches a certain level. |
| `ACQUAINTANCE` | At this level NPCs will appear in the *NPC Browser*. | | 
| `DATE` | Set when the PC goes out with an NPC. | | 
| `COUPLE` | Boyfriend/girlfriend. Counts as being the PC's partner. | | 
| `ENGAGED` | Engaged to be married. |  |
| `MARRIED` | The PC is married to this NPC. | Implemented in 0.4.16 |

#### getWasFirstAnalLover(): boolean

Returns `true` if the PC lost her anal virginity to this NPC.

#### getWasFirstLover(): boolean

Returns `true` if the PC lost her virginity to this NPC.

#### hasActiveVow(String): boolean

Returns `true` if the NPC has the specified *Vow* active with the PC.

**NOTES:**
- This will only ever be true with the PC's partner, and only at `ENGAGED` or `MARRIED` relationship status.
- If you're writing a general scene that allow any NPC then you should ensure your action conditions and written text takes possible vows into consideration.

#### hasTrait(String): boolean

Returns `true` if the NPC has the specified trait.

**NOTES:**
- See the enum reference for details.
- Male and Female NPCs technically use the same enum types for traits and there are some traits that are available to both.
- Gender-restricted traits will never appear on wrong-gender NPCs, but you won't get an error if you check something like `hasTrait("THICK_COCK")` on a female NPC, it will just return `false`.
- You'll find that most of your writing will need to consider some trait or other on either the PC or the NPC so this is a method you'll doubtless end up using a lot unless you're writing content where the PC is alone.

#### hasRelationshipFlag(String): boolean

Returns `true` if the PC's relationship with this NPC has the specified relationship flag.

**NOTES:** 
- See the enum reference for details.
- Relationship flags are used to track certain statuses that apply to the relationship. This has some overlap with NPC traits which are used the same way in some older scenes.
- You can add relationship flags using the `addRelationshipFlag `method, and there's a test flag to use as a placeholder.

**DEVELOPER'S NOTES:**
Because relationships are always between the PC and a single NPC, there isn't much practical difference between relationship flags and NPC traits, except that relationship flags can't get a line in the character browser.
It was probably bad design for me to include both, but that's in the code now and I don't see much to gain in refactoring it now.


#### isContactable(): boolean

Returns `true` if the NPC and PC have swapped phone numbers. 

**NOTES:**
- This allows male NPCs to ask the PC out on dates.

**DEVELOPER TIPS:**
- You should check this as a condition for actions where he asks for her number as it wouldn't make sense if he already has it.

#### isFriend(): boolean

Returns `true` if the NPC is one of the PC's friends.

**NOTES:**
- This will *not* return `true` if they're her partner.
- This does *not* mean they actually like each other, but you can assume that being a 'friend' means they're in regular contact.

#### isCohabiting(): boolean

Returns `true` if this NPC is cohabiting with the PC.

**NOTES:**
- The PC can only cohabit with one NPC.

**DEVELOPER'S NOTES:**
- In the current version this will return `true` if they are married and false otherwise. I do not have plans to change this but I've added this method as separate from checking for marriage just in case my plans change in the future.
- You should not put much effort into writing content that can only appear if the PC is cohabiting with someone not her husband: it's likely that it will never be able to appear in-game.

#### isPartner(): boolean

Returns` true` if this NPC is the PC's partner.

**NOTES:**
- Relationship status must be `COUPLE`, `ENGAGED` or `MARRIED`.
- The PC can only have one partner at a time.

#### isTryingForBaby(): boolean

Returns `true` if this NPC and the PC are trying for a baby.

**NOTES:**
- This doesn't refer to sneaky fertilisation attempts by impregnators but rather for situations where they've mutually agreed to have a child.

**DEVELOPER'S NOTES:**
- This hasn't been fully implemented in the game yet, but it's due in the nearish future so it's a good idea to consider it in your writing.

#### isBelievesVirgin(): boolean

Returns `true` if the NPC *believes* the PC is a virgin.

**NOTES:**
- It may not agree with her actual virgin status.
- Use this for NPC dialogue that references the PC's virginity.

#### getLikesPlayersBreasts(): boolean

Returns `true` if the NPC especially likes the PC's breasts. 

**NOTES:**
- This essentially compares the breast-size preference trait with the PC's breasts. 

**DEVELOPER'S NOTES:**
- It's possible for them to neither especially like nor dislike them so check `getDislikesPlayersBreasts` as well when writing for these.
- This method should be used for things like text where the NPC is admiring or complimenting the PC, especially if she's wearing a low-cut top.

#### getDislikesPlayersBreasts(): boolean

Returns `true` if the NPC dislikes the PC's breasts for being the wrong size. 

**DEVELOPER'S NOTES:**
- This is *not* the opposite of `getLikesPlayersBreasts`, as it's possible for *both* to return `false` if they have no strong opinion.

#### getLikesBreasts(ContextFemaleNpc): boolean

Returns `true` if the NPC likes the female NPC's breasts.

#### getDislikesBreasts(ContextFemaleNpc): boolean

Returns `true` if the NPC dislikes the female NPC's breasts.

#### hasDoneSexualActivity(String activity): boolean

Returns `true `if the PC has performed the sexual act at some point with this NPC. 

**NOTES:**
- See the enum guide for a list of valid sexual activities. 
- This has some overlap with methods like `getHadSex` – use whichever is most convenient.
- These values are never removed, so you can be confident that if the method returns `false` for kissing then the PC has never kissed this NPC, at least not unless there's a bug somewhere with the value being set.
- The method can't tell you how recently this happened though, or how often, or in which context. It's usually ok to make reasonable assumptions though.
- Entering a value not in the list of valid sexual activites will result in an error.

**DEVELOPER'S NOTES:**
- You could have an NPC say that he loves the PC's tight pussy if she has the snug pussy trait and they've had sex.  It's possible that this sexual encounter was actually quite un-enjoyable for the NPC, but the line is still acceptable even if there's some rare situations where it technically isn't accurate.


#### hasDoneCheatingActivity(String activity): boolean

Returns `true `if the PC has performed the sexual act at some point with this NPC, but only applies if the activity was done when the PC was *cheating* on her *current* partner. 

**NOTES:**
- See the enum guide for a list of valid sexual activities. 
- Entering a value not in the list of valid sexual activites will result in an error.
- Cheating activities are cleared if the partner finds out, and will also expire after a certain amount of time.


#### getCheatedWith(): boolean

Returns `true` if the PC has *cheated* on her *current* partner with this NPC **and** the cheating is still undiscovered and has not been removed due to time passing.

**NOTES:**
- Use caution with this method because the cheating could be due to a low-severity activity like kissing.  See `getCheatingSeverity`  as well.


#### getCheatingSeverity(): String

Returns the severity of the *highest* level active cheating with this NPC on the PC's current partner. 

**CHEATING SEVERITY LEVELS:**
| Level | Description | Notes |
| ----- | ----------- | ----- |
| `NONE` | | |
| `LIGHT` | | |
| `MODERATE` | | |
| `SEVERE` | | |

**NOTES:**
- Cheating that's been discovered or which has timed-out will *not* be counted.
- This will always return `NONE` if `hasCheatedWith()` returns `false`, and one of the other values if it's true.

----
# Female NPCs

These apply to female NPCs *only*.

## Actions

### Clothing status

These methods modify one or more clothing slot's status. 

**NOTES:**
- For more information on clothing statuses see the enum reference. This also lists allowable values.

**DEVELOPER TIPS:**
- These methods should be used when the NPC dresses or undresses, but also if her clothes become disheveled.  This is far less common for Female NPCs than for the PC, but can still happen on occasion.
- Also see the Character [fixClothing](Context-Objects#fixclothing-void) and [stripNaked](Context-Objects#stripnaked-void) methods which remove or put on all of the character's clothing.

**WARNING:**
- Be careful about setting clothing status directly. If an outfit did not include, say, a bra but you call [setBraStatus("WORN")](Context-Objects#setbrastatusstring-status-void) then they'll be described as wearing a "braless" and descriptive text will get muddled indeed. As a rule of thumb it's fine to *un*dress a character, but it's safest to use [fixClothing](Context-Objects#fixclothing-void) if you need to put clothes back on.

**Clothing Status Types:**
| Enum | Description | Notes |
| ---- | ----------- | ----- |
| `WORN` | The clothing item is being worn as intended. | |
| `DISHEVELED` | Generally set after the NPC gets groped.  | *Not applicable for legwear.*  It has little in the way of gameplay effect but modifies her description. Disheveled clothing still covers whatever it was supposed to cover. |
| `EXPOSED` | The clothing has been moved aside. | *Not applicable for legwear.*  The exact description of how depends on the clothing item) and no longer covers whatever it was meant to cover. |
| `OFF` | The clothing slot is empty. | The outfit has no clothing for it or because the clothing has been removed completely. |

**NOTES:**
- `DISHEVELED` is spelt with one "l", which is the US-English spelling. Using the "dishevelled" spelling will result in an error.

#### putOnLegwear(): void

Sets the character's legwear to `WORN`.

#### removeLegwear(): void

Sets the character's legwear to `OFF`.

#### setBottomStatus(String status): void

Sets lower-body clothing to the supplied status.

**NOTES:**
- For dresses and other items that cover multiple slots, setting status in any one slot to `OFF` will remove them from *both* slots.
- For dresses and other items that cover multiple slots, setting status to `EXPOSED` or `DISHEVELED` will *not* affect the other slot.
- Please note that you can have a dress that's been pulled up (lower body status `EXPOSED`) but still covers her breasts properly (upper body status `WORN`).

#### setBraStatus(String status): void

Sets bra clothing to the supplied status.

#### setPantiesStatus(String status): void

Sets panties to the supplied status.

#### setTopStatus(String status): void

Sets upper-body clothing to the supplied status.

#### stripExceptLegwear(): void

Like [stripNaked](Context-Objects#stripnaked-void) but will not remove any `WORN` legwear.

### Other Actions

#### haveSexWith(ContextMaleNpc): void

Sets the character's virginity to `false`. 

**DEVELOPER'S NOTES:**
The male NPC parameter is not actually used in the current version but it's there for potential future-proofing.
I don't want to break people's scenes by adding a simple `loseVirginity` method that'd need to be removed if NPC-NPC intercourse gets some more in-depth implementation.


#### performMakeoutAction(String pcResponse, Collection<String> moTypes, String npcPosition, String position, boolean allowBehaviourFaking, boolean canCountAsCheating, String dominant) : String

Performs a makeout action by the NPC. 

Makeout actions are how Newlife lets NPC actions be written for one scene (like a makeout) but then re-used when appropriate in 
others, such as the pervy client groping the PC in her office. While these were originally written to support the makeout scenes
they can be used in many other places.

However, this method only covers actions initiated by the NPC.  Player-actions have no equivalent and need to be written scene-by-scene.

Another limitation of using standard actions is that they obviously can't be specific to a particular scene. 
If there's something about your scene that requires different text output from normal then you'll need to write your own makeout 
content.

***How it works:***
Calling this method will use some standard logic to pick an appropriate action given the input parameters and run it, performing any changes like clothing removal or arousal modification and returning the action's text as a short paragraph.

The action type that gets run will be chosen from the supplied list using a weighted-random method. Even with only one allowable type the output may vary between calls. Internally there are several makeout actions for each type, each with their own conditions, and if more than one's conditions are met then one will be chosen at random.

The actions should cover the full range of situations that exist in the game at present. There are some combinations that are not in the game, notably some of the `SITTING` ones. These usually do not have actions defined for them (except where sitting content was written for the porn-movie scene).


**DEVELOPER'S NOTES:**
- The call for male PC's is very simliar but has an additional boolean `rough` (`performMakeoutAction(String pcResponse, Collection<String> moTypes, String npcPosition, String position, boolean rough, boolean allowBehaviourFaking, boolean canCountAsCheating) : String`)
- The concert scene uses custom NPC actions because I wanted them to reference the player being in the middle of a big crowd of people.
- The default makeout actions cannot be modified in the test structure. You can submit a new one if you have an idea for something that's sufficiently different to the existing actions but that will still work in the various situations the method gets called from. There isn't a formal way of doing this though, so such a submission would have to be written in freeform text for me to modify into Java code. 
- While many makeout actions have quite general conditions the system does support very specific ones, so if you have a great idea for a kissing sequence that only works if the NPC is, say, a paunchy, sleazy jerk and the pc is a slim heavily-pregnant bitchy woman with high stress then you can go ahead and suggest away.
- Because lesbian content is newer than the MF scenes there is less content within the makeout actions and you may find limited options for position/npcPosition combinations that do not occur in the main game.
- Please let me know if you see a makeout action returned whose text is jarringly inappropriate for the parameters.


Most of the parameters are enum values and **will** throw an error if the input do not *exactly* match a valid value, *including case*.

| Parameter | Type | Description | Values |
| --------- | ---- | ----------- | ------ | 
| pcResponse | ENUM | This determines how the PC will react to the NPC's attempt to get intimate with her. | `WELCOME`, `ACCEPT`, `REJECT` |
| moTypes | ENUM | Makeout types are a collection of values which must have *at least* one entry. | `KISS`, `TOUCH`, `GROPE`, `GRIND`, `UNDRESS`, `READY_SEX`, `KISS_BODY` |
| npcPositions | ENUM | The NPC's position relative to the PC.  | `BEHIND`, `FACE_TO_FACE`, `SIDE` |
| position | ENUM | The position of the PC and NPC. | `STANDING`, `LYING`, `SITTING` |
| allowBehaviourFaking | boolean | Whether to allow the NPC to 'fake' their behaviour when it's checked as part of handling an event. | |
| canCountAsCheating | boolean | This method will automatically record any SexualActivity as *cheating* if set to `true`. | | 
| dominant | ENUM | This determines who is taking the more active role in initiating the makeout. | `PC_DOMINANT`, `NPC_DOMINANT`, `NEITHER_DOMINANT` |

**NOTES:**
- **pcResponse:**. Scenes that include player-behaviour should usually use that to get the response,  although player-behaviour hasn't yet been exposed for player-submission content at the time of writing. 
- **pcResponse:**. The actual makeout scenes use a perhaps over-simplistic method of having `WELCOME` for arousal comfort level or higher and `ACCEPT` otherwise. The assumption there is that if the PC *wanted* to reject the NPC making out with her then she'd exit the makeout scene outright.
- **moTypes:** This defines which type of makeout action will be available. The weighting between types varies based on traits, arousal, alcohol and so on. This can be varied within a scene.
- **moTypes:** `TOUCH` and `GROPE` are similar but touch is a 'lighter' caress.
- **moTypes:** `UNDRESS` handles removing clothes from her upper body.
- **moTypes:** `READY_SEX` refers to undressing the PC in ways that are necessary for penetration, such as removing her panties, pulling up her skirt and so on.
- **position:** Some combinations of position & npcPosition have limited or specific content.
- **position:** `SIDE` is only valid when sitting.
- **position:** `LYING` and `FACE_TO_FACE` is for the final stage of the sofa-makeout with the PC lying face-down. It could be used for a similar position elsewhere, but not for on-all-fours positions.
- **position:** `SITTING` and `FACE_TO_FACE` is **not implemented**.
- **canCountAsCheating:** This will *not* count as cheating if the PC's response is `REJECT`.
- **canCountAsCheating:** If your scene is a sub-scene then you should check if the parent has set the `NOT_CHEATING` flag. 
- **canCountAsCheating:** You should set cheating to `false` for situations the PC has no control over where she isn't welcoming the action.

**Examples:**
- **moTypes:** Encouraging the pervy client adds the `GROPE` type to the options as well as making him take actions more often. The full makeout scenes use all of these.
- **canCountAsCheating:** It shouldn't count as cheating when the pervy client gropes the pc unless she's encouraged him.

**Makeout Types:**
| Value | Description | Notes |
| ----- | ----------- | ----- |
| `KISS` | Kissing | |
| `TOUCH` | Light caresses. | |
| `GROPE` | Full on groping. | |
| `GRIND` | | |
| `UNDRESS` | Removing clothes from the PC's upper body. | |
| `READY_SEX` | Undressing the PC for penetration. | |
| `KISS_BODY` | Kissing the PC's breasts or stomach. | |

#### setOnPill(boolean): void

Puts the NPC on or off the pill, as appropriate.

**NOTES:**
- Impregnations are calculated at the end of the week so calling `setOnPill(false)` means she can get pregnant from sex that same week even if it was in an earlier scene.

### Text Getters

#### getBreastsDesc(): String

Returns a string describing the NPC's breasts. 

**NOTES:**
- String is lowercase with no preceding or trailing spaces.
- See the enum section on Breasts for the descriptions of each breast-size.
- Size will increase by one level in the late stages of pregnancy, returning to normal after birth.
- PC has this [method](Context-Objects#getbreastsdesc-string) as well.

**Example:** `full breasts`.

#### getStomachDesc(): String

Returns a short phrase describing the NPC's stomach. 

**NOTES:**
- Identical to the PC's method of the same name.

**Example:** `heavily pregnant belly`

#### getGirlOrWoman(): String

Returns either `girl` or `woman`.   It will return "girl" if the NPC's age category is `LATE_TEENS` or `EARLY_TWENTIES`, or if it's `TWENTIES` and she has the `INNOCENT` character type.

**NOTES:**
- Be careful when writing adjectives preceding this method call. In particular "young woman" has a very different meaning to "young girl"!
- This method therefore won't fit every sentence, and sometimes it'll be better to just write out your own logic.
- Identical to the PC's method of the same name.

## Condition methods

### Clothing conditions & getters

**Clothing Status Types:**
| Enum | Description | Notes |
| ---- | ----------- | ----- |
| `WORN` | The clothing item is being worn as intended. | |
| `DISHEVELED` | Generally set after the NPC gets groped.  | *Not applicable for legwear.*  It has little in the way of gameplay effect but modifies her description. Disheveled clothing still covers whatever it was supposed to cover. |
| `EXPOSED` | The clothing has been moved aside. | *Not applicable for legwear.*  The exact description of how depends on the clothing item) and no longer covers whatever it was meant to cover. |
| `OFF` | The clothing slot is empty. | The outfit has no clothing for it or because the clothing has been removed completely. |

**NOTES:**
- `DISHEVELED` is spelt with one "l", which is the US-English spelling. Using the "dishevelled" spelling will result in an error.

#### getBra(): ClothingItem

Returns the NPC's bra clothing item object. 

**NOTES:**
- You should check `getBraStatus()` first to make sure that she's actually wearing one.
- See the clothing condition methods for more information about this object type.
- Identical to the PC's method of the same name.

#### getBottom(): Lower Body Clothing

Returns the NPC's lower body clothing. 

**NOTES:**
- You should check `getBottomStatus()` first to make sure that she's actually wearing some.
- See the clothing condition methods for more information about this object type.
- Identical to the PC's method of the same name.

#### getTop(): Upper Body Clothing

Returns the NPC's upper-body clothing. 

**NOTES:**
- You should check `getTopStatus()` first to make sure that she's actually wearing some.
- See the clothing condition methods for more information about this object type.
- Identical to the PC's method of the same name.

#### getLegwear(): Legwear

Returns the NPC's legwear. 

**NOTES:**
- You should check `isLegwearWorn()` first to make sure that she's actually wearing some.
- See the clothing condition methods for more information about this object type.
- Identical to the PC's method of the same name.

#### getPanties(): ClothingItem

Returns the NPC's panties clothing item object. 

**NOTES:**
- You should check `getPantiesStatus()` first to make sure that she's actually wearing some.
- See the clothing condition methods for more information about this object type.
- Identical to the PC's method of the same name.

#### getBottomStatus(): String

Returns the lower-body clothing status.

**NOTES:**
- Identical to the PC's method of the same name.

#### getBraStatus(): String

Returns the bra clothing status. 

**NOTES:**
- Identical to the PC's method of the same name.

#### getPantiesStatus(): String

Returns the panties clothing status.

**NOTES:**
- Identical to the PC's method of the same name.

#### getTopStatus(): String

Returns the upper-body clothing status. 

**NOTES:**
- Identical to the PC's method of the same name.

#### isLegwearWorn(): boolean

Returns `true` if the legwear status is `WORN`. Otherwise, it indicates that the legwear is `OFF` as the other two statuses are not available for legwear.

**NOTES:**
- Identical to the PC's method of the same name.

#### isPussyExposed(): boolean

Returns `true` if the NPC's pussy is exposed allowing her to be penetrated, touched or whatever. 

**NOTES:**
- This checks clothing statuses and the length of her lower-body clothing if it's a skirt. 
- Typically you'd use this in your writing rather than checking bottom and panties statuses.
- Identical to the PC's method of the same name.

#### isBreastsExposed(): boolean

Returns `true` if the NPC's breasts are uncovered.

**NOTES:**
- Identical to the PC's method of the same name.

#### isStomachExposed(): boolean

Returns `true` if the NPC's stomach is bare, either due to her top being `OFF` or `EXPOSED` or due to it having the `SHOWS_TUMMY` flag.

**NOTES:**
- Identical to the PC's method of the same name.

#### isClothesDisarrayed(): boolean

Returns `true` if *any* of the NPC's outfit has been disarrayed in any way.

**NOTES:**
- If any item has a clothing status other than `WORN` or, in the case of clothing slots where the outfit has no clothing item, `OFF`.
- Identical to the PC's method of the same name.

#### isNakedExceptLegwear(): boolean

Returns `true` if the character is completely naked *or* if she's only wearing legwear.

**NOTES:**
- Identical to the PC's method of the same name.

### Other condition methods

#### getBreasts(): String

Returns the NPC's breast size as a string enum. 

**BREAST TYPES:**
| ENUM | Scope | Description | Notes |
| :--- | :---- | :---------- | :---- |
| `SMALL` | PC/NPCs | small but perky tits | |
| `MEDIUM_SMALL` | PC/NPCs | pert tits | |
| `MEDIUM_LARGE` | PC/NPCs| full breasts | |
| `LARGE` | PC/NPCs | heavy breasts | |

**NOTES:**
- This isn't suitable to be inserted into text shown to the player, use `getBreastsDesc` for that. See the enum reference for possible values.
- Identical to the PC's method of the same name.


#### getCharType(): String

Returns the NPC's character type. 

**FEMALE NPC CHARACTER TYPES:**
| Type | Description | Notes |
| ---- | ----------- | ----- |
| `PARTY_GIRL` |  Party-girls love drinking and having fun. |  |
| `INNOCENT` | The stereotypical sweet & innocent character. | |
| `SOPHISTICATED` | A sophisticated NPC is a confident woman. | | 

*See the enum guide for more details.*

**NOTES:**
- This is very important for female NPCs and will almost always need to be considered when writing for them unless your scene's specifically restricted to just one character type. See the enum reference for details.


#### getFigure(): String

Returns the NPC's figure as an enum string value.

**FEMALE FIGURE TYPES:**
| Enum | Description | Notes |
| ---- | ----------- | ----- |
| `SLIM` | A slender and delicate figure.  | Initially the weakest figure but this can change if the PC trains fitness so should not be assumed. |
| `TONED` | A healthy fit physique, slim with lean muscles. |  |
| `WOMANLY` | An hourglass body with pronounced feminine curves. | This one can be a bit tricky to write for as words like "curvy" are often used for "BBW" body-types. I tend to use "curvaceous" or "hourglass" instead. |

**NOTES:**
- Identical to the PC's method of the same name.

#### isBreastsLargerThanPc(): boolean

Returns `true` if the NPC has larger breasts than the PC.

**NOTES:**
- Returns `false` for the same-size or smaller

#### isBreastsSmallerThanPc(): boolean

Returns `true` if the NPC has smaller breasts than the PC. 

**NOTES:**
- Returns `false` for the same-size or larger


#### isVirgin(): boolean

Returns `true` if the character is a virgin. 

#### isPregnant(): boolean

Returns `true` if the character is pregnant.

#### getPregnancyStage(): String

Returns the character's pregnancy stage.

**PREGNANCY STAGES:**
| Stage | Description | Notes |
| ----- | ----------- | ----- |
| `FLAT` | Flat stomach | Either she isn't pregnant or she's in the first trimester. |
| `BUMP` | Small baby bump | Second trimester. |
| `BIG` | Pregnant belly | First half of the third trimester. |
| `HUGE` | Heavily pregnant belly | Second half of the third trimester. |

**NOTES:**
- Identical to the PC method of the same name.


#### isLatePreg(): boolean

Returns `true `if the character is in the third trimester of pregnancy. (Pregnancy Stage is `BIG` or `HUGE`).

#### isLactating(): boolean

Returns `true` if the character is lactating.

**NOTES:**
- Lactation is something which may be worth mentioning in descriptions or in text based around her breasts.
- You shouldn't make assumptions about pregnancy from this trait. It's possible to not be lactating despite being heavily pregnant (if lactation is disabled in the game options) and it's possible to be lactating despite never having been pregnant due to the milky trait.
- Identical to the PC [method](Context-Objects#islactating-boolean) of the same name.

#### isMum(): boolean

Returns `true` if the character has given birth at least once.

**NOTES:**
- Identical to the PC method of the same name.

#### getBabies(): Collection `<Baby>`

Returns a collection of Baby objects which may be empty but will not be null.

**NOTES:**
- Identical to the PC method of the same name.

----
# Male NPCs

## Actions

#### performMakeoutAction(String pcResponse, Collection&lt;String&gt; moTypes, String npcPosition, String position, boolean rough, boolean allowBehaviourFaking, boolean canCountAsCheating) : String

Performs a makeout action by the NPC. 

Makeout actions are how Newlife lets NPC actions be written for one scene (like a makeout) but then re-used when appropriate in 
others, such as the pervy client groping the PC in her office. While these were originally written to support the makeout scenes
they can be used in many other places.

However, this method only covers actions initiated by the NPC.  Player-actions have no equivalent and need to be written scene-by-scene.

Another limitation of using standard actions is that they obviously can't be specific to a particular scene. 
If there's something about your scene that requires different text output from normal then you'll need to write your own makeout 
content.

***How it works:***
Calling this method will use some standard logic to pick an appropriate action given the input parameters and run it, performing any changes like clothing removal or arousal modification and returning the action's text as a short paragraph.

The action type that gets run will be chosen from the supplied list using a weighted-random method. Even with only one allowable type the output may vary between calls. Internally there are several makeout actions for each type, each with their own conditions, and if more than one's conditions are met then one will be chosen at random.

The actions should cover the full range of situations that exist in the game at present. There are some combinations that are not in the game, notably some of the `SITTING` ones. These usually do not have actions defined for them (except where sitting content was written for the porn-movie scene).


**DEVELOPER'S NOTES:**
- The call for female PC's is very simliar but does not have the additional boolean `rough` (`performMakeoutAction(String pcResponse, Collection<String> moTypes, String npcPosition, String position, boolean allowBehaviourFaking, boolean canCountAsCheating) : String`)
- The concert scene uses custom NPC actions because I wanted them to reference the player being in the middle of a big crowd of people.
- The default makeout actions cannot be modified in the test structure. You can submit a new one if you have an idea for something that's sufficiently different to the existing actions but that will still work in the various situations the method gets called from. There isn't a formal way of doing this though, so such a submission would have to be written in freeform text for me to modify into Java code. 
- While many makeout actions have quite general conditions the system does support very specific ones, so if you have a great idea for a kissing sequence that only works if the NPC is, say, a paunchy, sleazy jerk and the pc is a slim heavily-pregnant bitchy woman with high stress then you can go ahead and suggest away.


**Parameters**

Most of the parameters are enum values and **will** throw an error if the input do not *exactly* match a valid value, *including case*.

| Parameter | Type | Description | Values |
| --------- | ---- | ----------- | ------ | 
| pcResponse | ENUM | This determines how the PC will react to the NPC's attempt to get intimate with her. | `WELCOME`, `ACCEPT`, `REJECT` |
| moTypes | ENUM | Makeout types are a collection of values which must have *at least* one entry. | `KISS`, `TOUCH`, `GROPE`, `GRIND`, `UNDRESS`, `READY_SEX`, `KISS_BODY` |
| npcPositions | ENUM | The NPC's position relative to the PC.  | `BEHIND`, `FACE_TO_FACE`, `SIDE` |
| position | ENUM | The position of the PC and NPC. | `STANDING`, `LYING`, `SITTING` |
| rough | boolean | Whether the characters are in 'rough mode'. | |
| allowBehaviourFaking | boolean | Whether to allow the NPC to 'fake' their behaviour when it's checked as part of handling an event. | |
| canCountAsCheating | boolean | This method will automatically record any SexualActivity as *cheating* if set to `true`. | | 
| dominant | ENUM | This determines who is taking the more active role in initiating the makeout. | `PC_DOMINANT`, `NPC_DOMINANT`, `NEITHER_DOMINANT` |

**NOTES:**
- **pcResponse:**. Scenes that include player-behaviour should usually use that to get the response,  although player-behaviour hasn't yet been exposed for player-submission content at the time of writing. 
- **pcResponse:**. The actual makeout scenes use a perhaps over-simplistic method of having `WELCOME` for arousal comfort level or higher and `ACCEPT` otherwise. The assumption there is that if the PC *wanted* to reject the NPC making out with her then she'd exit the makeout scene outright.
- **moTypes:** This defines which type of makeout action will be available. The weighting between types varies based on traits, arousal, alcohol and so on. This can be varied within a scene.
- **moTypes:** `TOUCH` and `GROPE` are similar but touch is a 'lighter' caress.
- **moTypes:** `UNDRESS` handles removing clothes from her upper body.
- **moTypes:** `READY_SEX` refers to undressing the PC in ways that are necessary for penetration, such as removing her panties, pulling up her skirt and so on.
- **position:** Some combinations of position & npcPosition have limited or specific content.
- **position:** `SIDE` is only valid when sitting.
- **position:** `LYING` and `FACE_TO_FACE` is for the final stage of the sofa-makeout with the PC lying face-down. It could be used for a similar position elsewhere, but not for on-all-fours positions.
- **position:** `SITTING` and `FACE_TO_FACE` is **not implemented**.
- **canCountAsCheating:** This will *not* count as cheating if the PC's response is `REJECT`.
- **canCountAsCheating:** If your scene is a sub-scene then you should check if the parent has set the `NOT_CHEATING` flag. 
- **canCountAsCheating:** You should set cheating to `false` for situations the PC has no control over where she isn't welcoming the action.

**Examples:**
- **moTypes:** Encouraging the pervy client adds the `GROPE` type to the options as well as making him take actions more often. The full makeout scenes use all of these.
- **canCountAsCheating:** It shouldn't count as cheating when the pervy client gropes the pc unless she's encouraged him.

**Makeout Types:**
| Value | Description | Notes |
| ----- | ----------- | ----- |
| `KISS` | Kissing | |
| `TOUCH` | Light caresses. | |
| `GROPE` | Full on groping. | |
| `GRIND` | | |
| `UNDRESS` | Removing clothes from the PC's upper body. | |
| `READY_SEX` | Undressing the PC for penetration. | |
| `KISS_BODY` | Kissing the PC's breasts or stomach. | |


#### informVirginUntilMarriage(): boolean

Informs this NPC that the PC wants to stay virgin until her marriage.

**NOTES:**
- This will also inform him that she is a virgin and add the `INITIATE_PIV` limitation for the rest of this scene-chain. The limitation is added even if he refuses to respect her wishes.
- The boolean returned shows if he *accepts* her decision. If `false` then the `ACCEPTS_VIRGIN_UNTIL_MARRIAGE` relationship flag will *not* have been set and the NPC may attempt sex with her in future encounters.

#### removeCondom(): void

Sets the character to not be wearing a condom.

**NOTES:**
- Calling this when he already wasn't wearing one will do nothing.

#### wearCondom(): void

Sets the character to be wearing a condom. 

**NOTES:**
- Does not give him a chance to refuse or modify relationship values.
- If the PC is just asking him to wear one use `processCondomRequest` instead.


#### wearCondomWithSabotageChance(): void

Equivalent to `wearCondomWithSabotageChance(false)`, which is the most common use of that method.

#### wearCondomWithSabotageChance(boolean inhibited): void

Sets the NPC to be wearing a condom with no refusal chance and no relationship modifiers. 

**NOTES:**
- Unlike `wearCondom()` it also gives him an opportunity to sabotage it, potentially making it more likely to break.
- The boolean parameter 'inhibited' is whether the NPC should be reluctant to sabotage the condom and should be set to `true` if this is being called because the PC noticed sabotage and is making him replace the condom, or if he otherwise has reason to worry that the PC will be watching out for that sort of thing.

#### condomSabotageOpportunity(boolean inhibited)

Gives the NPC an opportunity to sabotage a condom. 

**NOTES:**
- This won't set him to be wearing one. Use `wearCondomWithSabotageChance` for that. 
- You should check that he's actually wearing one before calling this.
- The boolean parameter 'inhibited' is whether the NPC should be reluctant to sabotage the condom and should be set to `true` if this is being called because the PC noticed sabotage and is making him replace the condom, or if he otherwise has reason to worry that the PC will be watching out for that sort of thing.
- The method will check traits and relationship levels. You don't need to restrict it to impregnators: it'll make the check and won't have non-impregnators attempt sabotage.

**DEVELOPER'S NOTES:**
Typically, an NPC should get two chances for sabotage (assuming he puts on the condom). 
First when he puts it on via `wearCondomWithSabotageChance` and then a second time when sex begins. 

If you're writing a vaginal sex scene (very much not recommended for new writers or indeed for anyone until further methods are exposed for custom scenes!) then you should call this in your scene's intro.
In sex scene intros, you'd typically check for the relevant scene flag `INHIBIT_SABOTAGE`.


#### inseminatePlayer(int modifier, boolean canCountAsCheating): void

Inseminates the player, which may get her pregnant at the end-of-week pregnancy calculations.

**NOTES:**
- The int parameter is an integer modifier to her fertility chance for this specific insemination. For normal sex this should be 0. For less risky situations such as him finishing outside but some of his stuff getting in a dangerous place use a -5 or -10 modifier.
- The boolean parameter controls whether this insemination should be considered cheating if the PC is in a relationship.  It should be set to `false` in situations where the PC is with another man *with her partner's approval*.
- For general sex scenes the boolean should be set based on whether the `NOT_CHEATING` scene flag is set. See the enum reference document for information about scene flags.
- You don't need to check against fertility, contraception, existing pregnancies etc as the pregnancy calculations will do that for you: just call this method whenever he finishes inside her.
- If the PC gets inseminated multiple times in one scene, just make a separate `inseminatePlayer` call each time.
- Call this whenever a situation is unsafe for the player. 

**DEVELOPER'S NOTES:**
- Details of the pregnancy calculations aren't really necessary for writing, but bear in mind that repeated insemination will provide a small increase to her chances of conceiving but not a massive effect.
- Getting inseminated on 5 different weeks is riskier than being inseminated 5 times in 1 week. 


#### inseminatePlayer(int modifier): void

This is the same as calling the above `inseminatePlayer` method with `canCountAsCheating` set to true. 

**NOTES:**
- This is the most common use and should be fine for most scenes.

#### processCondomRequest(boolean StrongRequest):boolean

Requests that the NPC wear a condom. 

**NOTES:**
- This will modify relationship values (e.g. men who hate condoms dislike this) and, if successful, set him to be wearing a condom. 
- This also allows him an opportunity to sabotage the condom when putting it on.
- The input boolean is whether this is a *strong* request. This is the difference between the "ask him to wear a condom" and "tell him you're unprotected" actions.
- The method returns `true` if he agreed to wear a condom.
- The method does *not* check if the NPC has a condom as it can also be called when the player has one.

**DEVELOPER'S NOTES:**
- This method is only really used in makeout scenes and similar. I don't recommend choosing such a complex scene as your first if you're new to writing for Newlife.


#### requestPullout(boolean strongRequest): boolean

Returns `true` if the NPC agrees to pull out and updates relationship values.

**IMPORTANT:**
Because this affects relationships it should *not* be called multiple times.  
It is *strongly* recommended that you store the PC's request and the NPC's reaction in a context or scene variable which you then check & use to disable future requests. You will need to handle the result appropriately in your male orgasm section. 
Some NPCs will "agree" to pull-out but be lying, in particular impregnators always do this if they can get the PC pregnant. This also needs to be handled in your orgasm section.

**NOTES:**
- This method is only used in sex scenes. 
- Relationship values may alter if the NPC is annoyed at being asked.
- If he refuses he's *also* set as having refused to wear a condom. If he can't very well put one on if he's unwilling to withdraw his penis from the player.
- The input boolean is whether this is a *strong* request.  Strong requests are more likely to be accepted. There are no non-strong pullout requests in the current version of the game: a strong request would be one like the existing "ask him to pull out" whereas a weak one would be where she just hints or implies that she'd prefer it.

**DEVEOPER'S NOTE:**
- Due to the complexity of these scenes they are very much *not* recommended for a writer's first scene.


#### setJacketOpen(boolean): void

Sets the NPC's jacket to be open or closed depending on the boolean parameter.

#### setJacketWorn(boolean): void

Sets the NPC's jacket to be worn or removed depending on the boolean parameter. 

**NOTES:**
- This also sets Open to `false`, unlike with shirts.
- If the NPC's outfit did not include a jacket this method will do nothing. You cannot set a non-existent jacket to worn.
- Calling `setJacketWorn(true)` will also put his shirt back on (and closed), but *only* if his outfit included a jacket.

#### setShirtOpen(boolean): void

Sets the NPC's shirt to be open or closed depending on the boolean parameter.

**NOTES:**
- You should not call `setShirtOpen(true)` without first checking if he's wearing a jacket, unless his outfit type is one that can't include jackets.
- The rule is that for an NPC's shirt to be open his jacket must either be open or removed. If you do call this method when his jacket is worn and not open it will also open his jacket. This won't cause an error, but you'd normally need to directly check his jacket status first so you can vary the text.

#### setShirtWorn(boolean): void

Sets the NPC's shirt to be worn or removed depending on the boolean parameter.

**NOTES:**
- Calling this with a `true` parameter will also set it to be not-open.
- If you want the shirt to be unbuttoned you should call `setShirtOpen(true)` after this. 
- You can also use `fixClothing` to put on all of his clothing.
- When removing his shirt, you should normally check for jackets first unless his outfit type cannot include one (nightwear, sexy nightwear, athletic). 
- The rule is that his jacket must be removed for his shirt to be taken off. Calling this method with a `true` parameter will *automatically* remove his jacket if worn, but you'll normally need to directly check this yourself first so you can vary the scene's text to mention the jacket's removal. 
- In many scenes it will be preferable to have separate "remove jacket" and "remove shirt" actions with the second only being enabled when his jacket isn't worn.

#### setTrousersOpen(boolean): void

Sets whether the NPC's trousers are open. 

**NOTES:**
- His cock will be exposed if they are set to open.

#### setTrousersWorn(boolean): void

Sets whether the NPC's trousers are worn or not.

### Text Getters

#### getCockDesc(): String

Returns a short phrase describing his cock.

**NOTES:**
- String is lowercase with no preceding or trailing spaces.

**Example:** `thick, bare cock`

#### getHandAdj(): String

Returns a single, lowercase adjective for the NPC's hands or fingers. 

**NOTES:**
- It will be based on the NPC's body type.
- The method will *always* return a valid adjective. 

#### getTorsoDesc(): String

Returns a short string describing the NPC's torso. 

**NOTES:**
- It will be based on the NPC's body type.

#### getJacket(): String

Returns the NPC's jacket description.

**NOTES:**
- For a shorter string, use `getJacketBasicDesc`.
- Check that is jacket is worn before mentioning it. Unlike with shirts, jackets are often optional in many outfits and an NPC may not start wearing one. They can also begin open.

**Example:** `black suit jacket`

#### getJacketBasicDesc(): String

Returns a one or two word description of the NPC's jacket.

**NOTES:**
- This may read better in some sentences than the longer full description (`getJacket`).
- Check that is jacket is worn before mentioning it. Unlike with shirts, jackets are often optional in many outfits and an NPC may not start wearing one. They can also begin open.

#### getShirt(): String

Returns the NPC's shirt description.

**NOTES:**
- Check that his shirt is worn before mentioning it.
- For a shorter string, use `getShirtBasicDesc`.

**Example:** `white shirt`

#### getShirtBasicDesc(): String

Returns a one or two word description of the NPC's shirt.

**NOTES:**
- This may read better in some sentences than the longer full description (`getShirt`).
- Check that is shirt is worn before mentioning it.


#### getShortDesc(boolean requestedRough): String

Returns a short, lowercase phrase describing the man with no leading or trailing spaces. 

**NOTES:**
- The parameter controls whether phrases like "your master" will be included.
- If no trait/relationship-specific lines are available then the default is `this man`.

**Examples:** `your beloved husband`, `the man you're going to marry`, `this stranger`. 


#### getShortDesc(): String

A shortcut for `getShortDesc(false)`.

#### getTrousers(): String

Returns the NPC's trousers description.

**NOTES:**
- For a shorter string, use `getTrousersBasicDesc`.
- Check that they're worn before mentioning them.

**Example:** `blue jeans`. 


#### getTrousersBasicDesc(): String

Returns a one or two word description of the NPC's trousers.

**Examples:** `trousers`, `jeans`.

**NOTES:**
- This may read better in some sentences than the longer full description (`getTrousers`).
- Check that trousers are worn before mentioning it.


### Condition methods

#### getJacketHasButtons(): boolean

Returns `true` if the jacket has buttons. 

**NOTES:**
- If this returns `false` you can assume it uses a zipper.
- This is used to vary text when it's removed, such as "unbuttoned" or "unzipped".

#### isJacketOpen(): boolean

Returns `true` if the NPC's jacket is open.

#### isJacketWorn(): boolean

Returns `true` if the NPC's jacket is on.

#### isShirtOpen(): boolean

Returns `true` if the NPC's shirt is open.

#### isShirtWorn(): boolean

Returns `true` if the NPC's shirt is on.

#### isTrousersOpen(): boolean

Returns `true` if the NPC's trousers have been opened.

**NOTES:**
- If this returns `true`, his cock is exposed.

#### isTrousersWorn(): boolean

Returns `true` if the NPC's trousers are on.

#### getFigure(): String

Returns the NPC's body type.

#### getHadOrgasm(): boolean

Returns `true` if the NPC has had an orgasm in this scene chain. 

**NOTES:**
- This should typically block sex scenes.

#### hasCondom(): boolean

Returns `true` if the NPC is carrying a condom with him.

#### isWearingCondom(): boolean

Returns `true` if the NPC is wearing a condom.

#### getRefusedCondom(): boolean

Returns `true` if the NPC has refused to wear a condom during this scene or scene chain.

**NOTES:**
- Typically condom-request actions should be blocked if he's refused.

#### isCockExposed(): boolean

Returns `true` if the NPC's cock is exposed.

#### getHadBabyWithPc(): boolean

Returns `true` if the PC has a baby with this character *and* that baby's father is known.

**NOTES:**
- Also see `getBelievesHasBabyWithPc`
- If this NPC impregnated the PC but the baby's parentage is still a mystery then this method will return `false`.
- This method will return `false` for "cuckoo" babies (where the PC successfully lied to the NPC about them being the father).

#### getBelievesHasBabyWithPc(): boolean

Returns `true` if the PC has a baby with this character *and* that baby's father is known.

**NOTES:**
- Also see `getHadBabyWithPc`
- This method will return `true` for "cuckoo" babies (where the PC successfully lied to the NPC about them being the father).

#### isPcPregnantBy(): boolean

Returns `true` if the PC is *knowingly* pregnant by this character and they know about it. 

**NOTES:**
- This means the PC must have informed them that they're the father.
- This also returns `true` if the PC lied to them about being the father.

----
# Baby

Babies are not NPCs, they a collection.

## Actions

### Text Getters

#### getName(): String

Returns the baby's name.

#### getFatherName(): String

Returns the name of the baby's father.

### Condition methods

#### isMale(): boolean

Returns `true` if the baby is a boy, `false` for a girl.

#### getAge(): int

Returns the baby's age in weeks.

#### isFatherKnown(): boolean

Returns `true` if the father is known, `false` otherwise.

----
# ClothingItem

**NOTES:**
- A clothing item counts as singular if it has the `SINGULAR` clothing flag.

## Actions

### Text Getters

#### getItThem(): String

Returns either "it" or "them" depending on whether the clothing item is singular or not. 

#### getItThey(): String

Returns either "it" or "they" depending on whether the clothing item is singular or not.

### Condition methods

**NOTES:** 
- All female clothing items in all 5 slots have access to these methods.

//EDIT: This sentence is strange //

#### getBasicDesc(): String

Returns a one or two word description of the item.

**Code Examples:**
```Velocity
#if (!$w.getTop().isAlsoLowerBody())##
You lift your $w.getTop().getBasicDesc() and let the crowd look at your $w.getBra().getBasicDesc(). ##
#elseif ($w.getTop().hasFlag("LOWCUT"))##
You pull down the top of your $w.getTop().getBasicDesc() and let the crowd look at your $w.getBra().getBasicDesc().
#elseif ($w.getTop().getTopType() == "HALTERTOP")##
You grab the sides of your $w.getTop().getBasicDesc() and pull them together, letting the crowd look at your $w.getBra().getBasicDesc().##
#else##
You flash your $w.getBra().getBasicDesc() at the crowd on the patio. ##
#end##
```


**Examples:** `dress`, `skirt`, `blouse`

#### getColour(): String

Returns the item's colour as a text string

#### getShortDesc(): String

Returns the item's description. 

**NOTES:**
This is the string used in the wardrobe screen's clothing list and is the "short" description as opposed to the longer detailed description that isn't exposed for custom scenes. 
The short description is something like `thin white top` and is suitable for insertion in sentences where the sentence focuses on the item of clothing. 
If the clothing is just being mentioned in passing then it might be a bit too long and the basic description might be preferable.

#### hasFlag(String): boolean

Returns `true` if the clothing item has the specified Clothing Flag, it *must* be a valid flag or an error will result.

**NOTES:** 
- See the enum reference for details.

#### getExposeRemoves(): boolean

Returns `true` if the clothing item is marked to be removed instead of exposed. 

**DEVELOPER'S NOTES:**
- At the time of writing this is limited to non-dress tops with the "zip" toptype. If the clothing item has this flag then setting its status to `EXPOSED` will instead change it to `OFF`.

----
# Lower body clothing

## Actions

### Text Getters

#### Condition methods

##### getLength(): String

Returns the item's length.

**Clothing Lengths:**

| Value | Description | Notes |
| ----- | ----------- | ----- |
| `THIGH` | Skirts etc that go down to the player's thighs. | short skirts |
| `KNEES` | Knee-length | |
| `ANKLES` | Long skirts, trousers, etc. | |

##### isSkirt(): boolean

Returns `true` if this is a skirt-type lower-body clothing.

**Examples:** `skirt`, `dress`, `nightgown`.

**NOTES:**
- Check this before writing text that implies a man puts his hand up her skirt/dress, gets to look up it, or similar.
- Skirts get pulled up when exposed whereas trousers get pulled down.

----
# Legwear

## Actions

### Text Getters

#### getSingularBasicDesc(): String

Returns a single word description of the item.

**Example:** `stocking`

**NOTES:**
- This is the same as `getBasicDesc` but is always singular. 

### Condition methods

#### getSuspenderBelt(): String

Gets the type of suspender belt used by this legwear.

**VALUES:** `NONE`, `LACE`, `SILK`.

#### isLaceTopped(): boolean

Returns `true` if the stocking is lace-topped.

**NOTES:** 
- Affects some minor descriptive text.

#### isThighHigh(): boolean

Returns `true` for thigh-high stockings and `false` for above-the-knee socks.

----
# Upper body clothing

## Actions

### Text Getters

#### Condition methods

##### getTopType(): String

Returns the top-type as a string. 

**NOTES:**
- See enum reference for details.
- Top-type is important for descriptions of the PC's upper body, text where she gets undressed and sometimes text where her breasts are being touched.

##### isAlsoLowerBody(): boolean

Returns `true` if this is also lower-body clothing.

**NOTES:**
- This lets you check for dress-style clothing that covers multiple slots.
- This is the only situation where that will happen: a clothing item that covers both upper and lower-body with the lower-body `isSkirt` method returning `true`. 
- You do not need to write for the possibility of other multi-slot items such as playsuits or one-piece swimming costumes.

----
# Scene methods

**REMINDER:**
These methods use the context id `scene`.  

*For example:* `$scene.clearMap()`

## Actions

### Random item selection

The scene maintains an internal map of string-integer pairs to let writers easily pick from a weighted list.

This can be used to build up a *weighted* list of text snippets or enum values that you can later pick from.

*Weighted Example:**
For example, if a list has an item with a weight of 10 and another with a weight of 20 then the first has a 33% chance of being picked and the second has a 66% chance.


**NOTES:**
- Be careful with enum values because you need to make sure that every list item is valid.
- If the map has no entries then the various pick methods will return `null`. You should aim to ensure this can never happen. One way of handling this is to check if it's empty and use a default value if it is.
- Be sure to *clear* the list when it's fulfilled its purpose if you intend to use it again. 
- The list is *not* shared between scenes. If you call a custom sub-scene then it will *not* have access to your scene's weighted list.
- The chance of an item being picked is based on its *weight*.
- The scene object also has a simpler method to pick an item at random from a non-weighted list.

#### addWeightedItem(String, int): void

Adds the first String parameter to the scene's internal map of weighted items with the second parameter as its weight.

**NOTES:**
- The item will not be added if weight is less than or equal to zero.
- This ensures that the method `isWeightedMapEmpty` will return `true` if and *only* if the pick methods would return an actual String value.

#### isWeightedMapEmpty(): boolean

Returns `true` if the weighted map is empty.

#### pickItem(): String

Picks an item from the weighted map.

#### pickAndRemoveItem(): String

Like `pickItem`, but *removes* the returned String from the map afterwards.

#### pickItemAndClearMap(): String

Like pickItem, but *clears* the map completely afterwards.

#### clearMap: void

Clears the map without returning any values.

#### pickFromList(List<String>): String

Unlike the above methods, this doesn't use the internal map. 

Instead you need to define a List in your Velocity text and submit it as the parameter. 

**Example:** `$scene.pickFromList(\["TONED", $m.figure, "FAT"])`, will select one of the three entries at random. Each item has an equal chance of being returned.


**Coding Example:**

The most common use of this is to populate a list (such as different dialogue lines) based on conditions. 

To do this you'll want to build the list up step-by-step:

First, create an empty list

`#set($myList = \[\])`

Then, add items based on conditions. The `list.add` method will return a boolean, so it should be assigned to a throwaway temp variable to stop "true" or "false" being written to the output.

`#if($w.hasTrait("NICE"))#set($temp = $myList.add("Nice Text"))#end##`
`#if($w.hasTrait("RELAXED"))#set($temp = $myList.add("Relaxed Text"))#end##`

Finally, pick an item from the list to include in the text

`$scene.pickFromList($myList)`

Note that this uses a new if statement for each line. That way a character who's both `NICE` and `RELAXED` would have both options in the list with a chance of either appearing.

In actual dialogue actions it's usually worth including dozens of lines, each with their own specific conditions. The aim is that almost any character would have at least a couple of valid ones, allowing for variety if the action is repeated.

This method will return `null` if the input list is `null` or empty. That usually won't lead to readable text, so it's often also a good idea to include some default lines or ones where their conditions guarantee at least one possibility.

### Other Actions

#### addFlag(String): void

Saves a scene flag that can be checked with `$scene.hasFlag(String)` later.

**NOTES:**
- Scene flags persist across scenes within a scene chain this is the main way of passing information to sub-scenes. Scene flags are *not* an enum value so any string can be used. 

**DEVELOPER'S NOTES:**
I will at some point write a list of flags that can be returned from the makeout and sex sub-scenes, although this is likely to be one of the later documentation tasks.

#### removeFlag(String): void

Removes the provided scene flag. 

**NOTES:**
- This can be any string, but the method will do nothing if it doesn't match a flag that's been set.
- Some sub-scenes may set scene flags that are intended for use in the returning section of their parent scene and should be un-set afterwards, especially if the same sub-scene can be entered repeatedly and you want to avoid information from previous calls contaminating the response to later ones.

#### clearPostSexFlags(): void

//EDIT: This is a strange sentence //
Removes a sex of scene flags that are mainly intended for returning actions to track what happened in a preceding sex or makeout scene.

**NOTES:**
- This is important if your scene can launch multiple makeout transitions, or if it transitions to another scene which can. 
- Usually these flags would be cleared at the end of the transition's text section in the `.vm`.
- This usually can't be called in an effects section in the YAML, because this would remove the flags before the text is processed and prevent them from being used to modify it.
- This method is also called when you change active male NPC via `setActiveMaleNpc`, as long as the previous active NPC was set to a different character than the new one. This also clears a number of NPC-specific scene flags, such as `AGREED_ROUGH`.
- The list of flags removed by this is as follows: `COME_IN_MOUTH`, `FINISHED_SEX`, `FINISHED_ANAL_SEX`, `CAME_INSIDE`, `CAME_INSIDE_ANAL`, `MO_REJECTION`, `STOPPED_SEX`, `BLOCK_REJECTIONS`, `BLOCK_REQ_STOP_ROUGH`

#### setActiveMaleNpc(ContextMaleNpc): void

Sets the active male NPC. 

**NOTES:**
- This can be important because it affects which NPC's attractiveness modifies the PC's arousal. Scenes with multiple NPCs may also want to restrict some NPC actions to the active NPC.
- Changing an active male NPC will also clear certain scene-flags that are assumed to be specific to the previous guy.
- If your scene has no male NPCs then you'll obviously never use this.
- If your scene is a sub-scene with just a single male NPC then you usually won't need to use this as the parent should generally have set arousal from that NPC. 
- If you need the active NPC to be populated (e.g. to use the `isRoughAgreed `method) then use `setActiveMaleNpcNoArousal` *instead* of this method. Otherwise the NPC's attractiveness modifier could end up being added twice to the PC's arousal.
- If your scene is a starting scene with single male NPC then you should set that NPC as active in the intro.
- If your scene has multiple male NPCs then you should set the one who's primarily interacting with the PC as active. This may change over the course of the scene and you may not have an active npc at the start.
- It is safe to call this method when the new active male NPC is the same as the current one, in that case it does nothing.
- Also see `setActiveMaleNpcNoArousal`

#### setActiveMaleNpcNoArousal(ContextMaleNpc): void

Sets the active male NPC, but does *not* change arousal values or scene flags.

**NOTES:**
- This should be used when your scene is a sub-scene and the parent will have already set arousal based on the NPC's attractiveness, but you want them to be set as active in your scene so you can use methods like `isAgreedRough` or reference them with `$activeMaleNpc`.
- Also see `setActiveMaleNpc`

#### hideNpc(ContextNpc): void

Hides the NPC.

**NOTES:**
- Also see `unHideNpc`
- Also see `isNpcHidden`
- Takes an NPC (of either gender) as an argument. 
- Any hidden NPC will *not* appear if the player clicks the *Describe Characters* button.
- You might use this if an NPC is needed in a scene but isn't present initially. In this case you can have them present but hidden and un-hide them when they show up.
- You might use this if an NPC leaves: you can hide them so it'll seem to the player that they aren't present. (You'll also need to ensure any NPC action conditions are written so they can't take actions!)
- You might use this if you need a 'reference' NPC who isn't present but whose stats you'll need to check. Such as if your scene involves the PC talking about her boyfriend with one of her friends then you could have the boyfriend as an NPC so you can check his stats but hide him so it won't seem like he's there.
- If the NPC is to be hidden initially then you should call this method in the intro section.

#### unHideNpc(ContextNpc): void

Stops the NPC from being hidden.

**NOTES:**
- Also see `hideNpc`
- Also see `isNpcHidden`
- Takes an NPC (of either gender) as an argument. 

#### inseminateNpc(ContextMaleNpc, ContextFemaleNpc, int) : void

Inseminates the female NPC by the male one. 

**NOTES:**
- The first parameter is a male NPC.
- The second parameter is a female NPC.
- The third parameter is an int modifier that adjusts the chance of pregnancy.

**DEVELOPER'S NOTES:**
- Set the third parameter to zero for default situations where the male NPC cums inside the female one. 
- set the third parameter to -10 for situations where he partially pulls out but not well enough.

### Text Getters

#### addPossessiveSuffix(String): String

A helper method that returns the input string with a possessive suffix added. 

**Examples:** `John` to `John's`; `Lewis` to `Lewis'`.

#### capitalise(String): String

Returns the input string capitalised.

**NOTES:**
- Used if you're retrieving a non-capitalised string value from a method and want to use it to start a sentence.

#### getArticle(String): String

Gets the article ("a" or "an") appropriate to the provided string.

#### getFloor(): String

Returns the floor description for this scene's location.

**Example:** `softly-carpeted floor`

#### getWall(): String

Returns the wall description in this scene's location.

**Example:** `dirty alleyway wall`

### Condition methods

#### getActiveMaleNpc(): MaleNpc

Returns the active male NPC context object. 

**NOTES:**
- Equivalent to using `$activeMaleNpc`.

#### percent(int): boolean

Makes a random check with a percentage chance of success equal to the supplied int. 

**NOTES:**
- Values of zero or less will *always* return `false`
- Values of 100 or greater will *always* return `true`

#### randomNumber(int limit): int

Returns a random number from 0 to limit-1. 

**NOTES:**
- This will error if limit is 0 or negative.

**Example:** `randomNumber(3) `will return either 0, 1 or 2. 

#### randomBoolean: boolean

Returns either true or false, at random.

#### hasFlag(String): boolean

Returns `true` if the scene-flag represented by the parameter has been set, either via the `$scene.addFlag` method in a custom scene or by a sub-scene. 

**NOTES:**
- Scene flags are not an enum and can be any string.

#### getHasBed(): boolean

Returns `true` if this scene's location has a bed. 

**NOTES:**
- Transitions to the lying makeout should only happen in locations with beds.

#### isOutside(): boolean

Returns `true` if this scene's location counts as being outside. 

**NOTES:**
- The main effect of this is to use "ground" instead of "floor".

#### isNpcHidden(ContextNpc): boolean

Returns `true` if the NPC referenced is hidden.

**NOTES:**
- Also see `hideNpc`
- Also see `unHideNpc`
- Takes an NPC (of either gender) as an argument. 


#### isRoughAgreed(): boolean

Returns `true` if rough-mode has been agreed with the current active male NPC.

**NOTES:**
- An error will be thrown error if an active male NPC has *not* been set.
- Rough-mode counts as being set if the scene flag "`AGREED_ROUGH`" is set or if the relationship is flagged as always being rough. 
- The scene flag gets cleared whenever the active male NPC is changed.
- This method does *not* check the `BLOCK_ROUGH` trait. It's assumed that these characters will not be able to access a situation where the `AGREED_ROUGH` flag or always-rough relationship status will be set.
- If your scene is setting `AGREED_ROUGH` or the always-rough relationship status then you should *first* check for the `BLOCK_ROUGH` trait before doing so.

#### isNpcRough(boolean allowBehaviourFaking): boolean

Returns `true` if the active male NPC is allowed to take rough actions.

**NOTES:**
- An error will be thrown error if an active male NPC has *not* been set.
- This will return `true` if rough-mode has been agreed in which case `isRoughAgreed` will *also* return `true`. 
- This method can return `true` if the NPC is allowed to take rough actions *without* the approval of the PC.
- This checks his behaviour and also whether the PC has the `BLOCK_ROUGH` trait.
- When gating rough NPC actions behind this boolean, it will often be useful to write PC-reactions for both situations: where she's agreed to be treated roughly, and when she hasn't. In the latter case consider text for `LIKES_ROUGH` (where she enjoys it) and `LOW_SELF_ESTEEM` (where she accepts it as her due) as well as a default section where she's annoyed or angry.

----
# GameData methods

**REMINDER:**
These methods use the context id `gd`.  

*For example:* `$gd.addJobPerformanceModifier(5)`

## Actions

#### addJobPerformanceModifier(int amount): void

Adds a numeric modifier for the next time job performance is calculated. 

**NOTES:**
- This will only affect job performance once. The modifier can be positive or negative.
- Job performance affects the performance-related component of pay and the chances of promotion. Low performance can lead to negative events, potentially even a sacking.
- A large temporary modifier could get the PC a promotion even if her skills wouldn't normally be good enough, although getting promoted beyond her abilities will affect performance in the future as higher jobs have higher expectations.
- This method should typically be used if the PC does something that affects how she does at work that week – it's most commonly used in workplace events.
- Job performance is not strictly capped in either direction (it can be negative), but it's commonly in the 0-100 range based on work skills with modifiers for stress, traits and so on.

#### addStat(String stat): void

Increases the Stat by 1.

#### addStat(String stat, int amount): void

Increases the stat represented by the stat parameter by the amount of the second parameter.

#### setStat(String stat, int amount): void

Sets the stat to the amount provided, regardless of what its previous value was. 

**NOTES:**
Equivalent to calling `addStat(stat,(getStat(stat)*-1)+amount)`.

#### removeGameFlag(String): void

Un-sets the supplied GameFlag.

#### setGameFlag(String): void

Sets the GameFlag that matches the parameter. 

**NOTES:**
- An error will be thrown if the parameter isn't a valid value.

**DEVELOPER'S NOTES:**
Game-flags are used to convey information across scene chains.
For instance, if you need to flag that your scene has happened so you can vary its text on repeats. 
You can use the `TEST_FLAG` in testing, but make sure to let me know what new flag is needed and how it's to be used when you submit the scene.

### Text Getters

#### getJobTitle(): String

Return's the PC's job title. 

**Example:** `trainee saleswoman`

### Condition methods

#### getStat(String stat): int

Returns the integer value of the stat. The parameter *must* be a valid stat.

#### hasGameFlag(String flag): boolean

Returns `true` if the submitted gameflag is set. The parameter *must* be a valid GameFlag.

#### getAllowAnal(): boolean

Returns `true` if the "allow anal" game option has been set.

**NOTES:**
- Check this before writing any anal content.
- Alternate Syntax: `$gd.allowAnal`

**Code Examples:**

```Velocity
#if($gd.getAllowAnal())
  Anal Sex Content
#else
  Alternate Content
#end
```


