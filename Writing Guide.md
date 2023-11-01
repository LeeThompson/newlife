Newlife Writing Guide
=====================

Getting Started
---------------

Hi, welcome to the writing guide. This is a high-level overview of how
to write for Newlife.

First of all, you should contact me with a brief summary of what scene
you're looking to write. This is best done in a public forum so other
players can also comment. See the Submissions Guide for links to forum
threads. This is an important step because it means that if I forsee
issues with an idea that might stop if from being implemented I can let
you know *before* you spend a lot of time working on it.

Secondly, consider a text editor with appropriate syntax highlighting
for editing the YML and text files

Submissions structure
---------------------

A submitted scene takes the form of 2 files: a YAML file containing the
scene's structure and a text one with all the text that might be shown
to the player.

The YAML file must have a .yml extension. The example text file has the
.vm extension to allow Velocity syntax-highlighting in text editors. You
can also have a text file with the .txt extension, as long as it matches
whatever's set in the textFileName field in the YAML file.

Running the examples

The documentation folder contains examples of both of these. You can
open these up in an appropriate editor to see their structure and
comments. To run them:

-   Copy both the YML and text file to the user\_custom\_scenes folder
-   Run the game, and go into the options screen
-   Check the option to allow custom scene testing
-   Start a game
-   Choose the test activity in the weekday-evening timeslot

YML file structure

See the separate YML syntax file for an overview of how this file is
defined. For general YAML see <https://en.wikipedia.org/wiki/YAML>

The text file is in a simple pseudo-xml custom format. The text passages
are divided up into sections by tags. These start with e.g. &lt;tag&gt;
and finish with &lt;/tag&gt;. Unlike XML there is no top-level tag.
Because this is not XML, text within the tags does not need to have xml
special characters like &, &lt; or &gt; escaped.

Within the tags, text will be processed by Apache Velocity. See
<http://velocity.apache.org/engine/1.7/user-guide.html> for a guide on
how to use Velocity. While this might at first glance seem quite
complicated, Newlife text mostly does not use especially advanced
Velocity functionality. Primarily you'll be using if-elseif-else-end
clauses and accessing objects' methods.

Discussing your scene
---------------------

It's a good idea to bring up your scene for discussion before you start
work. You can do this on any forum listed in the scene-submisisons
guide. There's also a Discord for Newlife scene writers:
<https://discord.gg/66Q7UDy>

Editing Files
-------------

A number of text editors allow syntax highlighting of YAML and Velocity
files. Using one of these will be much easier than an editor that just
treats them as plain-text.

One free option is notepad++ (<https://notepad-plus-plus.org/>). This
will highlight yml files by default.

It also supports user-defined language files. One player, Rigel, has
made some files to support highlighting and autocompletion for Newlife's
.vm files (with Velocity text within tag pairs).

These are included in the "notepad++ highlighting by Rigel" folder
within the documentation one.

The first file is the userdefined language one named
userDefinedLanguage.xml. To import it into np++ go to the languages
menu, Define your Language. Then select Import and choose the file.

The second file is "velocity.xml". This allows autocompletion in np++.
To install it:

-   You need to be already using Rigel's Velocity user defined language
    file
-   Copy velocity.xml to the "plugins\\APIs" folder of your Notepad++
    installation (default would be "C:\\Program Files (x86)\\Notepad++",
    so "C:\\Program Files (x86)\\Notepad++\\plugins\\APIs" in full)
-   If you do have Notepad++ installed in the default location, Windows
    will ask for admin rights because you can only write into
    "C:\\Program Files (x86)" if you have them.
-   You'll need to restart Notepad++ if you had it open.

If you prefer not to use np++, other editors that have been recommended
by players are Atom (<https://atom.io/>) and Sublime
(<https://www.sublimetext.com/>)

Writing for Newlife
-------------------

Writing for Newlife is likely to be different to submitting content to
other text games. This is because of 3 design decisions that very much
shaped how it developed:

-   Newlife scenes are broken down into detailed individual actions,
    rather than being single large passages
-   Newlife has a lot of different internal variables.
-   Most of those variables affect not only game mechanics but also the
    text shown to the player.

These mean that Newlife scenes cannot be written as large short-story
style blocks of text. They need to be broken up into individual actions
which in turn need to be extensively divided to work for all relevant
variable combinations. In fact, it's rare to be able to write more than
a sentence or so without having to break off into conditional
statements.

That doesn't mean that traditional writing is useless for Newlife, but
rather that it's very much a starting point. I'll often begin an action
by writing a passage with a lot of assumptions about the characters,
then go through it step by step and consider all the places where
alternative versions need to be written.

An example

Let's imagine I'm writing a 'general' scene between the PC and a male
NPC, that can allow almost any combination of the two. This is a bad
idea for volunteer submissions because of its complexity, but such
scenes do exist: core scenes such as sex and makeout ones need to work
for most character combinations.

I might start by writing something like this:

"With an abrupt gesture, Bob beckons for you to approach him. You
hesitate a moment, eyes downcast, a faint flush colouring your cheeks.
He repeats his order, in words this time, barking out a command.

You tentatively walk over to him. Once in arms-reach he takes your hand
and brusquely pulls you close, spinning you around so you fall backwards
against him, his heavily-muscled body easily absorbing the impact.

His arms wrap around you, breath hot against your neck. In a low voice
he growls that he wants to empty his balls, and your pussy will be the
perfect receptacle."

Now, this is a decent enough piece of text, but it isn't suited to
Newlife writing as-is. I'd need to replace things like the NPC's name
with the appropriate method calls of course, but that isn't difficult.
The main challenge is going through it, and deciding which parts need to
be split up with alternative sections and implementing those variant
paths & actions.

First let's look at the action overall. This is obviously a quite harsh,
commanding action. Is it intended to be restricted to only harsh NPCs?
That's a possibility, but if so then there needs to be equivalent
actions that handle NPCs with other behaviours. This one could
alternatively be a general "npc beckons to PC" action with both harsh,
polite and loving options. This could affect the Pc's reactions in turn:
a confident PC might react badly to a barked order but better to a
polite request.

Next, the player's respose seems like it'd be limited to a specific type
of character. Specifically a shy one, and perhaps also one who's
attracted to this NPC or in love with him. What about other characters?
How would they react? This needs to be handled both in the text and in
game effects: a shy girl who obeys meekly would lead to a very different
NPC reaction from a bitchy one who disobeys and verbally cuts him down
to size. This could be handled by giving the player response actions, or
by checking her traits, relationship levels etc to decide what she does.

Then the second paragraph has yet more "meek" text. That'd need to vary
for different Pcs. The next part should vary based on the NPC's
body-type. Potentially it needs a different ending for each one,
although it might be possible to combine some in the same section.
Depending on how much I wanted to put into this action, there could be
some major variations. Perhaps if the NPC is skinny then the pc falling
against him knocks them both onto the floor, where they end up entwined
together. This part with the NPC pulling her to him doesn't seem like
it'd be only for harsh men, aside from the word "brusquely". It could
probably work for other paths through the action too.

The third paragraph has a speech section. This has 2 main issues;
firstly the "he growls" bit should be restricted on NPC behaviours, so
there needs to be a different lead-in for other ones. Then main part of
his line seems like it should be limited to men who plan to finish
inside her unprotected. That might not be the case based on traits or
relationship status, or a man with likes\_oral or likes\_anal might
prefer somewhere other than her vagina. A variety of different lines
would be needed there.

Lastly, there are two more steps. The penultimate one is to consider
game effects. Should this increase arousal or modify relationship
values? Probably arousal should be increased for the player only, and
only if the NPC's behaviour match the PC's preference traits. The PC
could also gain enjoyment if she has a very strong match. A PC who obeys
the NPC might increase his Enjoyment slightly, and one who disobeys
could lose some. Finally, if the text implies the PC gets annoyed or
angry with the NPC then she should lose liking towards him.

The final question is "what next?". Should the PC get text implying
she's getting turned on by the NPC's actions? Does she need a response
to what the NPC's done? Does this modify the scene's internal state in a
way that'll affect other actions (e.g. if the scene switches between
face-to-face and in-his-arms sections)?

As you can see, the final version of this passage is likely to be quite
a bit longer than the original, and the main challenge in writing is to
decide on which alternative sections need to be added to the text and
then implementing them.

There isn't an easy fix for this; you can expect to dedicate a lot of
your Newlife writing time to figuring out if statements. However, there
are some ways it can be mitigated. I'll give some of these in the next
section "Writing Tips" and the following one on preconditions.

Writing tips
------------

This section covers some general tips for writing. This includes advice
on how to manage writing for large numbers of variables as well as tips
on how to match my writing style in Newlife.

Write additively rather than multiplicatively where possible

Imagine you're writing content where an NPC gropes the PC's breasts. You
decide to vary the passage on her breast size in a more thorough way
than just inserting "full breasts" instead of "heavy breasts". That's 4
options. Then you decide on alternative text for the sensitive\_breasts
trait. That's 2. Then on whether she's wearing a top and bra, just a
top, just a bra or neither (4), then on whether the NPC gropes them
gently or roughly (2).

If you write a different section for each combination of these then you
need 4x2x4x2 = 64 passages of text. That's unreasonably many for a
single action, not to mention that there might in the future need to be
more variations (e.g. on lactation).

Instead, try to write the sections one after the other. For instance you
first have the roughness section "&lt;name&gt; tenderly reaches for your
&lt;breasts&gt;, caressing them with his &lt;adjective&gt; hands". Then
the clothing one "Without a bra, they move freely beneath your (thin)
&lt;top&gt;". Then size "They fit perfectly into his hands, not massive
unwieldy jugs but just the right size for him to enjoy". Finally,
sensitivity "your lips part in a silent exhalation, your breasts so
sensitive that your body warms to even the gentlest touch (rough: and
this particular caress is far from tender)".

In this case there's just 4+2+4+2 = 10 different sections that need to
be written. You'll notice that I did vary the last section based on
roughness as well: it's still possible to combine your conditions if
there's a specific section that needs to take another part into account.

There may be some situations where you have no choice but to write
multiplicitavely: for instance I've been in a situation in the past
where I've had to multiply out the 5 NPC behaviours and 8 PC ones to
ensure I had text that worked for each combination. However, this should
be avoided where possible.

Use generic else sections

Your scene needs to work for all character combinations that can access
it. This can sometimes seem overwhelming, especially if it's supposed to
work for almost any NPC.

One tip is to use a generically-written section that can apply to many
different trait combinations. Usually this will be a shorter and simpler
passage, but it can still be "good enough". You can have this as the
else section of an if-elseif-else-end clause and then write longer, more
specific paths for the if-sections.

An example of this in Newlife is the NPC orgasms in the missionary
scene. When Newlife was first released its text was much simpler and
more generic than it is now and there was just one "catch-all" orgasm
section. Since then much longer passages have been added, but that one
generic section is still there to catch any situations that aren't
covered by a more extensive option.

In the current version, the final missionary orgasm else clause picks
randomly between 2 'generic' passages, one of which is the tiny original
one from 0.1.0. Just a single line: "&lt;name&gt; thrusts balls deep
into you. He pauses a moment, shaft filling you completely, then he lets
out a powerful grunt and you feel a warm sticky wetness deep inside as
he ejaculates into you."

That particular passage is just 1 line of code whereas the method itself
is over 400, but despite being far smaller than the more specific
sections, it's still of great value.

The if statements preceding it cover particular situations that I could
think of an interesting & relevant orgasm section for. These are longer
and I think better than the generic one, but the specificity of their
requirements means I don't have a good idea for every single possible
combination. For example there's one for a male-start character with the
romantic trait who's having risky sex with someone she loves. It
obviously isn't possible to cover every possibility with checks that
specific, but having a generic passage at the end means it isn't
necessary.

Be careful with extra NPCs

A typical Newlife scene involves 2 characters. Adding more increases the
complexity in a non-linear fasion. Typically these sort of scenes will
need to be either heavily restricted or have quite a simple scope: see
the section on preconditions.

While I'd enjoy seeing a good-quality general "PC + any 2 NPCs"
threesome scene in the game, its size and complexity would be beyond
anything currently in Newlife – not something that seems feasible for a
single writer. Perhaps that might be a worthwhile project for a group of
writers who are all experienced with Newlife content, but it isn't
something I'd advise even considering for people new to it.

Don't try to shoehorn game mechanics into things they weren't designed
for

This might imply that your content might not be well-suited for the
game.

Alternatively it might just be that the user-submissions system needs
refinement in that area. If you find yourself trying to manipulate game
mechanics into doing things they clearly aren't suited for then you
should instead contact me and discuss the situation: it might be that
improvements to the system will allow your writing to proceed more
straightforwardly.

Avoid quoted speech

You should avoid directly-quoted speech for characters in Newlife. I
experimented with this in pre-release, but even with over a hundred
lines for the relevent action dialogue still became very repetitive.
Instead, use a line like "&lt;name&gt; tells you that you're the most
beautiful woman he's ever known". For me, when I read something like
this I can imagine that the NPC's exact words might vary between
different characters, so it isn't as odd when different ones use the
same line.

Space out your writing for readability

A common problem I see with posts online is the "wall of text" issue,
where someone's put a lot of time and effort into writing something but
it's almost unreadable because it isn't spaced out into paragraphs.

You need to make sure that text shown to the player has appropriate
spacing, including empty lines between paragraphs.

Use end-of-line comments to stop Velocity adding unwanted newlines

Velocity will tend to add Newlines every time you have a line-break in
your text. This can be a problem for big if statements, especially if
you want to e.g. pick how a line is supposed to end without inserting a
newline in the middle.

You can solve this by adding a 'comment' (\#\#) to the end of lines that
shouldn't include newlines. This flags everything on that line after the
comment to be ignored when Velocity processes your text, which means the
end-of-line newline character won't be added to the text shown to the
player.

Sketch out your scene's key points with a flowchart before starting

For many scenes, it's possible to start with a flowchart of the PC's
actions and possible NPC reactions to them. Sketching this out on paper
can be helpful to keep track of the scene's overall structure. These
charts can get excessively complex for larger scenes, but even then you
can do a stripped-down version with just the key nodes.

Make sure to at least skim the reference guides

It's hard to list variables that you'll definitely need to write for
because this will vary from scene to scene. As such, it's a good idea to
at least skim the reference guides and make notes of the key ones
that'll be relevant for your content.

Use random lists for dialogue and short descriptive sections

You can create lists in Velocity and pick from them randomly using the
appropriate method in the \$scene object. You can also use it's
weighted-map functionality to have a weighted list.

This lets you add variety to actions, especially ones that will show up
a lot.

This is especially useful for dialogue. While I've experimented with
various approaches in the past, some heavily overengineered, here's what
I currently consider best:

-   Start by dividing the dialogue by general action type. E.g.
    romantic, sexual comments, compliments, insults. Have a separate
    action or section for each one. That way you can have the other
    character react the same way to every line within a given section.
-   Build up a list of possible lines by checking a condition and adding
    them to your list/map as appropriate. Make sure to use end-of-line
    comments to stop the velocity text getting tons of unwanted
    blank lines.
-   Depending on how often the dialogue is to fire, you may need large
    numbers of lines. If the action is supposed to fire multiple times
    in a scene you'll probably want dozens of possible lines, perhaps
    even a hundred or more. This might seem like a lot, but because
    lines will be specific for traits or combinations of traits (e.g
    Likes\_cute + shy) most won't be valid for a specific playthrough.
-   Ensure that there'll always be at least one possible line. Usually
    this can be handled by adding some generic lines that are
    always possibilities. If you're using the weighted map you could
    give these a lower weight so more specific lines will show up more
    often if they're available. You can also check if the list is empty
    and only add the default lines if it is – this is a solution for
    when you don't like the generic lines as much as the specific ones.
-   Proceed to write your text as normal, inserting the line retrieved
    at random from the list/map at the appropriate place.

Consider key variables when planning a scene

Once you have an idea of which variables will be most important,
consider how they'll affect your scene. This might involve extra
actions, alternative descriptions, restrictions on the player's choices
and even entirely new paths through the scene.

I recommend looking over the reference guides, but here are some
starting points that will very often need to be considered:

MALE CHARACTER INTERACTIONS:

Vary heavily on NPC behaviour, with some influence of the personality
directly (e.g. Jerks being chauvinistic). NPC personality traits usually
also need to be considered. The PC's personality traits are also
relevant.

If your scene includes PC-behaviour (not available in the initial
release of user-submissions content, but no doubt an addition I'll put
in before too long) then that's also often relevant. If you aren't using
pc-behaviours then her direct liking & love will probably need to be
checked.

You'll also usually need to consider relationship status and especially
if he's her partner. It might also be relevant to check what they've
done together e.g. if they've had sex, have a child together or
whatever.

FEMALE CHARACTER INTERACTIONS

Some similarities with male ones, but these should vary heavily on the
female Npc character type. These tend to be very different from each
other so I often find that any interaction with a female NPC needs to be
split into a different section for each charType.

SEXUAL CONTENT

Sexual actions will often need to check attraction levels and arousal.
NPC & PC sexual traits and preference traits are also important. You'll
also often need to vary text & actions based on the characters'
clothing. Finally, physical variables such as Figure and breast-size
will often need alternative text.

Use parentheses in conditions with both AND (&&) and OR (||) operators

For readability, you should use parentheses in conditions that have both
&& and ||, even if when doesn't change how the program evaluates them.

For example instead of:

A && B || C && D

write:

(A && B) || (C && D)

Preconditions
-------------

Almost every scene in Newlife has some sort of preconditions. Your
submitted scene should include a section on how you think it should be
accessed, what conditions need to be met, and what restrictions exist on
NPCs that it can run with. This can be included as a comment at the top
of the yml file, or just in the message or post where you submit it.

Activity, Event or Sub-Scene

First you should specify how the scene is to be accessed. There are 3
main ways:

Activities are triggered by the player as a specific choice from the
weekly menu. I don't want to bloat the game out with huge numbers of
these, so I prefer submissions to be events or sub-scenes. However,
where it makes sense for the scene to be an activity I will accept these
submissions: check with me before writing though. An example would be,
say, a scene where the PC is doing charity work. This could be accessed
by a "Volunteer for Charity" activity on the weekend timeslot.

Events are picked randomly when the PC's week is being processed. An
event can have almost any set of preconditions. This includes things
like only when a specific activity is being run, as long as that
activity doesn't have a fixed scene that overrides random events.

Sub-scenes are accessed from within another scene using a scene
transition. You can write sub-scenes for your own scenes using the
custom scene transition. To connect up a sub-scene to existing Newlife
content you should specify which scene it splits off from and how it
should be accessed within that scene – I'll make the necessary
modifications to the Java scenes.

Scene repeatability and multi-scene chains

You should specify whether you want your scene to be repeatable and what
situations that should apply for. If your scene is to show up multiple
times in a playthrough then it should make sense for it to do so. It
should also have enough variation that it'll be rewarding for the player
to see it more than once per game.

You may also want your scene to unlock future ones. This is fine, but
these future-scenes need to be submitted alongside it. Or, if they
aren't, your scene needs to make sense without them being there.

You can also ask for your scene to only be accessible if an existing
scene has already run. For example you might want to write a work event
that only shows up if the PC has slept with her boss for a promotion.
That's typically not going to be a problem, although you should
definitely ask in advance if you're planning to take one of the special
NPCs in a new direction.

Restrictions on NPCs

Many scenes will need some sort of restriction on which NPCs can be
passed into it – this should be explained for each NPC in the
pre-conditions.

For example, if your scene is a random event where the PC's partner
surprises her with a grandiose romantic gesture then the conditions on
the NPC would be that he must be the PC's partner, he must have the
romantic personality, and he must have a certain level of love towards
her (probably crush+ in that example).

Another way of limiting NPCs is to use a special NPC. Don't go nuts
making tons of special NPCs as I don't want to bloat the game out with
hordes of them. However, there are some scenes where they make a lot of
sense.

If the NPC in your scene doesn't act in a way that's consistent with
other scenes then they should be a special NPC limited to your scene
only. It's also possible to have "special" NPCs that can show up in
other scenes. The repairmen and dance students are examples of this sort
of thing.

In some cases you might want to have a scene 'mark' an NPC. An example
of this is the treasure-hunting one. The first time this fires it can
happen with any interesting friend of the player's. I decided that it'd
be odd if every interesting friend turned out to be an urban explorer
though, so I had the scene mark this NPC by giving them the
treasure-hunter trait. Once this trait's been assigned the scene will
only ever fire for that NPC, even if the PC has multiple interesting
friends.

Restrictions on the PC

Some scenes are only available for certain player-characters. This is
something that you should be careful about adding as a precondition
though, because players almost always question why their character can't
access the content.

It's fine to have these restrictions if there's a genuine story reason
for it. For example, the evil impregnator friend will only ask bitchy
PCs for help because he wouldn't expect anyone who isn't equally horrid
to help him with his loathesome plan.

However, you shouldn't restrict your scene on PC traits just because you
don't want to write for a specific type of player-character –
restrictions need to be justifiable in a way that players will accept.

Other restrictions

Beyond characters, almost anything that's tracked in the game can be
used as a precondition. E.g. the anniversary scene has a precondition
that the weeks-in-current-relationship stat is a multiple of 26. If you
aren't sure, just ask.

Using preconditions to reduce scene complexity

Your writing can assume that the pre-conditions are met. E.g. If your
scene's pre-condition is that an NPC is the PC's partner then you can
assume this to be the case and you don't need to write alternative text
for NPCs she isn't together with (although you might need separate
bf/fiance/husband text in some places).

Where the situation is heavily restricted, your writing can be
dramatically simplified. The scene with Horse is an example. I knew that
a 3p makeout scene would be unreasonably large to write in a general
case, so I used a pair of heavily restricted NPCs. To pick one of the
many examples, Horse always has the same body type so there was no need
to write thickset/toned text for him.

It's therefore a good idea to decide on your preconditions early. That
way you won't be wasting time writing text for situations that won't
happen in-game.

However, preconditions have to make sense in the context of the game. If
the player is left asking things like "wait a minute, why does my
character have to be cute to access this scene?" then it becomes a
problem. As usual with this sort of thing, if you're unsure you should
ask on a forum so people, including me, can comment with our thoughts.

Testing and Debugging
---------------------

Scenes should be tested before submission. As well as doing this
yourself, it can also help to submit a WIP version to the appropriate
discord channels. That way other players can try out the scene and give
their feedback.

Errors can show up due to issues in either the vm or yaml files. Usually
the error message will help figure out the problem. You can also ask on
the discord if you need help tracking down a bug.

One of the more challenging issues is "Error tokenizing YAML". This
means there's a mistake in the yaml syntax: often an issue with
start-of-line spacing. The error will show up when the yaml file is
first being read, which is when you select the file from the testing
scene.

The error message itself doesn't tell you *where* the problem is in the
yaml file. However, there are tools that can help. I found a website
<http://www.yamllint.com/> which lets you validate yaml – simply paste
the entire contents of your yml file into the text area, click 'go', and
the site will point you towards any syntax issues.

Quality & Content restrictions
------------------------------

There are a number of restrictions on what content I'll accept into the
game. Of course every submission will be assessed on its own merits, but
here are some general guidelines:

Quality Restrictions

-   Submissions must be *complete *before they can be added to the game.
    They can't have dead-ends or "to be completed" sections. They must
    be at least "good enough" for all combinations of characters &
    game-situations that can lead to them being accessed.

    That said, if you're writing a voluntary user-contribution then
    you're under no obligation to finish your work, even if I've been
    giving you advice & support on your writing. A paid commission
    obviously comes with an expectation that something will be
    delivered, but not a voluntary submision. You shouldn't feel
    pressured to complete the scene if you don't want to – I certainly
    won't be upset if you stop writing partway.

    If you decide to abandon your work and want to open it up for other
    people to complete then you can post it on an appropriate forum or
    send it to me and explain that you won't be working on it
    any further. If you prefer to keep it to yourself then that's also
    fine of course.

-   Writing must be largely free of spelling & grammatical errors and
    have reasonable spacing and paragraph breaks.
-   Writing must be of a quality that I feel is good enough to include
    in the game. If you aren't very fluent in English then it's probably
    a bad idea to try to write for Newlife. Auto-translated content will
    certainly not be accepted.
-   The writing style must be one which I feel would work with the game.
    I'm not going to be upset over e.g. US-English spellings or idioms,
    but if our writing styles clash heavily then it'll look odd and
    out-of-place for players.
-   Submissions must work as-is without assuming any additional content
    will be written for them. If your scene is such that it'd be weird
    without a follow-up (e.g. if a character promises one) then that
    follow-up must also be submitted alongside it. If you're planning to
    write a multi-scene event-chain then it's probably better to start
    as a single self-contained scene that makes sense by itself and then
    modify the original scene when the follow-up is ready.

Content Restrictions

-   Submissons must not require significant changes to fundamental
    gameplay mechanics.
-   Submissions must not demand the addition of new 'complexity' changes
    such as traits, personalities, relationship types etc that require
    extensive updates to current & future scenes in order to make sense.
-   In some cases it might be possible to have a fetish-specific scene
    without new game mechanics designed around that fetish. For example
    if you want a scene where an NPC is defined by their great love of
    feet then it'd be odd for the player if that NPC was date-able
    because they'd never mention feet again on normal dates. It wouldn't
    be acceptable to demand a "foot fetish" trait be added and all
    scenes be rewritten with foot-content to support it. However, you
    could have a special NPC who only appears in your scene and scenes
    written by other foot-fans. Because they won't show up in the normal
    club/date/etc scenes it won't be out of place if their behaviour
    isn't consistent with a normal Newlife NPC.
-   It is acceptable for a submission to ask for changes that wouldn't
    need to be handled in other people's writing. Most obviously: new
    game-flags, stats, special NPCs or hidden 'marker' traits are often
    useful for multi-scene control. It's fine to ask for these, although
    you should do so in advance so you don't waste time writing if I
    decide to turn the request down.
-   It's acceptable to ask for minor 'recognition' lines added in a few
    specific places. Again, if this is critical to your submission then
    you should ask before writing.
-   It's also fine to ask for changes to a small number of specific
    existing scenes for the purposes of connecting up your scene. For
    instance if I've given you the go-ahead to write a date sub-scene
    then I'll obviously need to add an action or two to the date scene
    that handles transitioning to it.
-   Submissions must make sense in the modern-day-ish game-world.
    Fantasy or sci-fi elements can be very fun in games based on those
    premises, but they don't really fit with Newlife.
-   Submissions for inclusion in the main part of gameplay must have the
    PC be female and, as mentioned in the "no changes to game mechanics"
    section, must not have an NPC with aspects that aren't handled by
    current characters (e.g. futanari). In theory sub-scenes for the
    endgame or pre-transformation intro sequences could ignore this
    condition, but I imagine writing that sort of thing would have some
    real challenges as it's not what the user-submissions system was
    really designed for. I'm not going to veto such content, but it's
    probably a bad idea for someone new to writing for Newlife.

In addition to the above technical & storyline restrictions, there are
certain types of content which can't be included in Newlife for legal or
personal reasons:

-   Newlife is intended to be a fun light-hearted game, not a
    political statement. As such, any references to real-life politics
    or religion are forbidden. References to fictional politics (such as
    the Unethical Experimentation Party mentioned in the intro) are
    allowed, but they shouldn't be thiny-veiled versions of real-world
    political parties or religions.
-   Similar to the above, anything I consider to be unnecessarily
    controversial is forbidden. It's supposed to be a fun, sexy adult
    game, not a soap-box or a device through which to be 'edgy'.
-   No content may violate anyone's copyright.
-   I won't accept content involving real-life people,
    including celebrities. It is ok to make up a fictional actor,
    rock-star or whatever, but you can't refer to real ones.
-   No content that's illegal in the UK can be accepted into Newlife. In
    particular, you may not have any sexualised content of under-18s and
    they may not be present in any sexual or erotic scenes. This
    includes the PC's children which means things like eroticised
    breastfeeding scenes cannot be added. See the 'legal discussions'
    section below for more on legal restrictions.
-   Any content involving the "glorification of rape and sexual
    violence" is forbidden under Patreon's community guidelines and
    therefore cannot be added to Newlife. This sort of content also
    seems like it would be risky under the OPA (see the legal
    section below).
-   I won't accept submissions if I feel they'd be considered unpleasant
    or unsettling by a large proportion of players. This mostly affects
    certain fetishes involving bodily emissions (e.g. 'scat'). I do feel
    some sympathy to people with an interest in obscure fetishes which
    many find disgusting but have nothing legally or morally wrong
    with them. In the longer-term I might attempt to open up options to
    let writers play their scenes in Newlife in a non-testing capacity
    without them being part of the main distribution. That isn't a
    high-priority in the short-term though and is never likely to match
    the versatility of submitted content: Newlife wasn't designed with
    proper modding in mind and isn't really compatible with it barring
    dramatic changes to how the game works internally.
-   I won't accept any sexual content involving blood, sickness,
    mutilation, death, serious injury or extensive suffering. I have a
    personal aversion to reading this sort of content and I don't want
    to have to edit and maintain it. This includes even quite mild
    mention of blood, such as the PC's periods: you can assume she does
    have them but they always happen "off-screen" rather than in
    playable scenes.

Legal Discussions

The UK has an awful lot of laws against various types of adult content.
As a non-lawyer, I don't have an especially thorough understanding, and
I prefer to err on the side of caution: being too cautious means perhaps
blocking some scenes involving extreme content whereas insufficient
caution could land me in prison. Not exactly equal stakes!

A lot of UK porn laws define porn in a way that doesn't include
text-only content. However, there's one in particular that warrants
discussion here: the Obscene Publications Act.

This isn't a concern for the average UK porn viewer as it only covers
publication of content, not possession. For me though, it's a real
issue. The OPA (
<http://www.legislation.gov.uk/ukpga/Eliz2/7-8/66/contents>) allows
someone to be arrested for publishing material, including text, that may
"deprave or corrupt" people who view it.

The OPA has been used to arrest people for text-only content, and it's
been used against quite small-scale creators: I've read about one man
who was arrested for releasing a free fan-fiction story online. I find
it especially concerning because it's so vaguely worded. What exactly
will "deprave or corrupt"?

Now, this vagueness cuts both ways. Prosecutors have in some recent
cases failed to get convictions under the OPA because a jury disagreed
with the police over whether the materal would deprave or corrupt its
readers. I imagine however that being arrested must be a harrowing
experience even for people who aren't found guilty, and it isn't
something I want to risk.

While looking online, I found the Crown Prosecution Service guidelines
for the act
(<http://www.cps.gov.uk/legal/l_to_o/obscene_publications/#b02>). It has
the following passage:

It is impossible to define all types of activity which may be suitable
for prosecution. The following is not an exhaustive list but indicates
the categories of material most commonly prosecuted:

-   sexual act with an animal
-   realistic portrayals of rape
-   sadomasochistic material which goes beyond trifling and transient
    infliction of injury
-   torture with instruments
-   bondage (especially where gags are used with no apparent means of
    withdrawing consent)
-   dismemberment or graphic mutilation
-   activities involving perversion or degradation (such as drinking
    urine, urination or vomiting on to the body, or excretion or use
    of excreta)
-   fisting

If your writing involves any of the above, then I can't accept it in
Newlife – I'm not comfortable risking legal consequences for including a
writer's submission.

Scene ideas for starting writers
--------------------------------

General Advice

You should start small. Decide on an idea for a short scene with minimal
compexity as your first piece of writing.

A lot of the complexity in writing comes from the interactions of
multiple NPCs. Scenes with &gt;2 characters are massively more
challenging to write and should be avoided until you're very
experienced.

General scenes that can take almost any character are also much more
challenging to write for than more restricted ones. For your first
scene, aim to restrict it as much as is feasible.

Full sex or makeout scenes are very complex, both because they're
'general' ones that need to work with pretty much any PC+NPC combination
including many special NPCs and also beceause they're large scenes which
interact heavily with the most complicated parts of Newlife's game
mechanics. Not a good idea for a first piece of writing.

Some scenes have specific aspects that may not have been added to the
user-submissions system yet. Typically these are the more complex scenes
that I wouldn't expect someone to start with, and I'll be adding more
methods over time.Contact me if you find that you want to do something
which exists in a Newlife scene but which is either impossible or
awkward to add in a custom one and I'll see about hooking it up for
user-content.

The below sections are a few ideas I thought up that might be suitable
for starting writers and for next steps once someone's a bit more
familiar with the system. Of course you may have your own, different
ideas – that's fine of course.

Ideas for a first scene

The small friendship events that are triggered by the activity where the
PC spends time with her friends are ideal for a first scene. They're
designed as short vignettes that highlight a particular situation for a
certain friend's traits or personality. As such, they can easily be
heavily restricted, especially where the NPC's traits are concerned.
They're also usually quite short.

You could add a similar 'boyfriend' event, a small random flavour scene
that highlghts a certain aspect of the PC's partner.

Work is another place where small flavour interactions might make sense:
perhaps ones that provide further interaction with one of the special
work NPCs. You could also write a scene that's specific to when the pc's
boss has certain traits or personality.

A small random encounter is another possibility. The cupcake scene is a
good example. It'll sometimes be possible for such scenes to have only
the PC by herself, which makes them easier to write than ones with
PC-NPC interaction.

Another idea would be an erotic-dream scene. This could transition to
actual sex if the PC wakes up turned on and calls her lover to visit.
Having the main part of your scene be a dream would give you a lot of
flexibility about its size, and of course you wouldn't need to worry
about most relationship modifiers.

One suggestion on the discord was a motherhood scene: go to the park
with your baby, talk to some other mums etc. Such a scene probably
wouldn't interact much with the more complicated sexual parts of the
code beyond, perhaps, some flirting with single dads. That could make it
a fairly straightforward one to write.

Ideas for medium-complexity scenes

Once you're more familiar with writing for Newlife you could tackle more
in-depth scenes such as dating ones that focus on character interactions
or sexual scenes that are simpler than the 'general' sex scenes for one
reason or another.

One example would be to write a larger partner event covering a full
date, complete with flirting, behaviour-based interactions, dialogue
actions and some sexual activity. This could be distinguished from the
core date scenes by making it a specific situation: the bf taking the PC
out for a particular special occasion.

Another option would be to write a date sub-scene like the sex-shop.
This has the drawback that the date scene is accessible for virtually
any NPC so you can't assume they're the PC's partner unless that makes
sense in the preconditions to access the sub-scene. Still, such scenes
cover quite specific situations and are simpler than a big sex or
makeout scene.

A sexual scene that'd work well as a user-submission would be a
gloryhole one. Gloryholes aren't something I'm particularly into, but of
course that just makes them especially suited to be written by someone
else. Gloryholes would work very well for Newlife because they'd need
much less complexity than a full 2p sex scene. With the NPC on the other
side of the hole there'd probably be little or no dialogue, no
relationship effects if they don't know who the other person is, no need
for NPC actions and no need to reference many NPC variables such as
their body-type and many of their traits. Make sure to let me know
before attempting this though, as there can only really be one such
scene so I don't want to find out that many writers have worked on one
simultaneously and I have to reject most of their hard work.

Another sexual option would be a return to the BDSM club. If I get
multiple such submissions then this could work as an activity which
splits off into different sub-scenes at random. In this case you can
assume the PC is into BDSM as it'd only be available if they chose to
return. BDSM content is potentially easier to write. First, because a
restrained PC has fewer possible actions and therefore fewer variables
to consider, second because performing a show on stage might not require
a statted NPC.

Another idea for a medium-complexity scene might be a masturbation one.
Sexual content is normally quite challenging to write for Newlife as it
has a lot of relevant variables. A masturbation scene would massively
cut this down as there'd be no interaction with an NPC. However, it
isn't straightforward to see how this could be integrated with the game
in a way that improved gameplay and didn't become repetitive – which is
why I haven't written such a scene outside of the section in the intro.
If you want to write something like this then it'd be a good idea to
contact me before starting work, so we could work out the context in
which it'd be called.
