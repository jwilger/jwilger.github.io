---
layout: post
title: Retrospective Facilitation
date: 2009-01-13
comments: true
categories: [teams, work, retrospectives]
---

I facilitated my second release retrospective with the ProjectDX team yesterday.
The first, back in October, went well enough given that I was asked to
facilitate at the start of the retrospective and had no time to prepare; but
yesterday's retrospective went great since I knew ahead of time that I would be
facilitating.

<!-- more -->

The activities we used during the retrospective mainly came from Diana Larsen
and Esther Derby's book, Agile Retrospectives. We started off with the "ESVP"
(Explorer, Shopper, Vacationer, Prisoner) activity to find out what the group's
interest level was in relation to the work we were doing in the retrospective.
Nearly everyone in the group said they were an Explorer via anonymous vote. With
this group, I basically trust that outcome, although I did wonder if anyone may
have given the answer they thought they were "supposed" to give.

Next, I had the team build a time line of events from the past release. Prior to
the start of the retrospective, I drew the time line on our white board and
divided it into sections for each iteration (our cycle is 2 3-week sprints
followed by a 2-week, internal Alpha testing period and a 2-week customer Beta
testing period). The result looked something like:

```
|----------|----------|-------|-------|
| Sprint 1 | Sprint 2 | Alpha | Beta  |
|          |          |       |       |
|          |          |       |       |
|          |          |       |       |
|          |          |       |       |
|          |          |       |       |
|          |          |       |       |
11/03 -----11/24 -----12/15 --12/29 --01/09
|          |          |       |       |
|          |          |       |       |
|          |          |       |       |
|----------|----------|-------|-------|
```

During the retrospective, I had everyone take some time to think about any
events during that time period that were meaningful to them in any way, write
the event on a sticky note then stick the note on the time line in roughly the
right spot. We spent about 45 minutes generating events, during which time we
were free to look back at calendars and email as well as the commit logs from
our SCM. Having set the time box to 45 minutes, I said it was fine for people
to take a break if they felt like they couldn't remember any more events and
asked everyone to simply be back on time for the next step.

Rather than specifying that people work in pairs, I opted to have the team
self-organize here. It was interesting to see how—at first—everyone seemed to
work on their own, but as the more obvious events were posted to the board,
people started working in groups to come up with more data. At the end of the
allotted time, we had a white board full of events.

The area below the time line was intended for a graph of energy/emotion levels,
which I'll talk about in a moment, but JD Huntington had a great idea to also
add to that area a rough bar graph of our commit volume as reported by GitHub's
activity graphs.

After everyone had a last opportunity to look at the board and add any
last-minute stickies, I asked everyone to take a turn at the board and use
markers to place a blue dot next to any event which they felt positive about and
a red dot next to any event that they felt negative about. Then, I asked them to
think about their positive and negative energy/emotion levels throughout the
release and draw a line graph in the bottom section to signify their ups and
downs throughout the release cycle. At this point, we looked at each iteration
in the cycle and I asked the team to make observations about the data. Using
bullet lists at the bottom of the white board, we captured the observations as
further data points for analysis.

After a break for lunch, we used the "Patterns & Shifts" activity to generate
insights about the data on the time line. We gathered around the white board
where I asked each person to mark on the time line any point at which they felt
there was a shift or transition of some sort and to draw lines between any
events, graph points and observations that they felt were somehow related.

After no one was able to see any more connections, I asked the team to look for
any patterns among the connections and the shifts. The first thing we noticed
was that we felt like the real shift between iterations was constantly happening
about 3 days after the actual time box ended. Rather than get into a long
discussion about it when it was noticed, I asked the team to simply keep it in
mind as a possible concern during the next phase of the retrospective.

The next observation was that we had a number of connections with long lines
spanning two or more iterations. I asked everyone to focus on these connections
and look for those where we may have noticed an issue early on but it wasn't
addressed until much later. In some cases it turned out that while that was the
issue, the length of the line just signified that either the work took that long
or there was a conscious decision not to address the issue right away.

Reflecting on the other cases led to an interesting discovery, however. Chris
noticed that where the lines crossed the bounds of the iterations it was likely
signifying a parallel cycle which we were attempting to force into our release
cycle: specifically, we have both an explicit product release cycle and an
inexplicit customer deployment cycle occurring at the same time.

After we were finished recognizing patterns in the data, it was time to discuss
these patterns (and anything else on our minds) and come up with a few action
items for the next release cycle. Here I ran the team through the "Circle of
Questions" activity. In this activity, the group sits in a circle, and each
person takes turns asking a question to the person on their immediate left. The
question can be about anything they like (barring anything offensive or
attacking), but it's helpful to focus on the insights gained during the previous
stage of the retrospective. The person to the left answers the question to the
best of their ability, and then they ask the person to their left any other
question (or the same question if they feel they'd like a better answer). This
continues until the alloted time is up or you have gone around the entire circle
twice, whichever comes last. Make sure you go around the complete circle: if
some people in the group get more turns to ask or answer a question than others,
it can send the wrong message.

The thing that I really like about the Circle of Questions activity is that when
you have a mixed group of people—some of whom tend to dominate the conversation
while others tend to stay quiet—it gives everyone a chance to ask their
  questions and have their opinions heard without feeling like the most
  boisterous people have the only valuable input. We certainly have a mix like
  that in our case, and this activity worked wonderfully.

In the end, we came away with a number of things to change for the next release
cycle. It's interesting to note that none of our action items were directly
related to the insights generated from the time line. I think the insights are
still valuable (and are contained in the notes which we post to our internal
wiki), so we may still come back to them in the near future; we were running
over on time and had to wrap up even though the discussion could have continued
longer.

Before we held this retrospective, I think some of the team members felt that we
would not gain much from doing a full-day retrospective this time around. We had
made good progress on our action items from the previous retrospective, and the
general feeling was that things were going basically well. What could we
possibly need to change?

People, please don't hold retrospectives only when your team feels like there's
a problem that needs to be dealt with. If you hold retrospectives on a regular
basis, whether you feel like you "need" to or not, you will uncover issues
before the become problems. In our case, we managed to uncover a number of
issues during our retrospective that could easily have grown into much larger
problems if we didn't bother to think about them until the effect was obvious.

If you do have obvious issues, then you might choose a different set of
activities than what we did for this retrospective. The time line activity is
great for discovering potential improvements even when everything seems to be
going well, so I suggest giving it a try the next time your team is tempted to
skip a retrospective because no one thinks there's any huge problems.
