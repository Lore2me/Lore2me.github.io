---
layout: post
title: Clean Architecture
date: 2024-07-03 11:20 +0200
categories: [Knowledge, Coding, Architecture]
tags: [coding, architecture, clean-code]
description: "In this post we will talk about Clean Architecture and how it can help you to design software systems that are easy to understand, easy to maintain, and easy to test."
---
Clean Architecture is not fully specified.
So in this post I will try to explain what Clean Architecture is with specific items which are part of it.

# Flexible Architecture

Separation of concerns
-----------------------
Divide your system into distinct features with as little overlap in functionality as possible,
so that they can be combined freely.
This will make your system easier to understand, easier to maintain, and easier to test.  

Software reflects user's mental model
-------------------------------------
The software should reflect the user's mental model of the system.
When the structure and the interactions inside the software match the user's mental model,
changes in the real world can more easily be applied in software.

Abstraction
-----------
Abstraction is the process of hiding the implementation details of a system behind a well-defined interface.
Separating ideas from specific implementations provides the flexibility to change the implementation.
But beware of "ambiguous interfaces."

Prefer composition to inheritance
----------------------------------
Inheritance increases coupling between parent and child, thereby limiting reuse.

Tangle-/cycle-free dependencies
-------------------------------
The dependency graph of the elements of the architecture has no cycles, thus allowing locally bounded changes.

# Workflow
Use a top-down approach to find the architecture.

### 1. Context
What belongs to your system and what does not? Which external services will you use?

### 2. Break down into parts
Split the whole into parts by applying separation of concerns and the single-responsibility principle.

### 3. Communication
Which data flows through which call, message or event from one part to another?
What are the properties of the channels (sync/async, reliable/unreliable, etc.)?

### 4. Repeat for each part
Repeat the above-mentioned three steps for each part as if it were your system.
A part is a bounded context, subsystem, or component.

# Defer decisions
Decide only things you have enough knowledge about.
Otherwise find a way to defer the decision and build up more knowledge.
A good architecture allows you to defer most decisions until you have enough knowledge.

Remember the following statement: "Decide as late as possible, but not too late."
Why?
Because the more you know, the better your decisions will be.
A side of this, the more time you spend in your project, the more the architecture and the requirements will change.
Means that the decisions for now won't be the best decisions in the future.

# Architecture influencing forces
- Quality 
