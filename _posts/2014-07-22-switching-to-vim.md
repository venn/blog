---
layout: post
title: Switching to vim
author: justin
comments: true
---

You have likely encountered dozens of posts wherein the author extolls the virtues of their new and Vi IMproved life. They save thousands of tedious trips between mouse and keyboard each day. They edit text at the speed of thought. They can perform emergency hotfix heroics becuase vim is installed on every production server.[^1]

There are also posts describing the elegance of conceptualizing text editing in terms of text objects and motions.

These are all merits of vim but not what made me switch.

## Plays well with others

A while ago I started pair programming more often with vim users and my rudimentary skills soon became an obstacle. Sure there are setups where each pair can use their own editor but they require too much setup and as such tend to ruin impromptu sessions. Even though I knew it would be a lot of work, I wanted to become at least competent with vim.

## That other editor only crazy people use

I have been using emacs as my primary editor for about 10 years and I am fairly productive with it. vim is well-known for having a steep learning curve but I expected it would be especially difficult coming from such a different editing paridigm.[^2]

## Easier than I thought to pick up

Rather that hindering I think my emacs experience actually helped me to pick up vim faster. I suspect that learning how to work without a mouse, graphical file tree, etc. is a significant part of vim's learning curve for most people.

## But not too easy

I still have a ways to go. I am not yet as fast with vim as I was with emacs. I've also rewired enough of my muscle memory that switching back feels painful and cumbersome even though not doing so can be slow at times. The surprising thing is this doesn't bother me as much as I would have expected. I actually prefer to edit in vim even though I only know how to do a fraction of the things that I could do in emacs and a fraction of the things most other vim users can do.

## The interesting bit

Despite having so little practice and so little knowledge of various operations I'm nonetheless nearly as productive in vim as I was with emacs. I struggled to understand this but I have a theory: having only a small set of operations that compose well goes a lot farther than a large set of operations that do not.

Before I got to see people working with vim I had the mistaken impresison that they learned thousands of little keystroke combinations that let them do very specific things. This might be true for some really nerdcore developers but most people just learn efficient ways to perform common manipulations and do them over and over again until they are editing without thinking about it.

emacs is an incredibly rich development environment and supports some really powerful types of operations. However, remembering all of the little details is difficult. One often has to use the built-in help system or try out a few practice edits to make sure something works the way you expect.

The problem with this is that it takes you away from the task at hand. Thinking about a way to make the exact transformation you need in one shot is a waste of time when you can just make a handful of simpler modifications that accomplish the same thing.

Furthermore, once you start making these edits mechanically, without really thinking about what you are doing, your mind is freed up to think about the actual problem your code is trying to solve.

Understanding this made me feel strangely liberated: I don't have to become an expert with my editor in order to be able to use it well.

[^1]: Don't ever do this, even if you are an idiot.

[^2]: Fear of being excommunicated from the emacs community was another risk.
