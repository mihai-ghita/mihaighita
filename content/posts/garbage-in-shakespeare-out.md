---
title: "Garbage In, Shakespeare Out?"
date: 2026-03-15
draft: false
description: "Why does your AI keep producing bad code despite a capable model? The answer is almost always in your workflow, not the model itself."
---

"**Garbage In, Garbage Out**" is the classic warning. But working with AI coding agents has introduced a more dangerous myth: that the model is powerful enough to produce Shakespeare even when you feed it garbage.

I've made every one of these mistakes myself. The good news is that none of them require a new tool or a better model to fix — just a few deliberate shifts in how you set things up.

If your AI keeps producing code that misses the mark, you're probably stuck in one of these four traps: 
- **Tooling Overload** — too many MCP servers active at once
- **The Long Chat Trap** — keeping one chat open for hours
- **The "Mind Reader" Expectation** — vague, underspecified prompts
- **Context Stuffing** — tagging entire folders as context

## Tooling Overload
It is incredibly tempting to install every Model Context Protocol (MCP) server available the moment you set up your agent. We assume that giving the AI access to our database, GitHub, Slack, Jira, and file system all at once will make it a super-developer.

### The issue
This is a trap that directly leads to context bloat and model confusion. When an agent has too many tools, it struggles to decide which one to use. It wastes tokens searching through irrelevant data or hallucinates ways to combine tools that don't make sense.

### Example
> You ask your agent to "Fix the bug where user sessions expire too early." You have the GitHub, Jira, Postgres, and Slack MCPs all active. Instead of opening session_manager.py and adjusting the TTL constant, the agent queries your Postgres database for active sessions, then searches Jira for related tickets, then checks Slack history for reports of the issue — and finally suggests a database schema migration as the fix. The real problem? A single off-by-one error on a timeout value. Three tools, zero relevant context, and a wildly overcomplicated solution.

### The solution
Enable tools only when you actually need them. If you are doing pure logic changes in your codebase, turn off the external integration tools. Stick to highly targeted tools for the task at hand.

## The Long Chat Trap
This trap occurs when developers end up keeping one chat window open for a few hours. They expect the AI to be able to switch focus one task to another and to be careful with all instructions.

### The issue
The problem is that we hate feeling like we've wasted time. You might think, "I've already spent an hour explaining my code to the AI, I shouldn't start a new chat now!" But keeping that long chat open actually makes things worse.

The AI remembers everything in that chat—including all the broken code, dead ends, and mistakes from the last hour. Eventually, its memory gets so cluttered with bad information that it gets totally confused. It can no longer tell the difference between the bad code you tried 30 minutes ago and the actual fix you want right now.

### Example
> Imagine you are trying to optimize a slow, complex SQL query for your daily analytics job. You try three different indexing and JOIN strategies with the AI in one long chat thread. None of them work perfectly. By the fourth attempt, the AI gets confused and starts suggesting query fragments from the very first approach—the one you explicitly proved caused a bottleneck an hour ago. You end up typing: "No, I told you 20 messages ago that table scan is too slow!" You are no longer coding; you are just arguing with the AI.

### The solution
* Adopt the Golden Rule: Remember that one task equals one chat. Keep your sessions hyper-focused on a single objective.  
* Stop Fighting the AI: If the agent gets confused, don't argue with it. Attempting to correct a deeply confused model in a bloated chat thread rarely works.  
* Start Fresh: Simply restart the session. You will be much more productive if you explore possible solutions in a fresh chat rather than trying to salvage a broken one.  

## The "Mind Reader" Expectation
Using vague prompts like "Fix this" or "Optimize this service" is a guaranteed way to get poor results. We often treat AI like a senior engineer who has been at the company for 5 years and implicitly knows our unwritten backend standards.

### The issue
Your AI is not a mind reader. If you don't explicitly state your architectural preferences, ORM rules, and logging standards, the AI will just guess—and its guess will likely clash with your codebase.

### Example
> You highlight a buggy data-fetching service and tell the AI: "Refactor this."
The AI confidently refactors it, but swaps out your SQLAlchemy queries for raw SQL strings, changes your asynchronous functions to synchronous ones, and entirely removes your custom Datadog tracing middleware because you didn't tell it to keep it.

### The solution
* Prioritize specification over conversation.
* Create an AGENTS.md file in your repository to serve as a "Standard Operating Procedure" (detailing your tech stack, database transaction rules, and error-handling standards).
* Use a "Plan Mode" agent first, which forces the AI to write out a step-by-step plan for your approval before it generates a single line of code.

## Context Stuffing
There is a widespread misconception in the developer community that "more context is always better." When faced with a bug, developers will tag the entire src folder, hoping the AI will figure it out.

### The issues
**Lost in the Middle** — Models reliably recall information near the start and end of a prompt, but frequently miss details buried in the center. A critical bug description on line 1 and the fix on the last file — the model will likely act on those. Everything in between? A coin flip.

**Context Dilution** — The more unrelated code you include, the more the model "waters down" its attention on what actually matters. Your core instruction gets weaker relative to the noise, and the model starts solving the loudest problem in the context, not the one you described.

### Example 
> You need to fix a bug where a user's profile avatar isn't being saved. To be "thorough," you add to the context profile_controller.py, user_model.py, auth_middleware.py, storage_service.py, and your full settings.py. The agent gets drawn to an unrelated S3 bucket misconfiguration it spotted in settings.py and proposes a full file-upload refactor — instead of catching the single missing await on the storage call in profile_controller.py.

### The solution:
* Only provide the exact files relevant to the specific bug.
* Instead of having a large, sprawling conversation to fix the AI's mistakes, rollback your code changes, tweak your initial prompt, and try again.
* Your end goal: Always strive to have a successful one-shot prompt.

## Wrapping Up
AI coding agents are incredibly powerful, but they aren't magic. The secret to getting great code isn't about whispering the perfect, magical prompt; it's about keeping things organized.

By making these small shifts to your workflow, you will stop endlessly arguing with your AI and start shipping features faster. And who knows? If you stop feeding it garbage, you might actually get a little Shakespeare out of it instead of a comedy.