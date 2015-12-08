---
title: "Portal Adventure: Session One"
date: 2015-12-07T10:36:28-0800
commentIssueId: 1
excerpt: >
  This is the first post in an ongoing series in which I talk about the
  development of "Portal Adventure", a text-based adventure game that my
  10-year-old son and I are writing in order to help him learn about
  programming.

---

My second-youngest kid, Lachlan—a fourth-grader this year—became very
interested in computer programming over the last several months. He's
mostly been doing a lot of work on his own to learn; he's an avid reader
and has picked up a number of technical books to learn about JavaScript,
HTML, Ruby, etc. while asking me a few questions here and there and
showing me _more_ than a few little experiments he's worked on while
learning. He's made good progress, but we are at the point where he'll
really benefit from working on a bigger project with someone more
experienced. Fortunately, he lives with just such a person!

## False Starts ##

We have kicked around a number of ideas for what to build. Given that I
do most of _my_ work developing web applications and his interest in
HTML and JavaScript, our first ideas were for different web
applications that we could build. We made a few false-starts here, but
the problem—as I see it—is that he's not quite ready for the complexity
inherent in having to combine knowledge of HTML, CSS, JavaScript, Ruby,
web-servers, etc. in order to build a useful web application.

As we worked through things, I would have to spend so much time jumping
from topic to topic and explaining fundamentals that we could never
focus on one area long enough for him to develop a deep understanding,
and we couldn't make enough visible progress on our idea in order to
keep it exciting (for either of us). While we managed a couple of
sessions, it didn't really lead anywhere. I needed to find something a
little bit simpler.

## An Idea Emerges ##

Last week, I started playing a video game called [Pillars of
Eternity][pillars]. Lachlan saw me playing it and asked why I enjoyed it
so much, and I told him it is because I really like games that have a
rich and engaging story. This got us talking about games a bit, and I
recalled to him my experiences as a kid playing what is still one of my
favorite computer games of all time: [Zork][zork].

As I described Zork to Lachlan, it dawned on me that creating a similar
game might be a great project for us to work on together. It would have
the advantage of being complex enough to provide many teaching
opportunities, yet the interface to it is simple enough that he would
get to see _something_ working almost right away; no need to set up a
bunch of frameworks just to get a few strings to output to the console,
which is enough of a start to get the ball rolling. Plus, it's making a
game! What kid doesn't enjoy making up games?

I proposed the idea to Lachlan, and he immediately got excited about the
possibility. We kicked around a few ideas for the basics of the game and
came up with a concept for the game mechanics.

Much like Zork, the player will control a character via text commands
entered at a CLI prompt, and then the game will respond with the result.
The game will consist of multiple locations, each with a description of
the area and containing various items with which the character may
interact. We _may_ attempt to build a command-parser like the one in
Zork, but we might also take the easy way out and present a list of
possible actions from which the player may select. The basic options
would be for moving from location to location, picking up and dropping
items found throughout the game, and using items to interact with the
environment.

The game will be divided into a number of _levels_, each of which will
contain multiple _locations_. In order to move between levels, the player
must defeat enemies and/or solve puzzles and, by doing so, unlock the
_portal_ on that level. Once a level's portal is unlocked, the character
may travel from the portal location on their current level to the portal
location on any other level that has been previously unlocked. The
player wins the game when they unlock the portal on the final level.

## Our First Session ##

We had our first session of pairing on the game yesterday, and we spent
around three or four hours between discussing our first steps and then
getting to our first milestone. (A lot of that time, of course, was
taken up with explanations about some fairly basic stuff such as "here's
how we initialize a new git repository," and "this is the purpose of an
_object_ in object-oriented programming.")

Starting from the outside and working our way in, we determined that our
first milestone would be that we can launch the game (always as a new
game at this point, we will tackle saving games down the road) and it
will output a description of the starting location.

As for testing, we (well, _I_) decided not to try and automate any
full-stack testing with something like cucumber at this point—we will
perform that level of verification through hand-testing for now—and that
we will do extensive unit testing with RSpec. We may try to add in
full-stack acceptance testing down the road, but I wanted to make sure
we had enough time to get something done-done by the end of our first
session, and the milestone was simple enough to not need that level of
automated verification.

While the absolute simplest/dumbest way we could meet the milestone
requirement would be to just add a `puts` statement to the game
launcher, we instead took some time to think about what objects we would
need in order to implement the basic game mechanics and then implement
our first milestone in terms of (some of) those objects.

First, since we wanted to output the description of the location in which
the character starts the game, we clearly needed some type of `Location`
object with a description attribute. Easy enough.

Since we start off the game with a _character_ in that location, we
needed a `PlayerCharacter` object, and because we operate the game from
the point of view of that character, we want to get the description of
the location by having that player character inspect the location. That
last part will be important for the game mechanics, because the
description of the location that is output by the game may change
depending on certain attributes of the player character.

We would also need something to encapsulate the general state of the
game (who is the player character, what is the current location, etc.),
which we decided to call the `Universe`. This object would serve as the
factory that sets up the game context and then allows us to `#run` the
game.

Finally, rather than baking into the guts of the game the assumption
that it will run in a console with access to `STDIN` and `STDOUT` for
communication with the player, we would initialize the `Universe` with a
`PlayerInterface` that provides a higher-order abstraction around the
player's interaction with the game.

The result of our work after the first session can be found as of [this
commit][commit-milestone-1] at [the Portal Adventure Github
repository][git-repo].

![Result of first
milestone](/images/2015/screenshot-2015-12-07-15-06-45.png)

## Up Next ##

Next time, we will be implementing our first two commands: `look` and
`quit`. The former will simply display the description of the current
(and so far only) location and wait for another command, while the
latter will exit the game, returning the player to their shell prompt.

## Additional Ideas ##

Some additional ideas that I have for the game include:

* Random Level Creation - use a database of "challenges" to randomly
  create each level, either at the start of the game or perhaps as each
  level is unlocked.
* Game DSL - rather than random level creation (or in addition to the
  possibility of that?) create the game engine as something into which a
  separate "game description" can be loaded, thus allowing a
  content-creator to write new adventures.
  * I wonder if there's a way to use cucumber/gherkin for that? (cue evil
    laugh)
* Character attributes/skills - Use a D&D-like system of character
  attributes and skills to influence how the player goes about solving
  each level.
  * Would need to be careful to ensure that it was never impossible to
    solve a level.
* Multi-Character Adventuring Party - Especially if using
  attributes/skills, we could allow the player (or perhaps player*s* at
  this point) to switch between and control multiple player characters
  with different abilities.

## Constructive Feedback Appreciated ##

I hope that you'll follow along as we continue to develop Portal
Adventure and eventually enjoy playing the game, too. If you have any
feedback on our code or ideas about the game design, please feel free to
share them as [Github issues][gh-issues], comments on the commits, or
pull requests. And although I have a pretty thick skin when it comes
to...&laquo;ahem&raquo;...discussions about the best way to code things,
please keep in mind that there is a 10-year-old, very green programmer
working on this project and keep your feedback appropriate. :-)

Also, yes, I am aware that there are _numerous_ libraries and frameworks
out there that already allow people to create text-based adventure
games; no need to point them out other than in the context of "I see you
are attempting to do _X_. You might want to look at how something similar
was done in _open-source-codebase-Y_."

Remember, the main purpose of this is to help Lachlan learn about
programming, not just to develop a game that we want to play.

[pillars]: http://eternity.obsidian.net "Official Homepage for Pillars of Eternity"
[zork]: https://en.wikipedia.org/wiki/Zork "Zork - Wikipedia, the free encyclopedia"
[commit-milestone-1]: https://github.com/jwilger/portal_adventure/tree/285f56d0872f1bf47bc4b5d89bb813dfc61b5e41
[git-repo]: https://github.com/jwilger/portal_adventure
[gh-issues]: https://github.com/jwilger/portal_adventure/issues
