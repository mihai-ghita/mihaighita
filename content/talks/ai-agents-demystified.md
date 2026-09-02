---
title: "AI Agents, Demystified"
date: 2026-09-02
draft: false
description: "Seven words you keep hearing — chat history, context, skill, tool call, agent, sandbox, MCP — and the plain architecture behind each one."
slides: "/talks/ai-agents-demystified/presentation.html"
---

There is no magic here. Every one of those seven words — chat history, context, skill, tool call, agent, sandbox, MCP — is a boring engineering solution to a boring engineering constraint, and they build on each other in exactly that order:

- The model is stateless, so we invented **chat history**.
- History grows without limit, so we care about **context**.
- Context is finite but instructions are many, so we load them on demand as **skills**.
- The model can only emit text, so we invented **tool calls**.
- One tool call is rarely enough, so we wrapped it in a loop and called it an **agent**.
- The loop now runs code we never reviewed, so we need a **sandbox**.
- Everyone writes the same tools over and over, so we standardised on **MCP**.

This talk walks through each concept in that order, with the architecture behind it, so none of these words have to be magic anymore.
