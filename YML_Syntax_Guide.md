YML Syntax Guide
================

Overview
--------

This is the guide for how to structure Newlife scene definitions in
YAML. For an overview of general YAML syntax see
<https://en.wikipedia.org/wiki/YAML>.

There's a small example scene in the additional\_scenes documentation
folder. Copy this and the associated text file to the
user\_custom\_scenes folder to test them in-game.

To test a YML scene definition, it must be in the
additional\_scenes/user\_custom\_scenes folder with a .yml file
extension. Set the in-game option to allow testing of custom scenes and
choose the appropriate activity from the weekday-evening timeslot.

Only one scene should be defined per file.

General rules
-------------

YAML files use indentation to determine their structure and incorrect
indentation will usually make Newlife unable to parse the file.

Each entry in the file is a Map of key: value pairs. The value could
then be a text String, another Map or a List.

Maps and Lists can be nested multiple layers deep. For example the
scenetransition maleNPCs section is a Map (for each male NPC) within a
List (of maleNPcs) within a Map (the sceneTransition section) within a
Map (the Action definition) within a List (the list of actions) within a
Map (the overall scene definition).

Some String entries are passed to Velocity. These will be processed
similarly to Velocity content in the text file and use the same syntax.
Bear in mind that Velocity strings containing YAML special characters
such as \# or ! must be escaped by enclosing them in double-quotes.

In particular, any conditional section will be passed into velocity as
the condition in an \#if statement, any must be valid to be evaluated as
such. In most cases a blank or missing condition counts as TRUE. The
exception is in the scene-ending situations returnToParent and
finishScene which count as FALSE if not set.

Every action including the intro and returning sections *must* *always*
set at least one follow-up action (default actions count, as long as at
least one is always available) unless it defines a scene transition or
calls for the scene to end or return to parent. When setting follow-up
or default action lists with conditions make sure that at least one will
always be valid.

Whenever an action ID or text section is specified, the appropriate
action or text section with that ID must also exist in the appropriate
file.

If your scene is a sub-scene that's called by others then you must
decide if it's a returning one or not. If it's returning then you should
use returnToParent when it's done and never finishScene. Otherwise the
opposite holds true.

Top-Level Structure
-------------------

The top-level structure contains the following entries. Complex entries
such as sub-maps have their internal structure defined in later
sections:

#### textFileName

A simple String value. This is the filename for the text file associated
with this scene. It must match a file in the same directory.

#### sceneDescriptionTextId

A string matching the ID of the text section in the text file that'll be
used when the player clicks "describe scene". Required, and it must
match a valid ID.

Scene descriptions in submitted scenes should not contain actions that
modify game state because there's no limit to the number of times a
player can trigger them. This could be useful in testing though: e.g.
add an increaseArousal call to the scene description in order to
fine-tune arousal levels. This sort of thing must be removed before the
scene is submitted though.

The complexity of your scene definition will depend heavily on the
nature of the scene. Some scenes have very long scene definitions with
many conditions while others are extremely simple.

#### characterDescriptionTextId

An **optional** string matching the ID of the text section in the text
file that'll be used when the player clicks "describe characters".

Unlike the scene description section, this is optional. If it isn't set
then the default character description code will be used instead. When
using the default descriptions, you can hide NPCs using the
\$scene.hideNpc method. See the context object reference for details.

If this is set, then there must be a matching section in the .vm file.
Otherwise the player will see an error message when they click the
character description button.

The default descriptions will usually be the best choice for most
scenes. This lets you replace them if they're unsuited for your one
though.

#### testingInfo

Map that defines values needed by the testing scene.

#### intro

An action definition without short/long descriptions. Used when the
scene is first started. Uses the same structure as individual Action
sections.

#### behaviourChange

An action definition without short/long descriptions, much like the
intro one. This is used when one of the default behaviour-change actions
is used. (see useBehaviourActions in the Action section). The
pcBehaviour value for the active NPC is set before this is called, so
you can check it to see which behaviour the player chose.

behaviourChange is only used when a default behaviour-selection action
gets chosen. Setting behaviour directly (via the NPC setPcBehaviour
method) will not call this.

This section is only needed if one of your actions can set
useBehaviourActions. If that's the case, then it must be set or the
scene will error when a behaviour action gets chosen.

#### actions

A list of Action sections. All of the PC's actions must be defined here,
except for the default "finished" and "proceed" actions which will be
handled when you set the scene to finish or transition respectively. See
below for the structure of individual actions.

#### returningSections

List of Action sections without short/long descriptions. These are used
if one of your actions defines a scene transition to a sub-scene that
will return to its parent. Scenes that don't call such a transition will
not need this section.

#### defaultActions

A Map of name:value pairs where the name is an Action id and the value
is the conditional string that checks if it'll be available.

The default action section is needed if any of your actions sets
useDefaultActions to any condition that can evaluate as true. Otherwise
it can be left out.

#### maleNpcActions

List of NPC Action maps. The sub-map structure is defined below. This is
only needed if one of your actions specifies that Npc actions should be
taken.

This is usually in scenes which are 'turn-based' using a sequence of the
PC picking an action from the default list followed by the NPC taking
his action.

Narrative scenes that can be defined as a graph of nodes usually won't
need NPC actions. Instead the NPC's actions and can be defined within
the player-action's text & action sections.

#### femaleNpcActions

Identical to the male action list, except that these are run by female
NPCs instead of male ones.

#### sceneEndProcessing

An optional text entry. If set, this will be passed into velocity for
processing when one of the following happens:

-   The scene finishes
-   The scene returns to its parent
-   The scene transitions to another with no returning ID set.

Text output from sceneEndProcessing is discarded.

This can be used to add standard effects to happen when the scene
finishes. It's intended for scenes with many similar ending paths where
it'd be annoying to have to write in the same effects for every single
scene-exit: for example the cooking class scene uses this to increase
the player's skill.

TestingInfo
-----------

#### playerOutfit

String value that must be a valid outfit type. The PC will be dressed in
a random outfit of this type from her wardrobe.

#### maleNpcs

List of NPC maps. An NPC map has 2 entries, "id" and "outfit".

ID is a string which will be used as the NPC's ID in-scene. The NPC's
object in the Velocity context will be stored with this key.

Outfit is a String which must be a valid outfit type. It'll be used to
dress the NPC.

The testing scene will prompt the player to pick an NPC for each ID
before starting the scene.

#### femaleNpcs

Identical to the maleNpcs section, except the testing scene will prompt
for female NPCs.

#### location

The Location section used for this scene. This is the same as that used
in scene transitions, except that you cannot set useCurrentLocation due
to it not being set.

Action
------

Action sections are used in the actions and returningSections lists, as
well as for the intro. They take the form of a Map with the following
entries:

#### id:

String. The ID for this action. Required for actions and
returningSections. Used to reference this action in follow-up action
sections.

#### shortDesc:

String. The short description for this action, used in the action-picker
list in the UI. Must be a short single-line piece of text. Not required
for intro or returning sections.

This and the longDesc can be either fixed text or a text-id for a
section in the text file. The game will check if any such section exists
with this string as its ID and use it if it does. This allows you to
include dynamic object references such as an NPC's name.

Since 0.7.7, both short and long descriptions are set when the action is
chosen as an option for the player, and will be re-calculated if this
happens multiple times. As such, you can use variables that change
mid-scene such as arousal levels and so on.

Descriptions also should not include method calls that change game
state. If you need to make such a call when the scene's loaded it should
be in the intro section.

#### longDesc:

String. The long description for this action, shown in the action
description when the player selects it in the UI. Handled the same as
the shortDesc, but of course can be a longer piece of text. Not required
for intro or returning sections.

#### textId:

Key for a text section within the text file. This is required for all
action sections and the section must exist in that file.

#### effects:

This section handles game effects that the action should make. You can
also put these directly into the Velocity text sections. The effects
section is processed before the text.

A list of Maps. Each map has 2 entries, or just 1 if the condition is
omitted. These are:

effect:

String. The effect that is to be performed. This is passed directly into
Velocity and should consist of method call(s) that can be processed
there. Any text output by effects sections is discarded and will not be
shown to the player.

condition:

String. A condition string that determines if the effect will take
place. Optional and counts as true if blank or missing.

#### allowNpcActions:

String. A condition that determines if an NPC action will be triggered.
Treated as false if blank or if the entry isn't present.

An Npc action will not be made if the action calls for the scene to
transition or end.

See the NPC Action section for more information on how these are
processed.

#### finishScene:

String. A condition that determines if the scene should finish. Defaults
to false if not set. This is the highest priority entry and will
override any other follow-ups/transitions if true.

#### returnToParent

String condition defaulting to false. Similar to finishScene but instead
returns to the scene's parent. Second-highest priority after
finishScene.

Will cause an error if the scene has no parent – use this only for
sub-scenes.

#### sceneTransition

Map of a Scene Transition – see the definition below. Third-highest
priority when determining follow-up actions, and like finishScene and
returnToParent will block any NPC actions if it triggers.

#### useBehaviourActions:

String condition defaulting to false. Sets whether the player should be
presented with a list of behaviour-change actions related to the current
active male NPC (e.g. friendly, flirty, cute etc). The game will use a
standard method to decide which behaviours are available to the player:
the same logic used in the standard town-date scene and similar. This
will always give the player at least one action to choose from.

The active male NPC must be set when this evaluates to true or an error
will be thrown.

If this can evaluate to true then the action-response section for
behaviour change actions must be populated (see behaviourChange above).

This overrides useDefaultActions and the followUpActions section. Both
will be ignored if this is true.

If your scene uses behaviours (many don't) then it's often a good idea
to check pcBehaviour when the active male NPC gets set: often in the
intro. If this is null then the player should be prompted to choose a
behaviour. You may also want to have a "change your behaviour" action
that lets the player pick a new one at any time.

#### useDefaultActions:

String condition defaulting to false. Sets if the default action list
should be used. The followUpActions section will be ignored if this is
true.

#### followUpActions

Map of key:value pairs where the key is an action ID and the value is
the condition that's checked to see if the action should be added to the
available ones for the player. Blank conditions evaluate to true.

NPC Action
----------

NPC actions are found in the maleNpcActions and femaleNpcActions
sections. They're processed whenever an action sets allowNpcActions to
true, unless the scene is ending or transitioning.

If an Npc action returns follow-up actions then this will override any
follow-up actions defined in the player's action.

When NPC actions are triggered, each NPC of the appropriate gender is
checked against each action. These are built into a weighted list which
is then used to pick one. If you have a scene with multiple male NPCs
and want to restrict an action to the active one then you need to check
this specifically in its conditions.

The NPC that's performing the action can be accessed with \$npc while
the action is processing and in the condition to check if it should be
available.

#### id

String. The ID for this NPC action. Primarily used in error reporting.

#### effects

Effects Map. Identical to the player-action field of the same name.

#### textId

String. ID for the Velocity text section in the text file. Must exist
and be valid.

#### condition

String condition used to determine if this action should run for a given
NPC. Use \$npc to access that NPC if your scene has more than one.

#### weightMultiplierConditions

Optional. List of Strings representing conditions. Each one that
evaluates to true will double the action's weight for this NPC. You can
use this for actions that should be available to all NPCs but more
likely for those with certain traits. Avoid having more than a handful
of multiplier/divisors as they each have quite a large effect.

#### weightDivisorConditions

Same as weightMultiplierConditions but each one halves the weight.

#### followUpActions

Map of id:condition like the player-action equivalent. If an NPC action
calls for follow-up actions then these take priority over any requested
by the player-action.

When writing this is something to consider. If a player-action is a
multi-stage one that calls for follow-ups (e.g. "get a drink" followed
by a choice of several specfic drinks) then it shouldn't allow for NPC
actions.

#### finishScene

String condition. Identical to the player-action field of the same name.

#### returnToParent

String condition. Identical to the player-action field of the same name.

#### sceneTransition

Scene Transition Map. Identical to the player-action field of the same
name.

Scene Transition
----------------

Defines a transition to another scene. Unfortunately one of the more
fiddly and error-prone parts of Newlife scenes.

There are generally 2 types of transitions: returning and non-returning.

Returning transitions go to sub-scenes that are expected to return to
their parent. For example the Makeout scenes. These must define a
returningId and an appropriate returning section.

Non-returning transitions do not expect to come back to this scene. For
instance going to a date scene. They should not have a returningId
defined.

#### condition

String condition that determines if the transition should happen.

#### maleNpcs

List of maps. The Maps take 2 entries: id and npc. Both are required.

The id entry is the NPC's id in the scene you're going *to*. This is
usually defined in the transition type. For transitions to other custom
scenes check the testingInfo section to see which NPC ids it expects.

The npc entry is the NPC's id in *this scene*. This is checked against
the context so you can use \$npc and \$activeMaleNPC if they've been
set.

#### femaleNpcs

Same as maleNpcs but for female ones.

#### type

The type of transition. Must match one of the below uppercase values
exactly. The type will affect whether it's a returning transition and
which NPCs are required.

CUSTOM

The transition is to another custom scene. The transitionInfo section
must have an entry with the key ymlFile and the value of the other
scene's yml filename. You should not make a scene transition to itself,
or at least not in a way that can carry on indefinitely.

This may be returning or not. You'll need to check with the specific
custom scene for calls to returnToParent and finishScene. A custom scene
should not include both of these.

You'll also need to define NPCs based on what the custom scene expects.

STANDING\_MAKEOUT

Transition to a standing makeout. This is a returning sub-scene. It
takes one male NPC with the id "man".

LYING\_MAKEOUT

Transition to a lying makeout. This is a returning sub-scene. It takes
one male NPC with the id "man".

SITTING\_MAKEOUT

Transition to a sitting makeout. This is a returning sub-scene. It takes
one male NPC with the id "man". You can prevent this from transitioning
to other makeouts by setting a scene flag of
BLOCK\_SITTING\_MO\_TRANSITION\_TO\_OTHER\_MAKEOUTS. This also stops
going to bed for anal sex.

HOME\_DATE

Transition to a date at the PC's home. A non-returning transition. This
does not take a Location section as the location is always the player's
home. It takes one male NPC with the id "date".

The scene will use the PC's behaviour if this has been set via
setPcBehaviour on the relevant male NPC object. Otherwise the player
will be prompted for their behaviour post-transition.

DANCE\_TOGETHER

Transition to the 'dancing together' scene. A returning transition. It
takes one male NPC with the id "maleDancer". This is the scene used in
dance classes and when dancing with a date at home: the nightclub
dancing uses a different one.

The transitionInfo section may have an optional boolean parameter called
"inPublic". This determines whether the dance is in a public place or
not. Certain more intimate actions like kissing are blocked for public
dancing. Dancing at home on a date is not public, while the dance
classes and competitions are. It defaults to false if not set.

ORAL\_SEX

Transition to the oral sex scene. A returning transition. It takes one
male NPC with the id "man".

The transitionInfo section must have an entry with the key "position"
and a value of "STAND", "LIE" or "SIT" (case-sensitive), referring to
whether the man is standing, lying on his back or sitting down.

The oral scene does not take a Location so you don't need to set this
section in the transition.

CUNNILINGUS

Transition to the cunnilingus scene. A returning transition. It takes
one male NPC with the id "man".

The transitionInfo section must have an entry with the key "position"
and a value of "STANDING", "LYING" or "SITTING" (case-sensitive). Note
that this is different from the oral transition – I'll be standardising
these at some point but it's probably the oral\_sex ones that'll change.

A Location is required.

SIXTY\_NINE

Transition to the 69 scene. A returning transition. It takes one male
NPC with the id "man".

The 69 scene has the PC on top of the man in bed. The 69 scene is not
written to support heavily pregnant characters and while it won't break
outright, there is no specal text for this situation. It also assumes
both the man's cock and the pc's pussy are exposed before starting the
scene.

The custom scene transition doesn't support passing in a makeout scene,
so the 69 scene's exit paths that return to a makeout can't trigger. In
particular, the male NPC will not end this scene without a makeout to
return to unless he's had an orgasm.

This transition has no other parameters and does not take a location.

ANAL\_SEX

Transition to the anal sex scene directly, without going via a makeout.
Must have a location set. It takes one male NPC with the id "man". This
is a returning transition.

The transitionInfo section must have an entry with the key "lube" and a
value of "NONE", "SOME", "NATURAL" or "LOTS". This is case sensitive.

The transitionInfo section may also have an entry with the key "inBed"
and a value of "true". This will set the anal sex to be happening in
bed. If the entry is omitted or set to any other value then the anal
scene defaults to being on the floor, even if the provided location has
a bed in it.

STANDING\_FRONT\_SEX

Transition to the face-to-face standing sex scene. Returning transition
that takes one male NPC with the id "man". This requires a location.

STANDING\_BEHIND\_SEX

Transition to the face-to-face standing sex scene. Returning transition
that takes one male NPC with the id "man". This requires a location.

The TransitionInfo section may also have an entry with the key
"pressedAgainstWall" and a value of "true". This will set the scene to
start with the PC pressed fully up against the wall. If the entry is
omitted or set to any other value then it'll count as false.

MISSIONARY\_SEX

Transition to the missionary sex scene. Returning transition that takes
one male NPC with the id "man". This requires a location.

The TransitionInfo section may also have an entry with the key
"legsOpen" and a value of "true". This will set the scene to start with
the PC's legs open. If the entry is omitted or set to any other value
then it'll count as false.

It may also have an entry with the key "legsWrapped" and a value of
true. This will start the scene with your legs wrapped around your
partner. If both this and legsOpen are true, this one takes precedence.

DOGGY\_SEX

Transition to the doggy-style sex scene. Returning transition that takes
one male NPC with the id "man". This requires a location.

FACE\_DOWN\_SOFA\_SEX

Transition to the face-down sofa sex scene. Returning transition that
takes one male NPC with the id "man". This requires a location.

COWGIRL\_SEX

Transition to the cowgirl-position sex scene. Returning transition that
takes one male NPC with the id "man". This requires a location.

CHEATING\_CONFRONTATION

A returning transition to the scene where the PC's partner reacts to
finding out that she's been unfaithful. Requires a location.

This has 2 main paths: confession and discovery. In the first path, the
PC is confessing her cheating. This confesses all the cheating she's
done with all male NPCs.

The discovery path involves the bf finding out about the PC's cheating
with a specific male NPC. To use this path, the discoveredCheatingMan
npc should be set.

The transition takes the following parameters:

-   A male NPC with id "bf". This must be the PC's partner: her
    boyfriend, fiance or husband.
-   An optional male Npc with the ID "discoveredCheatingMan". This is
    the man the PC's partner has found out about. If this is set then
    the scene will use the discovery path, otherwise it'll use the
    confession one.
-   An optional boolean parameter "allowLie" in the
    TransitionInfo section. This determines whether the PC is allowed to
    lie to her partner and deny cheating. It defaults to false if
    not set. This value is not relevant in the confession path and can
    be omitted there.
-   An optional boolean parameter "blockSexTransitions" in the
    TransitionInfo section. This determines whether the
    cheating-confrontation scene is allowed to transition to sex between
    the PC and her partner. It defaults to false if not set, which in
    most cases will be the desirable option unless you're writing your
    own sex transition in the returning section that's more specific to
    your scene.

This transition should only be called if the PC has actually cheated
with at least one NPC (and with the specific discovered one for the
non-confession path) and should not be called if the
KNOWS\_LIKES\_TO\_SHARE relationship flag is set with the PC's partner.

This scene can end the PC's relationship, so the returning section may
need text for if they broke up.

It may also set a scene flag "UNHAPPY\_CHEATING\_DISCOVERY\_OUTCOME" for
when the interaction makes the NPC very unhappy:. This will not be set
if she asks for forgiveness and he grants it, but will be if she insults
him, tells him she wants to be with the other man or if he gives her a
final warning never to cheat again.

The returning section may also benefit from text for the
KNOWS\_LIKES\_TO\_SHARE relationship flag which will be set in this
scene if the PC's bf has the LIKES\_TO\_SHARE trait.

TOWN\_DATE

Transition to a date in town. A non-returning transition. Does not take
a Location section. It takes one male NPC with the id "date".

The scene will use the PC's behaviour if this has been set via
setPcBehaviour on the relevant male NPC object. Otherwise the player
will be prompted for their behaviour post-transition.

The transitionInfo section may have an optional boolean parameter called
"getReadyForDate". It defaults to false if not set. If this is true then
the scene starts at the "getting ready" section, like when towndate is
accessed from the week-planner. Otherwise it assumes the PC and NPC are
heading into town together having already met each other and will start
from the "let's go" action.

LESBIAN\_TOWN\_DATE

Lesbian equivalent to town-date above. Non-returning with no location.
Requires a female NPC with the id "date". This will use the PC's
behaviour if it's been set on the npc object.

It may containt a boolean parameter called getReadyForDate which works
the same as the parameter for the town\_date transition.

SPITROAST

Transition to a threesome spitroast scene, a returning transition.
Requires a location section.

This takes 2 male NPCs with the Ids "frontM" and "backM". The scene
assumes both men's cocks are exposed, as is the PC's pussy.

The transitionInfo section may also have an entry with the key "inBed"
and a value of "true". This will set the sex to be happening in bed. If
the entry is omitted or set to any other value then the scene defaults
to being on the floor, even if the provided location has a bed in it.

The transitionInfo section may have an optional entry called "style". If
present, this must have one of the following values: ENJOYING,
HUMILIATING, USING, ROUGH. If not present, the spitroast scene will
choose a style based on what it thinks would fit the characters best.

The ENJOYING style represents a threesome where all participants are
straightforwardly having fun with each-other.

The USING style represents one where the men are just using the PC for
her body and she's simply accepting the situation.

The ROUGH style represents one where the men are brutally fucking the
PC. This will automatically be replaced by USING if BLOCK\_ROUGH is set.
This style is not only for asshole men – it can also be used for
encounters where a LIKES\_ROUGH PC has specifically requested to be
treated roughly.

The HUMILIATING style means the PC's doormat partner has been pressured
into the encounter and isn't happy with it. If you set this style, the
scene will assume that frontM is the PC's partner and that he has the
doormat trait. Check for these conditions before using this style as the
scene will not make sense if they are not met.

LESBIAN\_HOME\_DATE

Transition to a date at the PC's home with another woman. A
non-returning transition. This does not take a Location section as the
location is always the player's home. It takes one female NPC with the
id "date".

The scene will use the PC's behaviour if this has been set via
setPcBehaviour on the relevant male NPC object. Otherwise the player
will be prompted for their behaviour post-transition.

LESBIAN\_LYING\_MAKEOUT

Transition to a makeout with a female NPC in bed. A returning
transition. It takes one female NPC with the id "npc". Additionally, you
must select which character is taking the more dominant role by adding a
mandatory transitionInfo entry with the id "dominant" and a value which
must be one of "PC\_DOMINANT","NPC\_DOMINANT" or "NEITHER\_DOMINANT". A
location is required.

LESBIAN\_STANDING\_MAKEOUT

Transition to a standing makeout with a female NPC A returning
transition. It takes one female NPC with the id "npc". Additionally, you
must select which character is taking the more dominant role by adding a
mandatory transitionInfo entry with the id "dominant" and a value which
must be one of "PC\_DOMINANT","NPC\_DOMINANT" or "NEITHER\_DOMINANT". A
location is required.

LESBIAN\_GIVING\_CUNNILINGUS

Transition to a scene where the PC is giving cunnilingus to a female
NPC. This can also be accessed from lesbian makeouts or from the
receiving cunnilingus scene. A returning transition. It takes one female
NPC with the id "npc". A location is not required.

This transition has two required entries in transitionInfo. First, it
must have an entry with the id of "npcAttitude" and a value of NORMAL,
TENDER or ROUGH. Second, it must have an entry with the id of
"npcPosition" and a value of STANDING, LYING or SITTING.

LESBIAN\_RECEIVING\_CUNNILINGUS

Transition to a scene where the PC is receiving cunnilingus from a
female NPC. This can also be accessed from lesbian makeouts or from the
giving cunnilingus scene. A returning transition. It takes one female
NPC with the id "npc". A location is not required.

This transition must have an entry in transitionInfo with the id of
"npcPosition" and a value of STANDING, LYING or SITTING.

OUTFIT\_CHANGE

Transition to a short scene that lets the PC change her outfit. A
returning transition. It takes no NPCs or location.

The transition has 3 required values in transitionInfo:

-   An entry with id "outfitType" and one of the following values:
    CASUAL, GOING\_OUT, BUSINESS, ATHLETIC, NIGHTWEAR, SEXY\_NIGHTWEAR,
    FORMAL, WEDDING. This determines the outfit types that the PC will
    be able to change into.
-   A boolean entry with the id "forceChangeIfPossible". If this is true
    the PC will be required to choose an outfit unless no valid
    ones exist.

The subscene will give the PC a choice of outfits, from all their
defined ones of the given type with the exception of the outfit she's
currently wearing. This does not guarantee that she will change her
outfit: even with the force-change option, there may not be any valid
outfits to change into. If the PC did change then the scene will set the
scene flag "SUCCESSFULLY\_CHANGED\_CLOTHES".

#### returningId

ID for a returning section. This must be set for returning scenes and
not for non-returning ones.

#### transitionInfo

Map of key:value pairs. This is a sort of catch-all category for
information that might be needed by a specific transition type. The only
value used at present is ymlFile for transitions to other custom scenes.

#### location

Location section: see the definition below.

Location
--------

Used in scene transitions and testing info. Defines a location.

If you're using an existing location then only that boolean is required.
Otherwise you need all 4 of the other values.

#### usePlayerHome:

Boolean. This is *not* a String condition. Use either "true" or "false".
If this is true the PC's home will be used. In that case any other
values in this Location section will be ignored.

#### useCurrentLocation

Boolean. This is *not* a String condition. Use either "true" or "false".
If this is true the current scene's location will be used. In that case
any other values in this Location section will be ignored.

#### wall

String. The wall description e.g. "cold brick wall". Should be a
lowercase string.

#### floor

String. The wall description e.g. "dirty alleyway floor". Should be a
lowercase string.

#### hasBed

Boolean. Whether the location has a bed. Affects which sex scenes will
be available in makeouts.

#### isOutside

Boolean. Whether the location counts as outside. Mostly used to switch
between "floor" and "ground" in some text sections.
