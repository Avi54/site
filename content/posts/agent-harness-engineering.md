---
title: "Agent Harness"
date: 2026-08-12
draft: false
tags:
  - Technology
  - AI
---
In his post ["Agent Harness Engineering"](https://addyosmani.com/blog/agent-harness-engineering/), Addy Osmani argues that conversations about AI coding tools have largely centered on the model itself. This discussion centers on answering questions like which one reasons best or which one writes the ideal code, but according to him, a model on its own is not an agent. It becomes one only once it is given a way to read and write files, run commands, and know when a task is actually finished. Osmani, building on a term coined by Trivedy, refers to this surrounding structure as the harness, which has become a common technical term.

## What the Harness Actually Is

Osmani mentions the following in the post, 

> Agent = Model + Harness. 

By this he means everything that isn't the model itself, the instructions it's given on startup, the tools it's allowed to call, the sandboxed environment, and the rules enforced at each step, such as a script that blocks a destructive command before it runs or one that runs a test suite after every edit (hooks). Osmani points out that tools like Claude Code often run on similar underlying models, yet behave differently, because the harness wrapped around each one differs. The model is one ingredient. The harness is the rest of the recipe, and per Osmani, it is where most of the actual engineering effort now goes.

The idea Osmani returns to throughout the piece isn't a specific technique but a discipline. Every mistake or unideal outcome the agent makes gets treated as permanent signal that should be avoided in the future. This implies the need for a rule to be established telling it never to do so again, and eventually a hook that checks for it automatically. If it runs a command it shouldn't have, that command gets blocked outright going forward. As he puts it, the harness a person ends up with reflects the specific history of what has gone wrong in their own work, which is why it can't simply be downloaded pre-built from someone else.

## Why Harnesses Must Persist Invariant of Model Improvement

Even a good enough model eventually doesn't make the harness unnecessary. Although Osmani concedes that models today plan and stay coherent over far longer stretches than previously, his central claim is that the harness doesn't shrink so much as move. As one class of task becomes reliable, models get pointed at harder tasks with new failure modes, and new scaffolding gets built to contain those instead. Every piece of a harness, he writes, encodes an assumption about what the model can't yet do alone. As that assumption stops holding, that piece should come out. As new capability opens up, new pieces are needed to reach it safely.

<!-- Osmani cites a data point that makes this concrete. On a coding benchmark, Trivedy documented the same model moving from a middling rank to a near-top rank once it was placed in a purpose-built harness instead of a default one, with no change to the model itself. That gap between what a model can do and what it appears to do in practice is, Osmani concludes, in large part a harness gap. -->

## References
Osmani, Addy. "Agent Harness Engineering." addyosmani.com, April 19, 2026, https://addyosmani.com/blog/agent-harness-engineering/