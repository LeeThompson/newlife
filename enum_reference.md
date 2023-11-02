# Wiki conversion notes
1. A few items need some researching
2. When functions are referenced, they should link to the Context wiki.
----

| ENUM | Scope | Description | Notes |
| :--- | :---- | :---------- | :---- |
| VALUE | VALUE | VALUE | VALUE |


# About this Document

This is the reference for "enum values" in Newlife custom scenes.   In this context, enum is short for "enumerated string", for a broader guide to the concept Wikipedia has an [article](https://en.wikipedia.org/wiki/Enumerated_type) on the subject.
Within Newlife, these are typically passed into or returned by various method as text strings.

This document lists the valid values for various enums relevant to Newlife player-written content. It also gives writing tips for how they're to be used in-scenes.

**IMPORTANT:**
When testing for enum values in if statements or passing them into methods the text you use will usually need to be case-sensitive and match exactly. Enum values are *always* written in ALL-CAPS.

----
### Age

All characters have an age, although not all options are available for all characters. Age has a small effect on attraction.  Male NPCs can be any age, but female ones, including the PC, can be no older than their thirties.  

Age is also checked for dialogue or text that references age differences: typically with an old man and a much younger player-character.

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
- Some scenes distinguish between using "girl" or "woman" to describe the PC based on her age. Typically late-teens or early-twenties use girl, as does late-twenties if she has the cute trait. 
- If a male NPC is using "rough content" and he is in his thirties and the female is younger she may address him as "daddy".
- For the PC, bear in mind that a *transformed* character might have originally been much older, so a "late teens" PC could have many decades of life experience despite looking like a teenager.  Alternatively, they could have been a naive 19 year-old beforehand too. It's in general a bad idea to write content based on the PC's pre-game life and this is no exception.
- For `LATE_TEENS` descriptions like "barely legal" or "just over the age of consent" should probably be *avoided* as the age of consent for real-life sex in the UK is 16 even though characters in adult content must be 18.

**DEVELOPER'S NOTES:**
- I've been asked to allow players to customise attraction to ages and while I have higher priority things for the time being I wouldn't rule out traits that modify attraction getting added in the future.
- I have had some requests to open up older ages for female characters, and may do so in the future. For the time being though you shouldn't worry about writing for characters that can't exist in the current version of the game.

**FUNCTIONS:**
- [getAge](Context-Objects#getage-string)
- [getAge](Context-Objects#getage-int) (Baby)
- [getAgeDesc](Context-Objects#getagedesc-string)
- [isOlderThan](Context-Objects#isolderthanstring-age-boolean)

----
### Breasts

For the `getBreasts` method for [PC](Context-Objects#getbreasts-string) and female [NPCs](Context-Objects#getbreasts-string-1).

The possible values along with their associated descriptions are:

| ENUM | Scope | Description | Notes |
| :--- | :---- | :---------- | :---- |
| `SMALL` | PC/NPCs | small but perky tits | |
| `MEDIUM_SMALL` | PC/NPCs | pert tits | |
| `MEDIUM_LARGE` | PC/NPCs| full breasts | |
| `LARGE` | PC/NPCs | heavy breasts | |

**NOTES:**
- There's often cause for unique content or text based on the player or NPC's breast-size, from descriptions when an NPC touches them through to low-self-esteem characters feeling insecure about their size.
- Adjectives like pert, perky, full and heavy do *not* have to be restricted to that particular breast size, and you should feel free to use them for other sizes in your writing if it's appropriate to do so.
- When writing about breasts, you may also want to consider the [isLactating](Context-Objects#islactating-boolean) method and the `SENSITIVE_BREASTS` trait.
- If you're writing about whether her nipples are erect or not then you should check her *arousal* ("comfort" level or higher can have erect nipples).
- Clothing also has a large impact on descriptions of the PC's body, especially things like breasts where you may need to consider her bra and top status and whether her top (if worn) is `LOWCUT`, `THIN` or `SHEER`.

**FUNCTIONS:**
- [getBreasts](Context-Objects#getbreasts-string) (PC)
- [getBreasts](Context-Objects#getbreasts-string-1) (NPC)
- [getBreastsDesc](Context-Objects#getbreastsdesc-string) (PC)
- [getBreastsDesc](Context-Objects#getbreastsdesc-string-1) (NPC)
- [getLikesBreasts](Context-Objects#getlikesbreastscontextfemalenpc-boolean) (NPC)
- [getDislikesBreasts](Context-Objects#getdislikesbreastscontextfemalenpc-boolean) (NPC)
- [getLikesPlayersBreasts](Context-Objects#getlikesplayersbreasts-boolean) (PC)
- [getDislikesPlayersBreasts](Context-Objects#getdislikesplayersbreasts-boolean) (PC)
- [isBreastsExposed](Context-Objects#isbreastsexposed-boolean) (PC)
- [isBreastsExposed](Context-Objects#isbreastsexposed-boolean-1) (NPC)
- [isBreastsLargerThanPc](Context-Objects#isbreastslargerthanpc-boolean)
- [isBreastsSmallerThanPc](Context-Objects#isbreastssmallerthanpc-boolean)
- [isLactating](Context-Objects#islactating-boolean) (PC)
- [isLactating](Context-Objects#islactating-boolean-1) (NPC) 



### Character Type

Used only by female NPCs, and generally more important for them than
Personality. In fact, I feel that I probably should have used a
character-type analogue for all NPCs instead. However, there's a lot of
content & game mechanics written around personality at this point, and I
don't feel it's a worthwhile use of time to rework it all.

Despite this, Female NPCs do have a personality variable and this does
have an effect. For instance a selfish+innocent NPC will sometimes talk
about how she wants men to buy her presents. Character type affects
which personality will be chosen and may block some entirely. See below
for details: you don't need to write content for charType+personality
combinations that can't occur in-game.

There are currently 3 available female character types. It's possible
that more may be added in the future, but that isn't something you need
to be concerned about in your writing.

Character type affects the character creation algorithm quite a lot. The
NPC's age is heavily affected as well as her personality and traits.
However, it's worth considering all valid combinations even if they
mostly just occur in custom characters. That said, while your scene
shouldn't outright break if an NPC turns out to be a sophisticated
teenager it might not be the best use of your writing time to add
extensive paths for rare or custom-only combinations.

Any character type can in theory be a virgin but the chance is heavily
influenced by charType. Sophisticated will only be a virgin if they're a
custom NPC, party-girls have just a tiny chance (even though there's a
friendship scene that's only accessible for PG virgins) while Innocent
are likely to be virgins.

PARTY\_GIRL:

Can have any personality although jerk & selfish are more common.
Party-girls love drinking and having fun. They lack the sexual
confidence of a Sophisticated NPC but will tend to be quite promiscuous
because they tend to have drunken hookups.

Party-girls have a sort of brash insecurity that leads them to
constantly try to be the centre of attention and prove how "wild", "fun"
and "crazy" they are. This is very relevant in the party-girl-virgin
scene where she feels bad about being a virgin because it conflicts with
the way she wants people to see her.

Party-girls can be a bit judge-y of the PC if she's more straight-laced.
They can also come across as a bit self-centred.

While the current content doesn't go into too much depth with different
personalities, if you're writing extensive PG content you should
consider how those would affect her behaviour, although also bear in
mind the influence of relationship-levels.

Jerk+PG would be the stereotypical "bitchy party-girl", Selfish would be
the one who expects everyone to give her attention all the time. Average
might be a more balanced realistic character who likes to be seen as
crazy but can mellow out if it's important for her friends. Caring would
want to share the fun times with her friends and people she likes while
romantic is the girl who has a facade of being the wild partier but
secretly wants someone to sweep her off her feet.

INNOCENT:

The stereotypical sweet & innocent character. Usually younger but this
isn't a fixed rule. These characters will never have the Jerk
personality but can be Selfish. Innocent NPCs are often virgins, but not
always, and this can change in-game.

Innocent NPCs will often look up to the Pc to guide them. A 'good' PC
might help teach them the ways of the world, take care of them and
protect them from being exploited. Of course it's also possible for the
PC to be just as innocent and naïve as an NPC, or for her to let her be
exploited or even encourage it.

Selfish innocent NPCs are more manipulative and interested in using
their looks and sexuality to get what they want, but in a bit of an
immature fashion. The "I want a man who buys me nice things" approach
rather than a selfish Sophisticated's "A relationship is about what I
want, and he's going to be my bitch". A caring innocent would be sweet
and loving, while a romantic one would the soft of girl who's always
dreaming about her future fairytale romance.

SOPHISTICATED:

A sophisticated NPC is a confident woman. She's talented and successful
and she knows it. Comfortable with her sexuality, she knows what she
wants and isn't shy about going for it. Samantha from Sex and the City
might be an example, although it's many years since I've seen the show
so I can't be entirely sure.

Sophisticated tend to be older (the default chargen algorithm will never
create them in their late teens) and will normally not be virgins. They
never have the Romantic personality.

Sophisticated NPCs are also usually quite skilled both socially and in
their areas of interest. An outgoing but socially awkward woman would be
better as a party-girl.

A Jerk sophisticated would be a cruel woman, using her force of
personality to hurt others socially: she might sleep with a rival's
boyfriend just to humiliate her or date a man in order to tear him down
and leave him miserable. The marriage of an evil heart and a
sophisticated NPC's formidable social skills makes for a terrifying
prospect.

A selfish sophisticated is a woman who's focused only on what she wants,
and uses other people to get it. Her force of personality makes it easy
for her to dominate her partners and often her friends.

An average sophisticated is, like many average-personality characters, a
less-defined more middle-of-the-road character. She might take advantage
of someone to get what she wants, but unless she dislikes them she'd try
to arrange matters so they end up happy too. A selfish sophisticated
might pick up a man she fancies, take him home, get him to get her off
and then kick him out and let him walk back to town alone. An average
one would take him home but would get him off as well, maybe let him
stay the night, and put him in a taxi home the next morning.

A caring sophisticated could be a protective 'big sister' figure. She's
usually the most confident in a social group and she uses that
confidence and her social skills to look out for her friends. She's
still very assured that she knows best, so she might try break up what
she sees as a bad pairing or push her friend to get together with a man
she things will make a good partner for them. She'd often take pity on
someone who looks pathetic or helpless. For instance if she sees that a
shy and insecure man is miserable due to striking out then she might
teach him how to get with a girl he likes or, if she finds him
acceptably attractive, take him home herself.

### Clothing Flag

All clothing items can have flags. However, not all flags are applicable
to items in every slot. Flags are checked via the clothingitem hasFlag
method. You cannot modify a clothing item's flags in a custom scene.

These are the flags that may be relevant in writing. There are a few
others, but they're used only to affect game mechanics and shouldn't
need to be referenced directly.

CLINGY: refers to especially clingy clothing. Just upper/lower-body
items.

DANCE: used for the special dance dress won in the tournament.

ILL\_FITTING: Used for the ill-fitting clothing items that may be part
of the PC's starting wardrobe.

LACY: used to distinguish between lacy & plain bras and panties. Usually
does not need to be referenced directly in scene as the item's short
description will usually include it.

LOWCUT: Upper-body clothing only. Shows off more cleavage and may be
worth referencing if e.g. an NPC is staring at the PC's tits. Lowcut
tops may allow him to get a hand inside and feel her breasts even
without removing the top first.

LOW\_RISE: for certain types of trousers etc. Has small description/stat
effects but is unlikely to affect your writing.

NO\_UNDERWIRE: Bras only. Check this if your text mentions the bra's
underwire and have an alternative line if it's set.

PULL\_DOWN: Used for trousers like yoga pants which can just be pulled
down without undoing them first, and also don't have an "unzip & reach
inside" option. Only appears on non-skirt lower-body clothing

SEE\_THROUGH: Refers to sheer items that are in some way see-through or
partially see-through. Currently only used on dresses and tops.

SHOWS\_BUM. For thongs and g-strings. A new addition and not heavily
used. Principally there so if a guy ejaculates over her behind while her
underwear is still on the player doesn't get text about her underwear
being covered with the stuff.

SHOWS\_TUMMY: For tops. Currently this refers to crop-tops but in time
it might include things like dresses with cut-away sections to show the
PC's stomach.

SILK: Used by Pjs only, and is mostly just there to make it easier to
create matching sets – I don't think any scenes mention it directly.

SINGULAR: For items that can be either singular or plural. E.g. "a
g-string" vs "a pair of panties" or "a skirt" vs "a pair of jeans". Tops
and Bras are always singular so you don't need to write alternative
text. Legwear has separate singular/plural methods depending on which
you need.

THIN: This fabric. May be worth mentioning in e.g. text that determines
if her nipples show through her clothing. Can appear on most clothing
items except bras and legwear.

### Clothing Status

The PC and female NPCs have a clothing status for each of the 5 clothing
slots, although only WORN and OFF are valid for legwear so there's a
boolean isLegwearWorn method instead of the enum getLegwearStatus.

If you just need to find out if her breasts or pussy are exposed then
the isBreastsExposed and isPussyExposed methods will be simpler than
checking for clothing status. The latter also checks for the
no-panties/short-skirt situation which counts as exposed regardless of
clothing status.

Note that dresses and similar clothing cover the Top and Bottom clothing
slots and have separate statuses for both. For instance a dress that's
been pulled down around the pc's waist would have top status of EXPOSED
but could still have a bottom status of WORN if it hasn't been pulled up
to her waist. Removing a dress completely by setting either status to
OFF will set both statuses.

It's possible to set statuses via appropriate methods (e.g.
setBraStatus(String status)). You should be careful when using these to
replace clothing as it'll cause bugs if e.g. the outfit didn't include a
bra but you set the bra status to anything other than OFF. This is the
cause of the "he removes your no panties" type bugs that occasionally
crop up.

To dress the player use the fixClothing method instead. In general, you
should always check statuses before modifying them. For instance, if you
want the PC's clothing to be dishevelled after she gets groped make sure
to check it wasn't EXPOSED or OFF first.

As a rule of thumb, undressing the PC should also be approached with
caution due to its heavy reliance on the perhaps over-complex clothing
system. The NPC makeout-action can be used to get default actions
allowing NPCs to undress the player.

Statuses are:

WORN: The clothing item is being worn as intended.

DISHEVELED: Generally set after the PC gets groped. It has little in the
way of gameplay effect but modifies her description. Disheveled clothing
still covers whatever it was supposed to cover. Note that the enum value
is spelt with 1 'L', which seems to be the US-English spelling. Using
dishevelled with 2 'L's will result in an error. Not applicable for
legwear.

EXPOSED: The clothing has been moved aside (the exact description of how
depends on the clothing item) and no longer covers whatever it was meant
to cover. Not applicable for legwear.

OFF: the clothing slot is empty, either because the outfit has no
clothing for it or because the clothing has been removed completely.

### Figure (female)

There are only 3 female body-types currently used by the game, although
I don't 100% rule out adding more in the future. There are actually 7
defined in the code (SKINNY,SLIM,TONED,WOMANLY,AVERAGE,LARGE,FAT), but
as only the main 3 will actually appear on characters there's no point
in writing content for the others.

The 3 body-types all represent various flavours of "conventionally
attractive". There isn't a properly-implemented body-type for
underweight or larger-than-average characters.

Figure does not describe the character's height. That's something that's
currently unspecified. I may or may not add height at a later date – it
isn't a high priority at the time of writing.

There isn't a separate variable for the PC's bottom and I don't intend
to add one – figure is a good enough approximaton. As such, you should
use it to choose text describing her bum. E.g. "tiny bottom"/"curvaceous
rump"/"firm arse" for slim/womanly/toned. There isn't a set method to
return a bottom description at the moment so you'll need to write your
own using an \#if statement if one is needed.

SLIM:

A slender and delicate figure. Initially the weakest figure but this can
change if the PC trains fitness so should not be assumed.

TONED:

A healthy fit physique, slim with lean muscles.

WOMANLY

An hourglass body with pronounced feminine curves (but still a flat
stomach). This one can be a bit tricky to write for as words like
"curvy" are often used for "BBW" body-types. I tend to use "curvaceous"
or "hourglass" instead.

### Figure (male)

Male figure will often affect descriptive text and may affect dialogue.
You can't assume the PC is attracted to /turned-off by any particular
body type as this is customisable in character creation.

Instead, use the PC method likesFigure(String figure) or
dislikesFigure(String figure). These will return a true/false value
depending on whether the PC likes or dislikes that body type. If the PC
is neutral towards a body-type then both will return false.

This lets you have different text depending on attraction & preferences.

For example, high attraction + muscular body type + likes figure might
say something like "You feel a heat rise in your lower belly as you
admire his magnificently muscled body".

High attraction + disliked body-type might instead say something like
"despite his regrettably over-muscled body, you feel yourself becoming
turned on as you look at him". Neutral would then have an alternative
version that doesn't mention his body.

This can lead to many different combinations of text being needed, but
that has the advantage of providing a more unique description that
highlights the PC's feelings towards that specific NPC.

There are a few methods related to body type. The male NPC method
getTorsoDesc outputs a text snippet like "broad powerful chest" or
"thickset body". This is set based on figure and will always be the same
for NPCs with the same body type. It's a non-capitalised string without
spaces before or after.

Another is the getHandAdj() method. This provides a 1-word adjective
used to describe a male NPC's hands or fingers. Again, this will always
return the same result for a given body-type.

The body types and their associated torso descriptions and hand
adjectives are:

AVERAGE: "unremarkable body", "masculine".

SKINNY: "skinny torso","bony".

TONED: "toned body", "strong".

MUSCULAR: "broad powerful chest", "powerful".

THICKSET: "thickset body", "large".

PAUNCHY: "flabby body","fleshy".

FAT: "bloated fat body","chubby".

### Game Flag

Game-wide true/false flags that are stored indefinitely. These need to
be defined in the code so you can't create your own on-the-fly. However,
if one is needed for your submitted content then I can add it when your
scene's integrated with the main game.

Scene-level flags can be used to communicate information between scenes
in the same chain, so this is only used when something will need to be
saved for future weeks. For example, if a random event should only occur
once then its scene will set a game-flag that prevents it firing again.

I haven't listed all game flags here as most of them are used to store
information about specific scenes and won't really be relevant for new
content and would just be bloating the file. For example the bakery
event has 4 flags to store which choices the player makes. If your scene
needs to branch off of a specific one and has to know what decisions the
player has made then make a comment and ask for the relevant
information.

A major use of flags is to store how the PC lost her virginity – this is
used in the art gallery scene where she talks about it to a friend. This
only gets set if she loses it in-game, of course. Female-start
characters who weren't virgins to begin with don't get this.

General information about her first time: more than one can be set at
once.

FIRST\_TIME\_DRUNK

FIRST\_TIME\_CAME\_INSIDE

FIRST\_TIME\_CAME\_INSIDE\_UNSAFE: ft\_came\_inside is also set when
this happens.

FIRST\_TIME\_ORGASM

FIRST\_TIME\_ENJOYABLE

Position/situation for her first time. No more than 1 of these gets set.

FIRST\_TIME\_STANDING\_FRONT

FIRST\_TIME\_MISSIONARY

FIRST\_TIME\_COWGIRL

FIRST\_TIME\_DOGGY

FIRST\_TIME\_STANDING\_BEHIND

FIRST\_TIME\_CONCERT

FIRST\_TIME\_SEX\_SHOP\_COUNTER

FIRST\_TIME\_ELECTRO\_COUCH

FIRST\_TIME\_BLACKJACK

Some game flags related to various scenes or similar: mostly listed here
as an illustration of how they're used as you're unlikely to need these
in your writing.

TOLD\_IVY\_PREGNANT: cleared when the PC gives birth. Used to restrict
the visit-Ivy activity.

DONE\_DANCE\_CONTEST: set when the PC competes in a dance context.
Modifies the intro text to that scene in subsequent attempts.

DANCE\_CONTEST\_TORE\_CLOTHING: Yeah, you know what this is for ;)

SALES\_GROPEY\_CLIENT\_HAD\_MEETING

SALES\_GROPEY\_CLIENT\_INVITED\_HOME

MET\_LOWLIVES

SCARED\_LOWLIVES: if this is set they should be afraid of the PC in
subsequent meetings.

KNOWS\_ABOUT\_TREASURE: for the treasure-hunting scene.

FOUND\_TREASURE

GOT\_PAST\_TREASURE\_RIVAL

DONE\_INNOCENT\_BONDAGE\_SCENE: used to restrict the scene to once/game.

REPLACED\_INNOCENT\_FOR\_BONDAGE: Indicates that the PC participated
properly.

MET\_HORSE

NO\_MORE\_GYM\_THREESOMES: Can be set in the scene where Horse becomes
dateable, depending on the PC's choices.

DEFEATED\_OFFICE\_RIVAL: Setting this will block the events where the
rival tries to mess with the PC. If the rival is told to quit the
company then she's also given the DISABLED trait.

Flags related to game control:

DO\_PROPOSAL: Triggers a proposal from the BF. There are some fairly
specific conditions around proposals so it's probably best you don't set
this.

HIDE\_TRAITS: set in the 'secret' starts, affects what's shown in the
character screen. Does not need to be considered in written content: the
player is supposed to be able to figure out their stats from game text.

PILL\_SABOTAGED: Indicates the player's contraception has been sabotaged
that week. Reset on a weekly basis when impregnation is processed. Set
this if your scene involves the PC's pill getting tampered with. You
should also check if it's set before an NPC attempts such tampering, so
he doesn't keep trying over and over until he's caught even after
succeeding.

For custom scene testing:

TEST\_FLAG: Never used in the main game. Intended for use in custom
scenes where it'd be replaced by a new one when said scene is integrated
into the game.

TEST\_FLAG2, TEST\_FLAG3: More test flags for custom scenes that need to
set several different ones.

### Hairstyle

All characters have a hairstyle. Hair length is a component of hairstyle
and is not stored separately. All hairstyles are technically valid on
all characters even though the game won't give "male" hairstyles to
female characters or vice-versa.

"Male" styles:

BALD

SHORT\_HAIR

SHOULDER\_LENGTH\_MENS\_HAIR

MAN\_BUN

"Unisex" styles:

AFRO

SHAVEN\_HEADED

MULLET

"Female" styles:

SHORT\_BOB

PIXIE\_CUT

BUN

SHOULDER\_BOB

SHOULDER\_STRAIGHT

WAVY\_SHOULDER\_LENGTH

PONYTAIL

PIGTAILS

LONG\_PONYTAIL

LONG\_HAIR

WAVY\_LONG

### Length

For lower-body clothing. Newlife supports 3 lengths, although the
descriptions sometimes vary on specific items. In particular wedding
dresses use the knee-length setting to refer to tea-length dresses
(which are actually a bit longer than knee-length ones IRL) and do not
have knee-length variants.

THIGH: Skirts etc that go down to the player's thighs. i.e. short ones.

KNEES: Knee-length skirts etc

ANKLES: Long skirts/trousers/etc

### NPC Behaviour

NPC behaviour is set for all NPCs when the scene starts, based on
personality, relationship levels and some traits. It's usually best to
use behaviour rather than raw personality to control an NPC's behaviour
towards the player. NPC-NPC interactions have to use personality as they
don't have relationship levels.

Behaviour will not vary within a scene chain so you don't need to write
content for that: for instance if a certain action is only available
when an NPC was being NICE or ROM(antic) then you don't need to have
follow-up content that checks for AVG, COLD or MEAN.

There are some situations where character with a different personality
might act differently despite having the same behaviour though. A common
example is the Jerk personality. After some criticism early after
release that jerks were just acting like assholes for no reason I
decided to write content to imply that they're sexist towards women.
This is an old-fashioned "women belong in the kitchen" type of
chauvinism. Thus a jerk might need different mean text (where it implies
he looks down on the PC for being a woman) compared to another
personality (who'll be being mean because he just doesn't like her). Of
course it's possible for a jerk to dislike the player too – you can
check liking directly on the NPC object if necessary for your writing.

It's possible for an NPC to 'fake' their behaviour if they want
something from the PC. Most scenes will want to use the behaviour that
allows faking, but the getBehaviourNoFaking() method lets you get it
without faking. You should use the no-faking method if the NPC is in a
situation where they wouldn't pretend just to sleep with the player, or
in sexual situations where they're already getting what they want.
Typically makeout & sex scenes should use no-faking: he starts showing
his true colours and the PC has to decide if she wants to say something
at such an intimate stage.

Faking takes into account traits, drunkenness and a few other things.
NPCs will also stop faking once they've got what they wanted. This is
usually to have sex with the PC at least once, but impregnators will
fake until they get her pregnant.

There are broadly 2 types of faking: charming NPCs will fake the
Romantic behaviour, and any (non-crude) NPC can fake the 'average'
behaviour if they'd otherwise be mean as long as they meet the criteria
for faking.

Behaviour should not stop an NPC from sleeping with the PC – check
attraction for that. Cold behaviour sex should imply that he's just
using her for sex, while mean behaviour will tend to be rough,
aggressive and/or cruel.

Female NPCs use the same behaviours, although their interactions with
the PC tend to be more limited due to not being date-able.

Behaviours are:

MEAN: The NPC is rude and unpleasant towards the player. Common for
Jerks. Other personalities need to dislike the PC. Never chosen by
caring NPCs (aka the best personality!)

COLD: The NPC is cold towards the player and might have sex with her but
won't show intimacy or treat her with much respect. Jerks always choose
mean instead. Common for selfish but average and romantic personalities
can pick it too. In particular, average personality is cold towards
strangers. Never chosen by caring.

AVG: Average. A default "polite" behaviour where he won't go out of his
way to be nice but won't be a dick either.

NICE: The NPC will go out of his way to make the PC happy. This appears
if he likes her a lot but is not in love with her. At maximum levels in
all relationship facets the romantic behaviour is used instead.

ROM: Romantic. Can be used by any NPC at high love levels (or low love
levels, for romantics) and overrides other behaviours, so love+dislike
will still be romantic. Can also be faked by Charming NPCs which should
make them popular with pcs who have the romantic trait.

### NPC Personality

NPC personality has a significant effect on how they behave in scenes.
However, it's often better to check NPC behaviour instead as it also
takes relationship levels into account. There are still some situations
where personality should be checked directly though.

JERK:

The NPC is a jerk who enjoys being mean to people. Male jerks are
chauvinistic and have a "women belong in the kitchen" attitude. This can
be relevant even when he's being nice to her. For instance there's a
section in the anniversary scene where he gets her cooking gear due to
this assumption and the PC has the option to get angry at him.

Jerks should also approve of the PC being bitchy to third parties and
may team up with her to be horrible to other people.

SELFISH:

Selfish NPCs care only about themselves. It's harder for them to fall in
love and they should avoid going out of their way to help other people
unless they have strong feelings for them: this is generally taken into
account in the behaviour system which has them choosing the COLD
behaviour until high relationship values.

NPC finances aren't especially well-developed at the moment, but I have
some long-term thoughts around having Selfish NPCs approve of a
transactional approach to romance which might make a wealthy selfish man
a good choice for a gold-digger PC.

AVERAGE

The name says it all really.

ROMANTIC

Romantic NPCs should like romantic behaviour from the PC more, but only
if they're interested in reciprocating (love of at least SOME or high
attraction). While not heavily implemented in game I tend to think of
them as the sort of person who could get excessively clingy.

CARING

The 'best' personality. They're generally nice and supportive to the PC
and to other people in general.

### NPC Traits

NPC traits cover a wide variety of things, from very specific ones that
are only relevant in a particular scene chain through to fundamental
traits that get checked over and over throughout the game.

It's a good idea to familiarise yourself with the key traits that will
affect your scene and consider how they might need their own content and
how they might interact with the PC's traits or with their relationship
status. For instance a scene where the PC sees a male NPC naked might
not only need to consider the THICK\_COCK trait in his description but
also to have some reaction text if the PC has the LIKES\_BIG trait.

Traits are divided into male-only, male-or-female and female-only
categories. As lesbian dating isn't implemented in Newlife many
"male-or-female" traits that relate to attraction have little or no
effect for female characters however. They might still be relevant on
occasion though, for instance if the PC is asking her friend's advice on
how to dress or act.

In most situations you don't need to write for characters that can't
normally be created by the game: notably if they have opposing traits
(e.g impregnator + conscientious).

Male Only

BIG\_BALLS

The man has large testicles and ejaculates more than usual. This should
usually modify his orgasm text and any writing that involves interaction
with his balls.

BIG\_COCK\_HEAD

The tip of his cock is unusually large and bulbous. Generally affects
its description but can also modify penetration text.

CHARMING

Charming NPCs are more 'smooth' and may need different interaction text.
They can also 'fake' the romantic behaviour and should generally be
well-liked by PCs with the romantic trait.

Opposed to sleazy, crude, taciturn.

CHEATER

No opposites. The NPC is more likely to cheat and may do so without
having a reason (as of 0.4.23 non-cheaters will only be unfaithful if
they're angry at the PC, which is only set on some paths in the scene
where she's caught cheating herself).

Normally only appears on selfish (most common), jerk or average NPCs, so
you don't need to write content specifically for caring/romantic +
cheater.

The trait can usually be ignored unless your scene specifically relates
to infidelity.

CONSCIENTIOUS

These men are more careful about using condoms and will also react well
to the PC using them and dislike it when she encourages risky behaviour.

When writing how an NPC feels about not using condoms, consider the
situation. In a serious relationship they might be more accepting of
having children, especially if they have the wants\_kids trait and not
its opposite. They should also be accepting of not using a condom if the
PC is on the pill or already pregnant.

Opposed to hates\_condoms, impregnator.

COOKING\_TEACHER

Special NPC trait for the teacher in the cooking class scene. Will not
be chosen as a random NPC for general scenes but can date the PC and end
up in a relationship with her.

CRUDE

A leftover from the old dialogue system, and a trait that I considered
removing but (mistakenly) decided to keep. You can see more discussion
of this here:

<http://splendidostrich.blogspot.co.uk/2015/08/sleazy-crude-and-boastful.html>

Crude mainly modifies dialogue. Refined PCs should generally dislike
spending time with crude or sleazy men.

Opposed to Charming

DANCE\_JUDGE

The NPC is the judge for the dance contest. Otherwise they're basically
a normal NPC and can show up at the club. The default dance\_judge is
always in his 40s or older, of selfish or average personality and a good
dancer.

DANCE\_STUDENT

The NPC is a student at the dance class. These NPCs always have the
good\_dancer trait. While not technically opposed to the other special
roles they're generated mid-game and will never have them, so that isn't
a situation you need to write for.

DANCE\_TEACHER

The teacher at the dance class. Always has the good\_dancer and
fashionable traits. Generated mid-game like the dance students.

DIVORCED

Added to the sales boss if he tells the PC he's finally divorced his
wife during a proposal scene, and used to prevent mention of his
marriage afterwards. A bit of a stop-gap: NPC relationships may get
handled in more depth later. Has no effect for anyone except the sales
boss.

DOORMAT

The doormat trait affects how an Npc should react to cheating. NPCs with
this trait will be upset about their partner cheating on them, but won't
stand up for themselves. They should never dump the PC for cheating.

If you're writing a doormat-specific path then consider having content
where they get belittled, shamed or humiliated by the PC, especially if
she has the bitchy trait.

FASHIONABLE

The NPC likes fashion and dresses in a more flamboyant manner. Mainly
relevant if your scene involves shopping together or the like.

FRIEND\_IMPREGNATOR\_ADVICE

Hidden trait used to flag up the NPC picked for the bitchy+impregnator
scene chain so the same one is chosen for its follow-ups. Unlikely to be
relevant to your writing.

GYM\_JERK

A special-NPC trait. The various special roles are all opposed to each
other and you can assume no NPC has more than one. This flags up the
special NPC who takes the PC to the changing-room makeouts with his
friend Horse. You usually won't need to check this trait unless you're
doing some Horse+jerk specific writing.

The gym jerk is heavily restricted in his traits etc. Among other
things, he always has both MISANTHROPE and COLD\_HEARTED. This is a
combination that won't be generated by the normal algorithm (as the
traits are usually limited to jerk & selfish personalities respectively)
but because of this NPC and potential custom ones it's a combination you
may need to consider in your writing. Of course those traits normally
don't need to get special content written for them – their primary
effect is to affect love/liking gain.

HANDSOME

The NPC is facially very handsome, and gets a bonus to his
attractiveness. This is handled in the various isAttraction methods.

Handsome NPCs may sometimes need special text. Also, if you're writing
content that assumes he is or isn't successful with other women then
it's one of the traits you should check for. I generally assume that
handsome, charming, toned or muscular NPCs have little trouble hooking
up with women so these need to be checked for if you're writing about
that sort of thing.

Opposed to Ugly.

IMPREGNATOR

An 'evil' trait that's intended to be hard-to-find: it has a very high
knowledge threshold. Impregnators will try to get women pregnant through
underhanded means such as sabotaging contraception.

Impregnators can have either wants\_kids, doesnt\_want\_kids or neither.

If they don't want kids then the idea is that they want to knock up the
PC but then leave her to be a single mum. As such, if they're in a
committed relationship with her and would want to stay together (check
Love for this) then they'd stop their efforts to fertilise her because
they don't want to have to raise a child.

The impregnator trait is only added by default to Jerk characters.
Custom NPCs may have it on other personalities but as a rule of thumb
you shouldn't bother writing unique content for combinations that won't
occur naturally in the game.

Impregnator is opposed to conscientious, likes\_anal and likes\_oral.

INFERTILE

The NPC cannot get the PC pregnant. Only appears on custom NPCs. Like
the PC trait, the NPC may not know about this. As such it shouldn't get
unique written content. This trait is handled in the impregnation
calculations so unless you're writing a scene in a fertility clinic or
something you won't need to worry about writing for it.

IS\_HORSE

Special character trait that flags this character as being the NPC
'Horse'. Horse is massively restricted in traits, appearance and
personality – probably more than any other NPC. Initially he's
restricted to the changing-room scene but can eventually become
date-able.

LIKES\_COOKING

NPCs with this trait can appear at the cooking class, enjoy cooking more
and are better at it. Unless your scene involves cooking it usually
won't be important for you.

LIKES\_TO\_SHARE

NPCs with this trait are happy with the idea of their partner sleeping
around. They won't get upset if she cheats and will be turned on to hear
stories about her hooking up with other men.

LONG\_LASTING

The NPC will take longer to finish when having sex.

LOWLIFE

Special character trait that flags this character as being a lowlife
that can abuse the PC and her friend in one scene. Lowlives are always
restricted to their own scenes.

LOWLIFE\_BF

Hidden trait that's set if a lowlife has a "romantic" moment with the
innocent friend. Only 1 lowlife can ever be assigned this trait in a
game. The matching innocent NPC gets INNOCENT\_WITH\_LOWLIFE\_BF.

NASTY\_SPERM

The NPC has unpleasant, foul-tasting sperm. The PC should lose Enjoyment
if he finishes in her mouth. Mostly just relevant in that situation.

PORN\_ACTOR

Trait used to identify the special NPC that can show up in the
porn-shoot scene. The NPC is limited to that scene so you needn't check
for their presence among randomly selected NPCs.

QUICKSHOT

The NPC will finish faster when having sex.

REPAIRMAN

This is a special NPC who can show up in the relevant scene. These NPCs
can show up in random scenes.

SALES\_BOSS

This is the PC's boss in the sales career which, at the time of writing,
is the only one.

SALES\_PERVY\_CLIENT

This is the perverted client that can grope the PC at her sales job.
Only appears in his own scenes and is only relevant there.

SALES\_SLACKER\_FRIENDSHIP\_NPC

A friendly old man that the PC can slack off on her job with. Only
relevant in his own scenes.

SLEAZY

See:

<http://splendidostrich.blogspot.co.uk/2015/08/sleazy-crude-and-boastful.html>

The sleazy trait means the NPC is quite sexual and will often talk about
it to the PC. This is disliked by Refined PCs but turns on those with an
overactive-imagination. Sleazy men get access to various 'pervy' date
actions such as bringing the PC to a porno theatre.

Opposed to Charming.

SMALL\_COCK

Opposed to THICK\_COCK but not to BIG\_COCK\_HEAD.

Should usually be checked in descriptions of the NPC's penis, especially
for PCs who like larger men. Such a PC will usually be less turned-on by
actions involving his penis.

The BIG\_COCK\_HEAD trait counteracts this and PCs who like big men
should generally consider small cock + big head to be neutral or
slightly positive.

TACITURN

The NPC doesn't speak much. Most NPC speaking actions should check for
this trait first. Non-speaking actions that involve speech can sometimes
be improved by checking for this trait and replacing the speech line
with one involving gestures or the like.

Opposed to Charming and Boastful.

TASTY\_SPERM

The NPC's sperm is particularly delicious. The PC should gain enjoyment
if he finishes in her mouth. Opposed to NASTY\_SPERM (obviously).

THICK\_COCK

The man's cock is especially thick. This should be considered in
descriptions of how it looks or feels. Checks for this should often also
check for the PC having LIKES\_BIG.

TRADITIONAL

Usually only appears on Jerk NPCs as it's a very chauvinistic trait.
Players can create custom NPCs that are non-jerk traditional characters,
but you don't need to write for this possibility. Traditional NPCs will
ask the PC to be a housewife after marriage, and will be fine with her
deciding to stay a virgin until marriage.

TREASURE\_HUNTER

A flag added to an NPC who shows up the the treasure\_hunter event when
it first fires. Afterwards the scene is restricted to just this NPC.

UGLY

Opposed to Handsome. The NPC is less attractive. May be worth checking
if the PC is insulting him or if you're writing text that implies he's
lonely and has a hard time dating. In the latter case also check if the
PC's sleeping with him or if he has the Charming trait or is Toned or
Muscular as those offer alternative ways of winning over women.

Male or Female

BAD\_DANCER

The NPC is bad at dancing and dislikes doing it. Opposed to GOOD\_DANCER

BOASTFUL

The NPC is a prideful and arrogant person who tends to boast a lot about
their accomplishments. This can annoy the PC, especially if combined
with Dull. However she's usually fine with the NPC boasting if they also
have the interesting trait.

Boastful also affects the character's behaviour. A boastful character
will be unlikely to do something that makes them look unsuccessful such
as asking for help. They'll also tend to be very assured of their own
superiority which means they might do things like expecting the PC to
dump her boyfriend if she gets a chance to be with them instead.

Boastful characters like it when the PC is shy & quiet because it lets
them talk about themselves.

Boastful is opposed to Taciturn.

COLD\_HEARTED

The NPC can never fall in love: their love points are fixed at zero.
This is only rarely checked directly – normally it's fine to just check
against Love.

CUNNING

The PC's bf will never discover cheating with this NPC: equivalent to
the PC's cunning trait. This is intended for gameplay effects and you
shouldn't normally need to vary your scene's text based on it.

DOESNT\_WANT\_KIDS

The NPC does not want to have children. With impregnator this means
he'll try to get the PC pregnant but won't want to stay with her. These
NPCs should avoid situations that might land them with a kid to look
after – for example they get a penalty for asking the PC to be their
girlfriend is she has kids or is pregnant.

DULL

The NPC is very boring in conversation. This is mostly relevant in
dialogue – they can still be good in bed. Opposed to Interesting.

GOOD\_DANCER

The NPC is a good dancer: mostly just relevant in dance-based scenes.
Opposed to Bad Dancer.

HATES\_CONDOMS

The NPC hates wearing condoms and will be very reluctant to wear one,
getting relationship penalties towards pcs who try to press the issue.
Opposed to conscientious.

INEPT\_LOVER

The NPC is bad in bed. Sex and makeout content with this NPC should
result in lower arousal & enjoyment for the PC and should usually have
alternative text highlighting that the NPC is clumsy, inept or clueless
about how to please a woman (or a man, in the case of npc-npc intimacy).

Opposed to both MAGIC\_FINGERS, TALENTED\_TONGUE and LIKES\_GOING\_DOWN
so you don't need to write content for this trait combined with any of
those. Can appear on either male or female NPCs.

INTERESTING

The NPC is fun and interesting to talk to. Opposed to Dull. The PC will
like spending time with this NPC and should improve relationship facets
when she does.

LIKES\_ANAL

Opposed to LIKES\_ORAL and PREFERS\_SEX: the NPC only gets (at most) 1
sexual activity preference. Also opposed to IMPREGNATOR as he can't
knock someone up via anal.

The NPC should like anal or related things like the PC talking about
enjoying it. They should be keen to initiate it given the opportunity.

Before writing any anal content, check \$gd.allowAnal. It's possible for
a game to have NPCs with this trait even when the option is false. This
includes things like characters talking about liking anal sex.

LIKES\_BIG\_TITS

The trait name should be self-explanatory. An NPC can have at most one
breast-size preference, and may have none. Typically you would use the
likesBreasts and dislikesBreasts methods instead of checking for this
trait.

LIKES\_CASUAL

The NPC likes 'casual' girls and dislikes ones who give themselves airs.
They should get on better with DOWN\_TO\_EARTH PCs and worse with POSH
or REFINED ones. They should also have preferences on the PC's
casualness/elegance scale.

This is often worth checking if he's giving her compliments or insults.
However, it is already taken into account for attractiveness
calculations so you don't need to make additional checks there. Opposed
to LIKES\_ELEGANT.

LIKES\_CUTE

The NPC likes cute/innocent girls and dislikes ones who act overtly
sexual. They should get on better with CUTE and SHY PCs and worse with
SULTRY or FLIRTY ones. They should also have preferences on how cutely
the PC dresses. They'll also like her telling them she's a virgin or
generally acting in a 'cute' manner.

This is often worth checking if he's giving her compliments or insults.
However, it is already taken into account for attractiveness
calculations so you don't need to make additional checks there. Opposed
to LIKES\_SEXY.

LIKES\_ELEGANT

The NPC likes 'elegant' girls and dislikes ones who dress down. They
should get on better with POSH and REFINED PCs and worse with
DOWN\_TO\_EARTH ones. They should also have preferences on the PC's
casualness/elegance scale.

This is often worth checking if he's giving her compliments or insults.
However, it is already taken into account for attractiveness
calculations so you don't need to make additional checks there. Opposed
to LIKES\_CASUAL.

LIKES\_GOING\_DOWN

Can technically be added to either male or female NPCs but currently
does nothing for female ones. For male NPCs it makes them enjoy giving
cunnilingus more, always agree to the PC requesting it and lets them
initiate it from makeout scenes.

LIKES\_MED\_TITS

The trait name should be self-explanatory. An NPC can have at most one
breast-size preference, and may have none. Typically you would use the
likesBreasts and dislikesBreasts methods instead of checking for this
trait.

LIKES\_ORAL

Likes oral sex. He should be more likely to initiate it and enjoy it
more if the PC does so or talks about it.

Opposed to likes\_anal and prefers\_sex. Also to Impregnator.

LIKES\_SEXY

The NPC likes 'naughty' girls and dislikes ones who act in a cutesy or
innocent manner. They should get on better with SULTRY or FLIRTY PCs and
worse with CUTE and SHY ones. They should also have preferences on how
cutely the PC dresses. They'll like her taking overtly sexual actions
like initiating sex.

This is often worth checking if he's giving her compliments or insults.
However, it is already taken into account for attractiveness
calculations so you don't need to make additional checks there. Opposed
to LIKES\_CUTE.

LIKES\_SMALL\_TITS

The trait name should be self-explanatory. An NPC can have at most one
breast-size preference, and may have none. Typically you would use the
likesBreasts and dislikesBreasts methods instead of checking for this
trait.

MAGIC\_FINGERS

The NPC is good with their hands. Actions where they touch up the PC
should usually have alternative text for this trait and get larger
arousal increases. You shouldn't give Enjoyment bonuses just him for
touching the Pc with this trait – although perhaps increase them if the
action also matches one of her sensitivity traits.

MISANTHROPE

The NPC doesn't like other people and their Liking value is capped at
the OK level. You won't normally need to vary text directly on this
trait - check Liking or Behaviour instead.

NO\_BEFRIEND

Hidden trait that stops the NPC being befriended. Not relevant to your
scene unless you're adding friends to the PC, which isn't possible for
user-submitted scenes in the current version anyway.

NO\_RANDOM\_APPEARANCE

Prevents the Npc appearing randomly in places like the club. They can
still ask the PC on dates if they get her number. Typically used to
restrict special NPCs to their unique scenes. You won't need to check
this in your writing.

ODDLY\_UNATTRACTIVE

Hidden trait, currently restricted to custom NPCs. Caps starting
attraction. Typically you wouldn't need to check for this – it'll be
considered when you look at an NPC's attractiveness.

PREFERS\_SEX

Sexual preference trait that's opposed to likes\_oral and likes\_anal.
This was originally envisaged as a "dislikes oral" trait back before
anal was added.

This should block the Npc from initiating oral or anal scenes, although
in the current version those aren't accessible directly from custom
scenes – use a transition to a makeout instead and the makeout will
handle this trait.

It's still sometimes going to be relevant for dialogue, NPC preferences
or "mini-sex" paths.

SEEN\_DANCE\_TROPHY

Not exactly the most groundbreaking trait. This flags that they've seen
the PC's dance winners trophy and thus she can't show it off to him
again.

TALENTED\_TONGUE

The NPC is especially good at giving cunnilingus. It has no effect for
female NPCs in the current version.

TESTING\_TRAIT

Does nothing. To be used as a placeholder if you expect your content to
get its own NPC trait. Scenes that need multiple traits can also use
**TESTING\_TRAIT2 **and **TESTING\_TRAIT3**.

TROUNCED

Set when the PC beats up an NPC. I have some fairly limitations on
violence in Newlife scenes and in particular you can't submit violent
partner abuse, although of course the PC can be quite verbally abusive
with the Bitchy trait.

This trait should get set if the NPC is doing something like groping the
PC against her will and she takes the option to give him a thumping.

UNLOVABLE

Hidden trait, currently restricted to custom NPCs. Prevents the PC from
falling for this NPC. Like the Aromantic trait but just affecting one
particular person. You shouldn't need to write for this – checks for
love will already take it into account.

VIGOROUS\_LOVER

NPC equivalent of the PC's passionate\_lover trait. Has a significant
effect in sex scenes and the like.

WANTS\_KIDS

The Npc wants to have children, but this doesn't mean they're so
desperate for them that they'll try to knock up someone they just met.
They should be happier/more accepting of having children with the PC if
they're in a relationship with her but this doesn't mean they'll have a
problem with her asking for protection.

Opposed to DOESNT\_WANT\_KIDS.

Female Only

BEAUTIFUL

Female equivalent of the HANDSOME trait.

DONT\_TAKE\_PILL

Stops the NPC from deciding to go on the pill unless specifically set
via setOnPill. You also need to call setOnPill(false) if you're adding
the trait as the trait won't stop her taking it if she already is.

INNOCENT\_BONDAGE\_NPC

Set when an Innocent friend takes the PC to the bondage-club event. This
then combines with that scene's relevant gameFlags to enable the
follow-up where she thanks the PC for helping her. Not likely to be
relevant for player-written content.

INNOCENT\_ENCOURAGED\_LOSE\_VIRGINITY

Set when the PC encourages an innocent friend to lose their virginity.
Enables the follow-up scene where she asks the PC for help. Not likely
to be relevant for player-written content.

INNOCENT\_NON\_VIRGIN\_QUESTION

Set when an Innocent friend asks the PC how they lost their virginity.
Used for scene-control. Not likely to be relevant for player-written
content.

INNOCENT\_SALES\_COLLEAGUE

Identifies this NPC as the innocent sales colleague who gets her own
scene-chain.

INNOCENT\_VIRGIN\_QUESTION

Set when an Innocent friend asks the PC how they want to lose their
virginity. Used for scene-control. Not likely to be relevant for
player-written content.

INNOCENT\_WITH\_LOWLIFE\_BF

Flags an innocent female NPC who went down the "romantic" path in the
befriending scene and is now dating one of the lowlives: the lowlife in
question gets the LOWLIFE\_BF trait. These NPCs should generally not be
given content where they hook up with other men.

PARTY\_GIRL\_SALES\_COLLEAGUE

Currently unused. I have an outline written somewhere for some scenes
involving an NPC with this trait.

PILLS\_SABOTAGED

The NPC's contraceptive pills have been sabotaged and will no longer
work. This is permanent unless the trait gets removed, which does not
happen in the main game at present. Female NPCs only.

PLAIN

Female equivalent of the UGLY trait.

REFUSED\_VIRGINITY\_LOSS\_REQUEST

Set when the PC refuses to help an Npc lose her virginity: blocks future
requests.

SLEPT\_WITH\_PCS\_PARTNER

Set when the PC sees a female NPC having sex with her partner. Removed
if she breaks up with said partner. This trait makes it more likely the
NPC will be chosen if he cheats again.

TREASURE\_HUNTER\_RIVAL

Identifies this NPC as the rival in the treasure-hunting scene.

### PC Behaviours

These are valid behaviours for the PC towards a particular NPC. When
using the default behaviour-choice actions (see the yaml guide for
details on how to do this), not all behaviours will be available: only
ones suitable to the PC and the active male NPC.

Not all scenes track PC behaviour. It's your decision whether it's
worthwhile for your scene. Using behaviours gives the player more choice
about how they want to act towards an Npc than simply checking
relationship & trait levels. However, it can be a fairly heavyweight
option and may not be worthwhile if you're only using behaviour in one
or two places.

The PC's behaviour will be null if not previously set. If your scene
uses behaviours then you should check for nullity whenever the active
male NPC gets set (often in the intro) and call behaviour actions. If
using the default behaviour actions you'll also need to write an
action-response for them. See the yaml guide for more on this.

So, behaviours:

FRIENDLY

The normal behaviour for most characters: the player acts in a
reasonably friendly & polite way but without being especially sexual.
This does not mean the PC and the NPC are friends: just that she's being
pleasant to them.

FLIRTY

The PC is flirting with the NPC, but in a socially-acceptable way that
doesn't verge into overt sexuality.

SEXUAL

The PC is being overtly sexual to the NPC. This might be seen as
inappropriate in some settings, and NPCs with LIKES\_CUTE will dislike
it. NPCs with LIKES\_SEXY will enjoy this though.

QUIET

Only available to shy characters. The PC is too shy to speak much. Most
NPCs will find it annoying to talk to someone like this but BOASTFUL
ones will enjoy the chance to talk about themselves and ones with
LIKES\_CUTE might find the PC's shyness sweet.

ROMANTIC

The PC is acting in a romantic way. Characters who don't have feelings
towards her might find it inappropriate. Ones who love her will enjoy
this. Characters with the ROMANTIC personality will usually enjoy this,
as long as their love is higher than the minimum value.

CUTE

The PC is acting in a cutesy sweet-and-innocent way. The game doesn't
track if the PC is genuinely like this or if it's an act she's putting
on. As such, it's easiest to focus writing on what the Pc says & does
rather than commenting on her reasons for it.

COLD

The PC is being cold and offputting to the NPC. This is obviously rude
and all NPCs dislike it.

RUDE

The PC is being rude, insulting and aggressive. Every NPC will hate
this.

### Player Traits

Checked via \$w.hasTrait(traitName). Player traits cover all kinds of
things. Many are very important when it comes to writing. You'll often
find yourself writing alternative text for different traits and adding
trait-specific actions.

Some traits are opposed to each other, and the character creation screen
will prevent them being taken together. e.g. Plain and Beautiful or
Outgoing and Shy. You don't need to consider these combinations in your
writing as they'll never appear in-game.

Cheat Traits:

These traits indicate that the player chosen the specified cheat at
character creation.

They should not normally be used to game any significant writing – they
aren't available to non-patrons and my policy is that there shouldn't be
any substantial content that's blocked from public-version players.

Single throwaway lines are fine though, as is recognising the trait in a
short alternative action description or whatever. They shouldn't have
full passages of text, actions or god-forbid entire scenes restricted to
them though. The key question when writing is: "Could a public-version
player be reasonably disappointed not to see this content?" If the
answer is yes, it shouldn't be blocked from them.

HUGBOX

PHONE\_FUN

BIG\_SHOPS

VOW\_MASTER

PSYCHIC

Character Background Traits:

ALWAYS\_FEMALE

This trait means the player took the female-start. They might still have
been transformed (see NOT\_TRANSFORMED below) but will not have ever
been a man. Any gender-bender content must check for this trait and
provide alternative text as appropriate.

NOT\_TRANSFORMED

This means the character was not transformed in the game introduction
sequence. This only happens if they took the female start *and* said
that their age & body-type was within those implemented in the game.
Quickstart female-start characters have this trait.

NON\_VIRGIN\_START

This means the character began the game as a non-virgin. This is never
set for male-start characters but might be for female-start ones
depending on their character creation choices. It's used in-game to
block text that assumes the PC has never e.g. had an orgasm from sex
just because the stat based on in-game encounters is zero..

PORN\_STAR

Set mid-game if the PC has successfully made a porn film that's good
enough to sell. Making a bad porno that doesn't appear in the sleazy
cinema won't add this trait.

Mutation Traits

These traits usually should not affect text or descriptions: their
purpose is to have specific strictly-defined effects on game mechanics
and they are not intended to add complexity to the writing.

FECUND

Increases how fast pregnancies proceed for the PC.

UNUSUAL\_BODY\_CHEMISTRY

Gives the pill a high failure rate, although the PC seems unaware of
this in-game.

CONDOM\_DAMAGING\_SECRETIONS

Massively increases the chance of condoms breaking without sabotage.
Again, the PC and her partners do not seem to be aware of this so you
don't need to write alternative dialogue for it.

INFERTILE

Classing this under 'mutations' feels a bit rude to people with IRL
fertility issues – my apologies!

This trait blocks impregnation but the idea is that neither the PC nor
anyone else actually knows that she's infertile. As such, you should not
modify your text on it. This allows people who enjoy impregnation-risk
text to see it even if they don't like their character actually getting
pregnant. Note that characters with this trait can still get pregnant if
the player gets the fertility treatment.

MILKY

This makes it so isLactating always returns true unless lactation is
disabled in the game options. You should use isLactating instead of
checking this trait as it also handles situations where the PC lactates
despite not having the trait due to pregnancy.

Willpower Traits

The PC can have at most 1 of these. If they have 0 then that means they
have normal willpower.

You normally will not check these traits directly – use testWill
instead. However, there are some situations where you might want
specific high/low will content that a willpower test isn't suitable for:
generally when the character's arousal won't very at that point in the
scene such as when she's having an orgasm.

LOW\_WILLPOWER

HIGH\_WILLPOWER

IRON\_WILL

Character Traits

These represent how the PC appears to others. In very early versions of
the game they were "voice" traits and affected how she spoke. They've
since broadened to cover general behaviour.

The PC will have at most 1 of these. There isn't a trait for "normal".
That's just the absence of the other traits.

These traits have a big effect on the PC behaviour system. This isn't
currently available for custom scenes but I'll no doubt add it as I
extend them. It's often better to check for PC behaviours rather than
character traits directly, but not all scenes have a set PC behaviour so
that won't always be an option.

Each of the character traits provides a significant increase to the
associated cute/naughty/elegant/casual stat.

DOWN\_TO\_EARTH

The opposite of 'posh'. Associated with casualness.

I guess I must have had plans for it back in 2013, but the
poshness/casualness continuum hasn't really had as much content as the
cuteness/naughtiness one. There are some scenes where they'll matter and
it's worth checking them against an NPC's preference traits if you're
writing compliments or insults, but overall the down-to-earth and posh
traits tend to be more peripheral.

The PC probably speaks with some sort of working-class accent, but you
can't easily make assumptions about this because she isn't necessarily
even British. The intro implies that the PC is the player themselves in
the future, and only around 7% of my players are from the UK, according
to blogger stats. Just another reason to avoid directly quoted speech.

Generally should avoid snooty 'posh' events. For example, if you're
writing an event where the PC visits the opera it should probably be
blocked for down\_to\_earth or have an alternative intro where she only
goes because of her friend/date's encouragement.

Down-to-earth is opposed to the Refined trait. Of course a working-class
character could be refined – this would imply a sort of would-be
social-climber. However, I assume that such a character would hide their
down-to-earth background and would therefore have a different character
trait: probably "normal".

POSH

The opposite of down-to-earth. Associated with elegance.

The character comes across as being posh and upper-class. Again, we
can't assume this is from the *British* upper-classes.

This doesn't necessarily mean the character is obsessed with class and
status: use Refined for that. A posh character could be quite
chilled-out, but her background would be evident in how she speaks and
behaves.

CUTE

The opposite of sultry. Associated with cuteness.

Note that the cute trait has no opposites; it's possible for a character
to be both cute and flirty.

This is one of the harder ones to write for, because it isn't clear if
the character is genuinely naïve & innocent, or if she's just putting on
a cutesy act. In some cases you can be a bit ambiguous: often both would
act the same.

Otherwise, if you to assume she's genuinely naïve then that's fine for
smaller pieces of writing. For significant events such as if a guy's
taking advantage of her you should check associated traits (usually
isVirgin). If they match you can probably safely assume she's genuinely
an innocent. Otherwise it's a good idea to let the player choose: have
an action or actions that assume she's genuinely naïve but have one
where she shows she actually does know what's going on.

Cute characters should act in a stereotypically innocent, girlish way –
cuteness is kind of associated with immaturity. However, you shouldn't
have her act in a way that implies she's pretending to be underage –
this is something that will make quite a few players uncomfortable.

SULTRY

The opposite of Cute. Associated with naughtiness.

The sultry trait is opposed to SHY.

This implies the character has a very overt sexuality, perhaps so much
so that it can seem over-the-top.

I originally envisaged it as a character whose understanding of how
women act is more informed by porn than by real life. Of course Newlife
is an adult product so that's a perfectly reasonable way for someone to
want their character to act – scenes should avoid "judging" the
character by her behaviour although individual NPCs can do so,
especially if they have likes\_cute.

Over time I've sort of softened that perception a bit. There are still
some OTT behaviours associated with the trait, but it could also
represent a character who's simply directly sexual rather than being
flirtatious. It's the difference between flirting with a guy and hinting
he can take you home and simply telling him directly that she wants to
fuck. In fact, if we were to convert NPCs to PCs then quite a few
Sophisticated female NPCs could have this trait.

As a rule of thumb, if you're giving the character sexual behaviour, ask
yourself if it's something you'd be likely to see in real life – not
just in rare extreme cases, but from an "ordinary girl". If it is then
you should allow it for any character, or limit it by the more moderate
"flirty" trait. If it's the sort of over the top behaviour that feels
more suited to porn films then it should be gated by Sultry. E.g. she
grinds her butt against a stranger in a club: flirty (or drunk or
whatever). She takes his cock out on the dancefloor and starts sucking
him off: sultry.

In addition, when gating actions by the flirty trait, consider whether
to use flirty OR sultry. If the action implies she's especially skilled
or practiced at flirtation then it should only check flirty, but if it's
just a matter of her putting herself out there then either is fine.

A theme I've seen in some other adult games is the idea that if a
character "acts like a slut" then she'll get a "reputation" and guys
will start "treating her like one". This is fine for those games which
are focusing on different fetishes such as humiliation, but I prefer to
take a different approach in Newlife. In fact I almost never use words
like "slut" at all unless it's from a (usually-jerk) NPC insulting the
player. In Newlife the PC can be as promiscuous as she likes, and she
isn't going to get judged for it unless she's cheating on her partner
(or unless the judger is an asshole).

(normal – not a trait):

There isn't a trait for the 'normal' character type: it's defined as the
absence of the others. Normal usually doesn't need unique content, but
this might be necessary if you're writing an if statement where all the
others get distinctive text. In hindsight I'm not sure if having the
various normal/average settings on many of these enums was a good idea,
but I don't intend to make a change at this stage.

Personality Traits

These traits affect the PC's personality. As such, they're relevant in
an awful lot of writing and will very frequently need unique actions or
alternative text passages. Some are more significant than others: LSE,
Shy, Flirty, Bitchy, Maternal, Romantic in particular get a lot of
content.

AMBITIOUS

The PC is an ambitious and driven person, who really cares about success
in her career. Opposed to Relaxed.

Mostly just relevant for work-related scenes but could also be used in
competitive hobby-type events like the dance contest.

An ambitious PC can unlock actions that'd normally be blocked to her if
they'll further her career. For example, your scene might limit getting
sexual with her boss to when she fancies him, but an ambitious character
might do it even if she finds him unattractive if she thinks it'll help
her win a promotion in the future.

Ambitious characters should get stress/anxiety reduction when they
achieve major successes such as promotions or winning the dance contest
– of course promotions can't be awarded in user-written content, but
it's to be considered if your scene involves a similar accomplishment.

An ambitious character should also approve of NPCs acting in a
similarly-driven way unless it's directly against her interests, and she
should disapprove of men who lack that drive. An exception could be made
if their lack of career-focus is to her benefit. For instance if she has
kids then a "house-husband" type of man who'll free her up to be a
success at work might make a good spouse.

BABY\_CRAZY

Only partially-implemented. You should probably write for this in your
scenes as it's likely to get put into the game before too long, but bear
in mind that the PC can't currently choose it so it may not be a good
idea to write giant paths of content limited to just this character.

Baby-crazy is intended as an extreme version of the Maternal trait. One
where the PC will do insane things like trying to get pregnant by men
she's only just met.

Baby-crazy should completely block any player-actions involving
contraception or trying not to get pregnant. It can also be worth
writing dialogue lines or alternative text for this.

BITCHY

The 'evil' trait.

Opposed only to NICE. This is important: a PC can have traits like SHY,
CUTE or LOW\_SELF\_ESTEEM that might be associated with the
stereotypically sweet & innocent character and still be a horrible
person. When writing for these PCs you can't always assume she's a
mild-hearted sweetie – check for this trait. Of course a cute bitchy
girl might appear to be all sweetness and light... until she shows her
true colours and uses her venomous tongue to (figuratively) cut the
hapless NPC to pieces.

This should gate a lot of the nastier stuff the PC can do. In some cases
nastier actions can also be unlocked if she dislikes the NPC and lacks
the NICE trait, but this is to be considered on a case-by-case basis
depending on how harsh they are. Also consider limiting her cruelty if
she really likes or loves the NPC in question.

Particularly nice actions can sometimes be worth blocking for characters
with this trait too.

It's often worth writing alternative text when she does things like
rejecting men or asking them to leave. The normal version can be polite
while the bitchy version can be cutting, rude or cruel. The player
shouldn't be given a choice about being rude in these cases: they chose
the trait and the associated relationship penalties are a price they
have to pay.

Bitchy characters should get a small stress reduction if they get to
enjoy being horrid to someone.

Some actions available to these characters should increase the
ACTS\_OF\_EVIL stat.

LOW\_SELF\_ESTEEM

Doesn't respect herself and will generally not think well of herself. A
fairly complex trait to write for. Some pointers:

-   She generally reacts well to being treated disrespectfully as it's
    how she feels she deserves to be treated, and should get lower
    (or no) relationship penalties.
-   She might react worse to being treated very nicely or complimented.
    She has trouble accepting that a compliment could be genuine so she
    might assume that a man being nice to her is actually trying to
    manipulate or trick her.
-   Might agree with an NPC who insults her.
-   Might sabotage good relationships, as she feels she doesn't deserve
    them or that the NPC would be better off with another woman.
-   May be worth mentioning in descriptive text. For instance instead of
    something like "he looks at you open-mouthed, captivated by your
    beauty" you might write "he stares at you, and you shiver
    uncomfortably, sure that's he's judging you" or "he stares at you,
    clearly admiring your looks. You smile, happy to be recognised for
    the only thing that gives you value".

SHY

The PC is shy and quiet, disliking confrontation. Opposed to Sultry,
Outgoing and Flirty.

Most NPCs will dislike talking with an over-quiet PC, except for men
with LIKES\_CUTE or BOASTFUL.

FLIRTY

The PC is especially flirtatious, and is good at flirting too. Opposed
to Shy.

OUTGOING

The PC is outgoing and extroverted. They like spending time with people
and are generally better at it, although you can usually check charm
instead of this trait directly – they get a bonus to the skill.

NICE

The PC is very nice and kind-hearted. Usually good to mention when she's
being complimented. She has a hard time being cruel to people and should
have mean actions blocked or suffer stress from them. Opposed to Bitchy.

MATERNAL

The PC is comfortable with the idea of being a mother, and better at
raising children (although this is usually handled with their starting
increase to the Childcare skill). Maternal PCs should get alternative
text related to pregnancy.

Note the difference from BABY\_CRAZY. A Maternal PC is still rational.
They'll see the bright side of an accidental pregnancy but they aren't
going to head out and try to get impregnated by random strangers who'll
leave them as a single mum.

RELAXED

The opposite to Ambitious. A relaxed PC is more laid-back and doesn't
let things bother her as much. She also doesn't care about her career
very much and won't work as hard as a PC without this trait.

ROMANTIC

The PC is very romantic. She falls in love more easily and adores men
who treat her with romance. For very big romantic gestures also check
her love level. If it's at SOME or higher then she'll love them, at NONE
she might be disappointed that they're coming from that particular NPC
instead of someone she likes better.

AROMANTIC

Unlike the other personality traits, aromantic is not intended to
influence writing very much. It's a newer trait specifically added on
the understanding that it wouldn't meaningfully increase the complexity
of adding new content. As such, you usually won't need to check for it.

Aromantic completely blocks increases in Love for the player, but this
is handled by the various love-increase methods and you don't need to
put in checks yourself.

Sexual Preference Traits

HAIR\_TRIGGER

The PC orgasms more easily. Usually won't need extensive writing, but
can sometimes be worth mentioning in text or dialogue.

HARD\_TO\_PLEASE

The PC doesn't orgasm as often, an opposite to Hair Trigger.

WET\_PUSSY

The PC's pussy is especially wet and well-lubricated. Generally just
modifies descriptions of it, but also makes it easier for her to have
sex (by modifying the comfort arousal level threshold).

SENSITIVE\_PUSSY

The PC gains extra arousal from stimulation of her vagina, both from sex
and touching. You need to implement this in any such actions you write.
It's usually a good idea to mention it in the text too so the player
knows that their trait choice is having an effect.

This is generally the strongest arousal-increasing trait because it
takes effect every turn in the sex scenes..

SENSITIVE\_BREASTS

The PC gets extra arousal from having her breasts caressed. You may wish
to cap arousal increases from some actions to stop the PC orgasming from
less intense types of touches. If you're doing this for breast-groping
then PCs with this trait should ignore the cap.

PASSIONATE\_LOVER

The PC is more passionate and energetic when having sex. They're also
louder and should be described as such. This trait overrides Shy once
the PC starts to get highly aroused during sex: they might barely speak
normally but they'll scream their heads off when they're about to come.

This is listed under preferences because it also affects the type of
sexual activity the PC prefers – she should have a liking for more
passionate encounters and be less thrilled by tender lovemaking.

OVERACTIVE\_IMAGINATION

The PC fantasizes about sex more and is more easily turned on by dirty
talk.

LIKES\_BARE

The PC enjoys unprotected sex more.

LIKES\_BIG

The PC likes men with large penises. Check the THICK\_COCK and
SMALL\_COCK traits and, to a lesser extent, BIG\_COCK\_HEAD.

LIKES\_ORAL

The PC likes giving oral sex.

LIKES\_ROUGH

The PC enjoys being treated roughly in a sexual manner.

LIKES\_ANAL

The PC likes anal sex. If you're writing general sexual dialogue where
characters hint at what they like then you should write lines for this.
She should also get increased arousal/enjoyment from anal-related
actions by NPCs.

When writing anal content, be sure to check the game-option isn't set to
disable it. See the GameData method reference for more on this.

LIKES\_OLDER

The PC is more attracted to older men. This affects attraction so you'll
usually be ok just checking that for most pieces of writing. It might be
worth checking directly if you're writing text that specifies his age so
you can tell the difference between the PC being attracted to someone
despite his age or because of it.

Sexual skill traits

SNUG\_PUSSY

The PC's pussy is very tight and men will orgasm more easily from sex
with her (and enjoy it more).

CLEVER\_HANDS

The PC is very skilled with her hands. She should give more arousal and
enjoyment when using them to please a man, and the text should reflect
that skill.

SKILLFUL\_TONGUE

The PC is very skilled at oral sex, giving more arousal and enjoyment.

Other Traits

BEAUTIFUL

The PC is especially beautiful. This is already taken into account when
you check attractiveness.

However, there are some situations where it should get special text e.g.
LOW\_SELF\_ESTEEM characters who are also BEAUTIFUL might not be
insecure about their looks but rather about other things instead.

It should also be used in situations where an NPC cares about how his
girlfriend looks to others: a beautiful PC would count as "arm-candy" to
impress other people whereas one who isn't beautiful but has high
attractiveness would be very sexy to him but perhaps not so good for
showing off.

BLOCK\_ROUGH

A hidden trait that's set when the player chooses to block rough content
in the game. It's really a player option rather than a character trait.

This should act as a hard block for all such content, whether it's
initiated by the PC or by an NPC. Scenes for which such content is
completely critical should be blocked when their pre-conditions are
checked. Other scenes should make sure there's always a non-rough path
and that this is the only one available when this trait exists.

As this is really a game setting respecting it should always override
anything else, no matter how much you feel rough content might suit the
situation or an NPC's character.

CLEAR\_HEAD

The PC is very resistant to alcohol. Mostly handled by the isDrunk and
isVeryDrunk checks which will always return false for these PCs.

CUNNING

A trait based around deceit and secrecy. It's intended to mostly only be
used in scenes based around cheating and similar: this blocks random
discovery of her infidelities and stops the dirty client's wife from
catching her getting busy with him.

Although this stops random discoveries of her cheating, it doesn't mean
this will never come to light. In particular, the man she cheated with
might tell her partner.

You normally won't need to worry about writing special content for this,
unless your scene is based around the PC keeping something a secret.

FORGETFUL

The PC sometimes forgets to take her pill. You can extend this to refer
to other situations too, but don't overdo it. She's a bit ditzy; she
doesn't have brain damage.

LOW\_STANDARDS

The PC has low standards and gets an increase to attraction towards all
NPCs. You won't often need to check this in text: attraction checks
already include the effect.

PERCEPTIVE

The PC gets a bonus to her knowledge of NPCs. May be worth handling in
scenes if it seems especially relevant. For example perceptive PCs are
better at spotting condom sabotage.

PICKY

Opposite to low\_standards.

PLAIN

Opposite to Beautiful. Attractiveness effects are already handled when
you check attraction so you don't need to check for it there.

This is useful to check directly when a LOW\_SELF\_ESTEEM PC is being
insecure, or someone insults the PC. You can also write "you're
beautiful to me" type of content for NPCs who have high attraction to
her despite this trait.

A character with neither the beautiful nor the plain trait counts as
"pretty", the default level of facial attractiveness.

REFINED

The PC is very concerned by seeming 'proper' and 'correct'. She'll tend
to dislike interacting with CRUDE and SLEAZY men. The PC should be
opposed to acting in a way that she fears will affect her reputation
such as going to the nightclub toilets with a man. This principally
affects how she acts in public – she isn't opposed to having sex in
private.

Note that the PC's fears about how she's seen are basically groundless
in the Newlife world. Non-jerk people aren't going to judge her for
being a "slut", but she'll still judge *herself* and feel bad about it.

### Pregnancy Stage

The physical stage of the PC or a female NPC's pregnancy, expressed as a
description of her belly. It's accessed via getPregnancyStage(). Not
pregnant uses FLAT but so does first-trimester. You should use
isKnownPregnant() rather than checking pregnancy stage if you just want
to know if the PC is with child. For NPCs use isPregnant or isLatePreg
if you're only checking for 3^rd^ trimester.

This ties in with getStomachDesc() which provides a short text
description suitable for inserting into sentences. IsLactating() is
another method to consider when writing about pregnancy. Currently
isLactating just returns true in late pregnancy but in the future I want
to extend that so it'll also cover a period after childbirth.

Rough sex actions involving the stomach should check pregnancy stage and
be disabled if they'd clearly be unsafe. The same goes for situations
where a large belly would prevent actions. For example face-to-face
standing sex is unavailable in late pregnancy (i.e. BIG/HUGE). Text that
involves the PC drinking alcohol should check isKnownPregnant first and
have alternative pregnancy text.

There are a few further pregnancy/children related methods that aren't
currently exposed in custom scenes. I intend to add them in time, once
I've got initial feedback on the system. If you plan to write content
centred on the PC's pregnancy or family then send me an outline and I'll
see if I need to expedite adding any of them. And once again a reminder:
text that mentions the PC's kids can't do so in a sexualised way, and
they can't be present in scenes where sexual activity takes place.

FLAT ("flat stomach"):

The PC has a flat stomach: either she isn't pregnant or she's in the
first trimester.

BUMP("small baby bump"):

The PC is in the 2^nd^ trimester. She's visibly pregnant but her belly
isn't especially large yet. The PC will always know she's pregnant by
this stage – you don't need to have different paths based on
isKnownPregnant for any stage except FLAT.

BIG("pregnant belly"):

The PC is in the 1^st^ half of the 3^rd^ trimester.

HUGE("heavily pregnant belly"):

The PC is in the final part of her 3^rd^ trimester and will be giving
birth soon.

### Relationship Flag

These flags are stored for the relationship between the PC and an NPC.
As Relationships in Newlife are always PC-NPC, in practice this overlaps
heavily with NPC traits and there are often situations where some piece
of information could be tracked as either. If it's related to a
relationship and doesn't need to be shown in the character browser, then
using a relationship flag is IMO preferable.

The following are flags that you may find it useful to be able to check.

JUST\_FRIENDS

The PC has asked the NPC to just be friends and he has accepted this,
perhaps with some reluctance.

This should be un-set if she initiates any sexual activity with him in
your scene. Transitions to existing sex/makeout scenes do not need to
remove it, as they'll automatically clear the flag.

This should block him from making sexual advances to the PC unless he's
in a situation where his desires should override it. For instance if
he's drunk, has high arousal, is especially attracted to her, or feels
that the PC has been leading him on.

BLOCK\_JUST\_FRIENDS\_REQUEST

Temporary flag that lasts for 1 week. Automatically set when the
JUST\_FRIENDS flag is removed. Check this if your scene has an action
where the PC can tell an NPC to just be friends: it's used to stop the
player from setting & un-setting the flag within the same scene chain.

ALWAYS\_ROUGH:

Sets rough-mode to always be enabled with these characters. To check
rough-mode you should use\$scene.roughAgreed which will also check for
temporary rough-mode. However, if you're writing an action where
always-rough gets set then you should first check it isn't already
enabled.

LOCK\_ALWAYS\_ROUGH

Prevents removing always-rough status. You should check this before any
actions that do so.

REFUSED\_PROPOSAL

Set if the PC refuses an NPCs marriage proposal. Makes it less likely
he'll propose in the future.

PROPOSAL\_NOT\_YET

Set when the NPC proposes marriage and the PC tells him she isn't ready
yet. Has few game-effects, but may sometimes be worth checking for
dialogue, e.g. if the NPC is hoping that some romantic gesture will
change her mind.

PC\_OWES\_FAVOUR

Gets set if the NPC does the PC a large favour, but currently has no
game-effects. Currently this is only set when he pays for her wedding
dress.

CHEATING\_LAST\_CHANCE

Set if the NPC has told the PC that he'll break up with her if she
cheats again. Will never be set by DOORMAT or LIKES\_TO\_SHARE NPCs.

AGREED\_SHARE\_WITH\_PARTNER

The PC's partner has agreed that she can have sex with this NPC. Any
further sexual activities between them won't count as cheating.

KNOWS\_LIKES\_TO\_SHARE

The PC has discovered that the NPC likes to share. Sexual activity while
he's the BF will no longer count as cheating.

LOCK\_TRYING\_FOR\_BABY

Locks trying-for-baby status. This should block any actions that remove
it other than actually giving birth.

TEXTED\_BOSS\_TITS\_PHOTO

Set to true if the NPC was the PC's boss when she texted him a topless
photo. If this is set then the sales boss will talk about it at lunch,
after which the flag is removed.

TEST\_FLAG1 / TEST\_FLAG2 / TEST\_FLAG3

These three flags can be used as placeholders in your scenes if they
need new flags to be added. I'll replace them with appropriate ones when
the scene gets integrated to the game. Be sure to leave a comment
explaining what values should be added and what they do.

### Relationship Status

The PC has a relationship status with each NPC, although this is only
really relevant for male ones. It can be accessed by the
getRelationship() method on any NPC.

The NPC and PC relationship description returns an appropriate 1- or
2-word description of the relationship. E.g. "boyfriend", "girlfriend",
"stranger" etc. In practice it's mostly used after checking isPartner to
determine between boyfriend, fiancé and husband – the values for
stranger, acquaintance and date are "stranger", "acquaintance" and
"romantic interest" which don't necessarily fit as neatly into a
sentence.

Relationship status can be changed by choosing the
changeRelationshipStatus(String) method or the breakup(boolean) one. You
should always use breakup when transitioning from couple or engaged to
not being in a relationship any more.

Any relationship status of COUPLE or higher counts as being the PC's
partner. The PC should only have 1 partner at a time. You need to check
that the PC is single first if you want to make an NPC her boyfriend.

STRANGER: starting level. Automatically moves to acquaintance when
knowledge reaches a certain level.

ACQUAINTANCE: At this level NPCs will appear in the npc browser.

DATE: Set when the PC goes out with an NPC.

COUPLE: boyfriend/girlfriend. Counts as being the PC's partner. The game
currently only supports relationships with men so setting a female NPC
to be the PC's girlfriend would likely be buggy.

ENGAGED: Engaged to be married. If you're writing content where the PC
or her partner gets angry and may dump the other one then you might want
to write alternative versions for engaged and perhaps versions where
they just break off the engagement but remain a couple. Implement this
by calling changeRelationshipStatus("COUPLE"): Breakup is only used for
full breakups.

MARRIED: Implemented in 0.4.16. The PC is married to this NPC. You can
assume they live together as well, although cohabitation content will
probably be improved on in later versions. Being married will always
activate any Vows. At present there are no plans to implement divorce.
If you have writing that involves a breakup it should check for marriage
first and have an alternative non-breakup path instead.

### Scene Flag

Scene flags are not an enum value – they can take the form of any string
and you will not get an error for setting or checking a value not listed
here.

You can (and often should) add your own flags to track information
within your scene and pass it to sub-scenes. If a scene flag is only
relevant to your scene then you should prepend it with the scene's name
to avoid possible conflicts with sub-scenes. For instance the
jerk-blackmail scene uses "JERK\_BLACKMAIL\_WANTS\_ORAL**" **instead of
just "WANTS\_ORAL".

These are some scene flags that are used by existing scenes. These may
be useful to check when returning from them to tailor your returning
section to whatever happened in the sub-scene. They can also be useful
to control what can happen in a follow-up scene.

This isn't a complete list of every flag in these scenes – just a
selection that are likely to be important. I'll add more if they prove
relevant to writers.

Post-sex flags

These flags are cleared by \$scene.clearPostSexFlags. They're relevant
only for a single sex or makeout scene. Some are used to restrict
actions in a sex scene and should be sex beforehand, others are sex in
the sex scene and allow information to be handled in the returning
section.

COME\_IN\_MOUTH

FINISHED\_SEX

FINISHED\_ANAL\_SEX

CAME\_INSIDE

CAME\_INSIDE\_ANAL

DONT\_UNDRESS: Used in the makeout and oral scenes to stop the PC's
upper-body clothing from being removed. She can still take off her bra
if the top's already exposed but cannot remove or expose her top or take
off her legwear. The NPC will not do so either (specifically the UNDRESS
makeout action is removed from the list, but the READY\_SEX one
remains).

MO\_REJECTION: Only applies if the harsher "stop touching me" rejection
was used. The standard "end makeout" action doesn't set a flag. Used in
returning sections to handle negative outcomes from makeouts.

STOPPED\_SEX: Another harsh rejection: can often be handled together
with the above flag, often with the NPC leaving in a huff.

BLOCK\_REJECTIONS: Blocks rejection actions – set this before initiating
a makeout if it wouldn't make sense for the PC to reject the NPC. For
instance, it's set in some situations where the PC has just accepted a
marriage proposal and it'd be bizarre for her to follow-up by turfing
her fiancé out of bed.

BLOCK\_REQ\_STOP\_ROUGH: Stops the PC asking the NPC to stop being
rough. Currently only gets used in the lowlife scene.

LOST\_VIRGINITY: Set at the end of a PIV sex scene if the PC lost her
(vaginal) virginity. Intended for virginity-loss text in the returning
section.

NPC specific flags

These flags are removed when you change active NPC, as long as the
active npc was previously set to a different character.

INHIBIT\_SABOTAGE: Reduces the chances of condom sabotage.

TOLD\_VIRGIN\_NOPREG: The NPC told the PC that she can't get pregnant
because it's her first time.

AGREED\_ROUGH: Temporary agreed rough-mode. Use \$scene.isNpcRough and
\$scene.isRoughAgreed to check for rough-mode, but this can be checked
along with isNpcRough to see if he's being rough because she okayed it,
or because he's an asshole.

ASKED\_BARE: Set when the PC asks the NPC for bare sex, regardless of
whether he agrees or not.

AGREED\_BARE: Set when the PC and Npc agree not to use a condom. Add
this before transitioning to a makeout scene to disable condom requests.

AGREED\_INSEMINATION: Blocks pulling-out finishes for sex. Typically
combined with the above condom-disabling flag.

NO\_ORAL: Blocks oral sex. Typically set when a character rejects it.

BLOCK\_ANAL: Blocks anal sex. Typically set when a character rejects it.

LIED\_CLAIMING\_UNPROTECTED: The PC told the NPC she was unprotected,
even though she's actually on the pill. You may need to check this in
some dialogue, if the PC has had a chance to take the appropriate action
in a makeout scene.

NO\_CUNNILINGUS: Added if a request for cunnilingus is refused. Blocks
further requests from the player and initiation from the NPC.

ONLY\_NPC\_CUNNILINGUS: Stops the PC requesting cunnilingus but allows
the NPC to initiate it. Newlife uses this in the "get the boss off to
get a promotion scene" because the context of the sex scene is that it's
about the boss' pleasure so him going down makes sense only if it's what
he wants to do.

BLOCK\_MILK\_ACTIONS: Blocks breastfeeding and similar actions.

Other flags:

BLOCK\_PILL\_SABOTAGE: Stops the NPC from being able to sabotage the
PC's pill. This is currently only set if she discovers a sabotage
attempt, but you can set it before going into a date scene if you want
to make sure he doesn't get a chance at such shenanigans.

NOT\_CHEATING: This marks that whatever's happening in the current scene
should not count as cheating. You can set this before calling a makeout
scene if e.g the PC's boyfriend has given his approval.

You don't need to set this to mark that the PC is single or that an NPC
is her partner: that's handled by the standard cheating logic when you
call addSexualActivity and inseminatePlayer.

If your scene is a sub-scene such as a makeout or sex scene then you
should check if this flag has been set when you make calls to
addSexualActivity and inseminatePlayer.

HUSBAND\_AWAY\_FOR\_NIGHT: Affects the Home-Date scene by letting an NPC
sleep over even when the PC lives with her partner. Should only be set
when the PC is living with her partner (check via \$w.livingWithPartner)
and when the NPC is not him.

### Sexual Activity

Sexual activity represents whether the PC has done the relevant activity
with the NPC. You can check this using the male NPC's
hasDoneSexualActivity method. It may be useful in writing dialogue that
references a previous hanky-panky.

You should also call addSexualActivity when the PC does something on
this list with an NPC, otherwise this won't be recognised in future
scenes.

KISSING:

Counts as 'light' cheating only. Set when the PC willingly kisses an
NPC, either by initiating it or by being a willing participant.

TOUCH\_COCK:

Light cheating. Set this if the PC touches the NPC's penis.

GROPE\_BREASTS:\
Light cheating. Set if the NPC gropes the PC's breasts, even through
clothing.

FEEL\_PUSSY:

Light cheating. Set if the NPC feels up the PC's pussy. This includes
touching her through her panties, but not if it's being done through
actual lower-body clothing.

PC\_ORGASM:

Moderate cheating. Set when the NPC makes the PC orgasm. Handled
automatically by the causePlayerOrgasm method.

HANDS\_ORGASM:

Set when the PC brings the NPC off with her hands.

ORAL:

Set when the PC takes the NPC's cock into her mouth. This should be set
at that point, even if the oral sex isn't to completion.

CAME\_IN\_MOUTH:

Set when the NPC ejaculates into the PC's mouth. Usually at the end of
oral, but not always. If your text is referencing this then you may need
to check the NASTY\_SPERM and TASTY\_SPERM traits.

TITJOB;

Set when the PC gives the Npc a titjob, not necessarily to completion.

SEX:

This and below count as Severe cheating. Set when the PC and NPC have
penetrative vaginal sex until he orgasms. Setting this when the PC is a
virgin will automatically update her virginity status.

ANAL:\
Anal sex: handled similarly to the SEX value.

CAME\_INSIDE:

Should be set when the NPC ejaculates into the PC, regardless of whether
it's a safe-day or not. This only applies to full internal ejaculation,
not to finishing outside but in a risky position.

CAME\_INSIDE\_ANAL:

As above, but for anal sex.

LOST\_VIRGINITY:

This can be checked to see if the PC lost her (vaginal) virginity to an
NPC. *Do not* set this via addSexualActivity. Instead you should add the
SEX activity and it'll automatically be updated.

LOST\_ANAL\_VIRGINITY:

As above, but for anal. Should not be set directly – use
addSexualActivity("ANAL",...) instead.

### Skill

Skills can be increased by using the relevant methods on the player
context object, although skill-training in scenes should usually be rare
and limited to small values. NPCs do not have skills.

The method \$w.getSkill("SKILL") will return an int value for the
relevant skill.

The maximum skill value is 100 but some traits will limit a character's
skill training to lower levels. The property \$w.skillMaxed will return
true if a skill has reached its maximum value but it's usually better to
check against fixed numeric values and if a character's skill ceiling
prevents them from accessing a certain action then that's just a
consequence of their trait choices.

Skill values can be negative. This is most often seen in CHARM and
FEMININITY, both of which can be significantly negative based on
character-creation choices.

New skills are likely to be added as the game is developed further.
Current skills are:

ADMIN:

Currently "Paperwork" in the game UI. Used in the office work career,
but not elsewhere.

CHARM:

Represents the pc's interpersonal skills and can be checked to see if
they do well in a social situation. Low charm could result in a
foot-in-mouth situation while high charm could let them avoid an
embarrassment or let them convince someone to their point-of-view.

It may be worth combining charm checks with the isDrunk or isVeryDrunk
method as a pissed PC might forget their social skills.

Charm usually should not increase in-scene unless the whole point of the
section is training the PC's social skills.

CHILDCARE:

Affects how good the PC is at taking care of children. Rarely used
directly in-scene but might be worth checking if e.g. you want someone
to compliment the PC on being a good parent. Could be increased if a
scene involves extensive interaction with children. However, bear in
mind that underage characters can only be present in a scene if it's
entirely non-sexual. That includes the PC doing sexual things with an
adult NPC in their presence or sexualised depictions of things like
breastfeeding and childbirth.

DANCE:

How good the PC is at dancing. Used heavily in scenes where the PC
dances and rarely otherwise. Choosing to dance in a scene may increase
the skill by a point.

FASHION:

The PC's fashion skill. Don't use this to see if she should be
complimented on her clothing as a high-skill PC could still be wearing
ill-fitting clothes. Clothing stats should be used instead. The fashion
skill could dictate how good the PC is at finding nice clothes in shops,
her ability to bargain-hunt for clothing, her ability to recognise how
well or poorly someone's dressed or how much of a reputation she has for
being a fashion-guru among her friends.

FEMININITY:

Perhaps the most important skill in most scenes. Femininity represents
how comfortable the PC is with being a woman and how convincing their
behaviour is. It modifies attractiveness.

Female-start characters currently always have high femininity (starting
at 75). I have no particular plans to change this but that isn't a
binding promise so it's a good idea to check the ALWAYS\_FEMALE trait as
well if you're writing content for low-femininity characters that only
applies to gender-bent men.

Some things to consider in writing:

Low femininity (say &lt;20, and especially &lt;0) might lead to her
being seen as oddly mannish.

Lowish femininity might lead to special text about how the PC is
surprised at being treated as a woman or how something is different to
when they were male. The exact threshold will vary: if the text is
particularly sexy then I'll have a wider range so more players see it.
Generally consider &lt;20 or &lt;30, but up to &lt;40 is fine if the
text is very interesting or even &lt;50 if it doesn't assume the PC has
only just become female.

High femininity especially &gt;75 should result in male-start characters
getting the same text as female-start ones, or getting text that
mentions them being completely comfortable as a woman, barely
remembering what it's like to be a man, or feeling like it'd be strange
to be male again.

I have considered adding options to change this, but for now the game
assumes that a male-start PC was heterosexual so she had no sexual
experience with men before the game began.

Femininity can increase if the PC does something that represents
acceptance of being female.

FITNESS:

How fit and strong the PC is. Somewhat influenced by body-type, although
it's possible for a toned character to have low fitness or a slim one to
be quite strong.

Should be checked anytime the PC's strength is relevant or if you want
to add text that implies she's strong or weak compared to an NPC. NPCs
do not have skills, but you can figure out an approximate strength
hierarchy from their body-types.

MANAGEMENT:

Appears as "Business management" in the character screen. Only used for
career progression.

### Stat

Numeric stats. Mostly these are shown in the character screen and for
many this is their sole purpose. Some stats are checked in the code
though: for example RELATIONSHIP\_DURATION is used in the anniversary
scene to figure out which anniversary the player's celebrating.

There are a few hidden stats that aren't shown to the player.

New stats can be added for user-submitted scenes if they're really
needed.

You should increase stats as appropriate in your scenes. Stats like
money earned will automatically be changed when you call the methods to
change the PC's money though, so you don't need to worry about those. As
a rule of thumb, if the method has enough information to increase a
stat, it will. So calling the haveOrgasm method will increase
all\_orgasms but you need to increase sex\_orgasms or anal\_orgasms
manually as it doesn't know what's happening in your scene to make the
PC come.

TIMES\_CLUBBING

HOUSE\_PARTIES

SHOPPING\_TRIPS

DATES

SEX\_PARTNERS: Unique sexual partners. Vaginal sex only.

SHAGS: or "times had sex", as it appears in the character screen. This
is only vaginal sex.

ANAL\_PARTNERS

ANAL\_SHAGS

TIMES\_UNFAITHFUL

ORAL\_PLEASURE

TITJOB\_PLEASURE

HANDJOB\_PLEASURE

CONDOM\_SEX

RISKY\_INSEMINATIONS

BROKEN\_CONDOMS

ALL\_ORGASMS

SEX\_ORGASMS

ANAL\_ORGASMS

CUNNILINGUS\_ORGASMS

BEST\_JOB\_PERFORMANCE

MONEY\_EARNED

MONEY\_SPENT\_CLOTHES

DRINKS\_BOUGHT

HANGOVERS\_CURED

DRINKS\_TREATED: Times someone's bought a drink for the PC.

TIMES\_MUGGED

BEATINGS\_GIVEN: "Can't act like a twat and not expect a little tap,
just a little tap on the nose". Seriously though, I feel that actual
domestic violence is a bit too dark for how I like to imagine Newlife so
leave beatings for criminals and the like and restrict the pc to only
verbally abusing her boyfriend...

ACTS\_OF\_EVIL: Increase this as appropriate when the PC does something
evil. Evil actions are often but not always restricted to bitch
characters.

HEROES\_REWARDED

WEEKS\_HIGH\_STRESS: Extreme/max stress weeks also increment this.

WEEKS\_EXTREME\_STRESS: Max stress weeks also increment this.

WEEKS\_MAX\_STRESS

ANXIETY: total anxiety gained across the whole game.

RELATIONSHIP\_DURATION: weeks in current relationship. Multiples of 26
are anniversaries.

WEEKS\_SINCE\_ORGASM: Weeks since the last time the PC had an orgasm in
a scene. Incremented by 1 at the start of each week.

WEEKS\_SINCE\_SEX: Weeks since the last time the PC had vaginal sex.
Incremented by 1 at the start of each week.

WEEKS\_SINCE\_ANAL: Weeks since the last time the PC had anal sex. Like
other anal stats, it's only shown on the character screen when anal
content is enabled. Incremented by 1 at the start of each week.

WEEKS\_SINCE\_INSEMINATION: Weeks since the last time the PC was
inseminated. This counts all inseminations including any that didn't
involve penetration.

These are some of the hidden stats. They're used to control access to
certain scenes or activities.

HOUSE\_PARTY\_COOLDOWN

CONCERTS\_ATTENDED

GYM\_CHANGING\_ROOM\_THREESOMES

SALES\_SLACKER\_FRIENDSHIP\_MEETS

OFFICE\_RIVAL\_DOMINANCE: Values above 100 enable the scene where the
rival begs the PC for mercy. It can go negative but you should check its
current value before reducing it and not drop it below -50 so the player
still has some chance of recovery even if the rival is beating her at
first. You only need to change this if you're writing content involving
the PC and office rival competing with each-other.

### Stuff

Items that the PC can buy or otherwise acquire. The most important one
is obviously the kettle, which must be obtained for her to make tea.

PILL

CONDOMS

PREGNANCY\_ACCELERATION\_TREATMENT

IVYS\_PREGNANCY\_ACCELERATION

FERTILITY\_TREATMENT

DANCE\_TROPHY

DANCE\_WOODEN\_SPOON

DANCE\_COUPON

GYM\_MEMBERSHIP

PARTNER\_PHOTO

SPA\_VOUCHER

TEDDIES

EROTIC\_ART

ELEGANT\_ART

POSTERS

GIANT\_TEDDY

SPECIAL\_RABBIT

AWESOME\_BABY\_TOYS

GOURMET\_COOKBOOK

COOKING\_GEAR

DVD\_PLAYER

TV

BIG\_TV

SOUND\_SYSTEM

PC

LUBE

SEX\_TOY

KETTLE

### Top Type

Top type is (obviously) only available for tops and affects quite a bit
of undressing text. There are a number of real-world top-types that
aren't implemented in the game, and this sometimes restricts the
addition of new items.

STRAPPY

HALTERTOP

STRAPLESS

ZIP (zips down the back, may or may not have sleeves – that's left
unspecified)

BUTTONS (buttons down the front)

SLEEVED (not implemented yet, but will be in the future – probably the
next significant addition to the player's clothing options. Intended for
t-shirts and similar. These are delayed because unlike the other types
their EXPOSED state would be pulled up above the PC's breasts instead of
down around her waist so a fair bit of descriptive text needs to be
rewritten for them to be added).

### Vow

Vows are promises made in a special scene while a couple is engaged. Use
the NPC method hasActiveVow to see if a player has a certain vow agreed
with that NPC.

Vows are only relevant for couples and only at ENGAGED or MARRIED
relationship status (depending on game options). As such, you don't need
to check vows for female NPCs or if you know an NPC isn't the PC's
partner.

Vows are treated as binding promises in-game, and the player should not
be given the option to break an active vow. For instance, any actions
where she requests a condom or puts one on her partner should check for
an active NO\_CONDOMS vow first and be disabled if that's set.

The vow doesn't define who asked for it. While many vows can only be
requested by one partner some are available for both. In any case, you
can't assume that one character has been unhappily pressured into
agreeing to a vow as they could have been happy about the request even
if they didn't ask for it themselves. The only exception would be if a
character has traits that clearly show they'd be opposed to a certain
trait, such as an NPC with doesnt\_want\_kids having agreed to have a
family.

More vows may be added as the game is developed further.

SUPPORT\_PC\_FINANCIALLY:

The NPC has agreed to give financial support to the PC. Should be
checked if she asks her partner to pay for something for her. If he's
promised this vow then he should agree regardless of his opinion.

HELP\_WITH\_KIDS;

The NPC has agreed to help raise any children the PC has. This applies
to both her kids with him and any she had with other men before. The vow
is available to couples without kids, referring to their future
children. Check \$w.isMum() to see if the PC has children.

This is mostly significant for its gameplay effects in week procession
and usually won't matter in writing, but if you're including a scene
with the PC struggling with her kids then you should consider checking
for this with her boyfriend and having him help.

HAVE\_CHILD:

The couple has promised to have at least one child. This sets the
tryingForBaby relationship flag once active until the vow is completed.
tryingForBaby is not fully implemented yet but it's still a good idea to
take it into account when writing new scenes. You usually would just
need to check tryingForBaby in your writing rather than the individual
babymaking vows.

HAVE\_SON:

Like HAVE\_CHILD but only completed when the PC has a son.

HAVE\_THREE\_KIDS:

Like HAVE\_CHILD but only completed when the PC has had 3 children.

HAVE\_MANY\_KIDS:

Like HAVE\_CHILD but is never completed and will permanently set the
couple as trying for children.

ALWAYS\_ACCEPT\_SEX:

Blocks the PC from refusing sex from her partner.

NO\_CONDOMS:

Blocks either partner from using condoms.

NO\_PILL:

Stops the PC from going on the pill. You'd normally just check isOnPill
rather than worrying about vows.

GO\_ON\_PILL:

Requires the PC to go on the pill and stops her going off it unless the
couple are explicitly trying for a baby. Your writing will usually just
need to check isOnPill as it's rare that a scene would need to change
the PC's pill status.

ALWAYS\_CONDOMS:

The NPC will always wear a condom before sex unless the PC specifically
asks him not to. TryingForBaby status will override this.

