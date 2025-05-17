# Project 2: Environmental Engineering

Our first project exercise introduced the basics of game flow. We divided our
game up into scenes and then used basic if/elif/else logic to control which
functions are called based on user input.

This time we are expanding upon that to add in game state tracking and (very
basic) inventory management. We will also get introduced to `gametools.py`,
which is a library of functions that will allow you to greatly enhance the
visual appeal of your game in very simple ways.

## Learning Objectives

1. Use lists as a way to manage program state
2. Practice working with list functions
3. Practice inspecting list content
4. Practice iterating over lists

## Introduction

This time, the scenes for this game are mostly completed for you. Instead of
adding new scenes, you will be interacting with in-game objects and dynamically
changing the scene descriptions and user options based on what your player has
chosen to do in the game.

We are also deliberately keeping this simple so we can focus on the main goals
of this assignment. These are:

  - Managing game state: "State" just means persistent memory. We want to keep
    track of anything that the player has done that might impact the way a room
    is described or what options they have available. We will track game state
    using a list.
  
  - Managing inventory: Inventory is a list of items that the player is
    carrying. This actually is just another type of game state. The only reason
    we track it separately is to make it easy to distinguish between things a
    player has done or encountered versus things a player is carrying.

  - Using lists with gametools.get_choice() to simplify how a player makes
    choices in the game.

## gametools.py Function Library

This assignment includes a very gentle introduction to the gametools library.
These functions were designed to make it really easy to do relatively fancy
things with your game. You're being introduced to five functions today:

  - `pause()`: this is just a "Press any key to continue..." function that allows
    you to pause output (likely to allow the user to read before calling clear).
  
  - `clear()`: this just clears the screen.

  - `write()`: for this week, write is just another way of calling print(). But it
    has a lot of extra features that will be cool and useful in the near future.

  - `write_md()`: similar to write, this prints text to the screen. But this
    version accepts a string of "markdown" formatted text (remember that??) and
    does its best to display it on the screen formatted as a markdown document.
    Headings, bold, italics and lists all display quite well in the terminal.

  - `get_choice()`: this is the most "exciting" of the new functions. Instead of a
    player having to type in their choice, they can use arrow keys to select
    from a list of valid choices. You simply pass a list of strings as your
    "choices" (and optionally a list of ints representing indexes to hide) and
    you get back the index of the item that the player chose.

Feel free to look at [GAMETOOLS.md](GAMETOOLS.md) for a more detailed look at
these and a couple other functions. There's a lot there that CAN be used to
spice up your game, but not much that NEEDS to be used, especially not yet.

## Tasks

First a quick note. These programs have a lot of lines of code. And thus they
appear to be intimidating. And doubtless at first glance they are. But a large
part of the code is comments or just narrative being displayed on the screen.
And most of the rest is actually very basic branching logic.

  - Take it slowly
  - Read and *__understand__* the logic
  - Copy/Paste as needed, but *__understand__* BEFORE you copy/paste so that you are
    not just "hacking' something that works.

There are a few tasks to complete this week, though there are no explicit tests
for you to run to verify everything works. As with the first project assignment,
these are going to be run interactively and hand graded to give you more freedom
and so that your instructor can enjoy your creativity and wit.

  1.  show_inventory(): this is really simple, but you just need to iterate over
      the inventory list and print out the contents as a "bulleted" list.
      There's a heading and a special case for an empty list, but otherwise,
      this should be old hat now.

      > NOTE: We're accessing `inventory` (and later `game_state`) from within
      > functions even though they are defined in the "global" scope. And we are
      > doing so WITHOUT using the `global` keyword. Though it is generally
      > frowned upon to access global-scope variables from a function like this,
      > it's sometimes the "right" solution. And this is one of those times.
      >
      > Why can you modify inventory and game_state despite not having a global
      > keyword? It has to do with the "rabbit hole" of memory management. You
      > are not actually modifying the value of the inventory variable. That
      > value is a reference to a list which is stored in a shared pool of
      > memory. You are actually modifying the items in that shared list. If
      > your head is spinning, don't worry...maybe you should worry if it
      > **isn't** spinning. It's a complex topic and not really a learning goal
      > for this course. So it's okay to just accept that it works and move on.

  2.  "Fix" two additional scenes: after reading through and trying to
      understand how the `cell` and `hall` scenes work, you are given specific
      tasks to perform to make the `armory` and `bobs_lair` functions work
      correctly.

  3.  The only semi-freeform bit here is the final scene--`attack_bob()`. Here
      you are given basic guidance and it's up to you to write the narrative and
      finish out the (very short) game.

The "map" this time is quite small:
```
    ┌───────┐            N                      
    │ Cell  │          W + E                    
    └───┬───┘            S                      
        │
    ┌───┴───┐    ┌────────────┐   ┌────────┐
    │ Hall  ├────┤ Bob's Lair ├───┤ Armory │
    │       │    │)attack bob)│   │        │
    └───────┘    └─────┬──────┘   └────────┘
                    LOCKED!
```
It looks kinda similar, but this time you have torches, keys and spears that are
required to allow the game to progress.

Cell and Hall (and the Intro) are 100% complete. These should serve as
references for how the core game logic _should_ work.

As before, effort and creativity count. But it's a smaller percentage this time
since it's a smaller part of this sample game. So expect points to be
distributed as follows:

  - 90% functionality
  - 10% creativity and effort

## Assignment Completion Procedures

You will complete and submit this assignment in a similar way to prior
assignments. To avoid cluttering up this README with the same instructions each
time, they have been broken out into a separate file. Please reference
[PROCEDURES.md](PROCEDURES.md) to see the details if you have forgotten.

In summary:

  1. Complete the code per the instructions
  2. Run the game to test and debug interactively
  3. Execute the automated tests to ensure expected functionality

When finished, do not forget to:

1. Commit and Sync:
    - Switch to version control tab
    - Stage all changed files
    - _**Enter a commit message**_
    - Click Commit
    - Click Sync
2. Validate your submission in GitHub
3. Submit the final commit ID in D2L
