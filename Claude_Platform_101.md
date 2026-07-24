# Claude Platform --- Complete Study Notes

> A comprehensive revision guide covering the core concepts of the
> Anthropic Claude Platform.

------------------------------------------------------------------------

# Learning Roadmap

1.  Claude Platform
2.  Messages API
3.  Model Selection
4.  Agent Loop
5.  Tool Use
6.  Extended Thinking
7.  Built-in Tools
8.  Skills
9.  MCP
10. Context Management
11. Managed Agents
12. Building Managed Agents
13. Claude Code
14. Choosing the Right Feature
15. Production Best Practices
16. Interview Cheat Sheet

------------------------------------------------------------------------

# 1. Claude Platform

## Purpose

Build AI applications programmatically using Claude.

## Components

-   REST API
-   SDKs
-   CLI
-   Claude Console

## Three Layers

### Primitives (Build)

-   Messages API
-   Tool Use
-   Files
-   Web Search
-   Code Execution
-   MCP
-   Skills

### Infrastructure (Scale)

-   Managed Agents
-   Queues
-   Retries
-   Observability
-   Prompt Caching
-   Memory

### Controls (Operate)

-   Dashboards
-   Evaluations
-   Workspaces
-   Usage Limits
-   Logs

**Memory Trick:** Build → Scale → Operate

------------------------------------------------------------------------

# 2. Messages API

The foundation of every Claude application.

Core call:

`client.messages.create()`

## Important Parameters

  Parameter       Purpose
  --------------- ------------------
  model           Claude model
  messages        Conversation
  system          Behavior/persona
  max_tokens      Response limit
  tools           Available tools
  thinking        Enable reasoning
  output_config   Thinking effort

Response = content blocks (not plain text).

Common block types: - text - tool_use - tool_result - thinking -
server_tool_use

------------------------------------------------------------------------

# 3. Model Selection

## Haiku

Fast • Cheapest • High-volume

Use: - Classification - Routing - Extraction

## Sonnet ⭐

Best default.

Use: - Coding - Chatbots - Summaries - Most production apps

## Opus

Highest reasoning.

Use: - Planning - Debugging - Complex coding - Deep analysis

## Fable

Maximum capability. Use only when worth the cost.

## Selection Strategy

Haiku → Sonnet → Opus → Fable

Always benchmark on 20--30 real examples.

------------------------------------------------------------------------

# 4. Agent Loop

Agent = Claude repeatedly reasons until task completion.

Flow

User → Reason → Tool? → Execute → Return Result → Repeat → end_turn

Important: - tool_use = execute tool - end_turn = finished

Claude reasons. Your application executes.

------------------------------------------------------------------------

# 5. Tool Use

Tool = Function exposed to Claude.

Contains: - Name - Description - Input Schema

Golden Rule: Good descriptions produce good tool selection.

------------------------------------------------------------------------

# 6. Extended Thinking

Purpose: Improve reasoning quality.

Enable: thinking={"type":"adaptive"}

Effort: low → medium → high → xhigh → max

Use for: - Math - Planning - Debugging - Trade-offs

Avoid: - Simple extraction - Classification

------------------------------------------------------------------------

# 7. Built-in Tools

## Server Tools

Hosted by Anthropic.

-   Web Search
-   Code Execution
-   Web Fetch

No manual loop.

## Client Tools

Run locally.

-   Memory
-   Bash

------------------------------------------------------------------------

# 8. Skills

Skill = Reusable procedure.

Contains: - SKILL.md - Scripts - Resources

Tools = What Claude can do. Skills = How Claude should do it.

------------------------------------------------------------------------

# 9. MCP

Model Context Protocol.

Purpose: Connect Claude to third-party services.

Examples: Slack, GitHub, Linear, Asana.

Comparison:

-   Tools → Your systems
-   Skills → Your workflow
-   MCP → Third-party services

------------------------------------------------------------------------

# 10. Context Management

Context includes: - System Prompt - Messages - Tools - Files - Skills -
Thinking

Patterns

1.  Just-in-Time Context
2.  Server-side Compaction
3.  Prompt Caching
4.  Memory

Use all four together in production.

------------------------------------------------------------------------

# 11. Managed Agents

Anthropic hosts: - Agent loop - Sandbox - Tool execution - Recovery

Core primitives: - Agent - Environment - Session - Events

------------------------------------------------------------------------

# 12. Building Managed Agents

Workflow

Create Agent → Create Environment → Create Session → Open Stream → Send
Event → Receive Events → session.status_idle

Open the stream BEFORE sending the first event.

------------------------------------------------------------------------

# 13. Claude Code

Terminal coding agent.

Can: - Edit files - Run code - Fix errors - Generate SDK integrations

Prompt should specify: - File - Pattern - Desired outcome

------------------------------------------------------------------------

# Choosing the Right Feature

  Need                      Feature
  ------------------------- ----------------
  External data             Tool
  Third-party integration   MCP
  Company SOP               Skill
  Better reasoning          Thinking
  Persistent knowledge      Memory
  Lower costs               Prompt Cache
  Long automation           Managed Agents
  Code generation           Claude Code

------------------------------------------------------------------------

# Production Best Practices

-   Default to Sonnet.
-   Benchmark models before deployment.
-   Minimize context.
-   Retrieve information just-in-time.
-   Cache stable prompts.
-   Write precise tool descriptions.
-   Store long-term state in Memory.
-   Prefer MCP over custom third-party integrations.
-   Use Skills for repeatable business workflows.
-   Use Managed Agents for long-running jobs.
-   Monitor token usage and latency.

------------------------------------------------------------------------

# Common Mistakes

-   Using Opus for simple tasks.
-   Loading unnecessary context.
-   Vague tool descriptions.
-   Hardcoding API keys.
-   Ignoring token usage.
-   Using Skills instead of Tools (or vice versa).
-   Forgetting to open managed-agent streams before sending events.

------------------------------------------------------------------------

# Interview Cheat Sheet

**Messages API** --- Core API.

**Tool** --- Claude requests, app executes.

**Skill** --- Reusable procedure.

**MCP** --- Third-party integration protocol.

**Thinking** --- Step-by-step reasoning.

**Memory** --- Cross-session persistence.

**Prompt Cache** --- Reduce repeated token costs.

**Managed Agent** --- Anthropic-hosted agent loop.

**Session** --- Single agent execution.

**Environment** --- Sandbox.

**Event Stream** --- Communication channel.

------------------------------------------------------------------------

# Final Architecture

User ↓ Application ↓ Messages API ↓ Claude

Optional capabilities: - Tools - Skills - MCP - Thinking - Built-in
Tools - Context Management - Managed Agents - Claude Code

------------------------------------------------------------------------

# One-Page Revision

-   Messages API is the foundation.
-   Sonnet is the best default model.
-   Tools = Actions.
-   Skills = Procedures.
-   MCP = Third-party integrations.
-   Thinking = Better reasoning.
-   Memory = Long-term knowledge.
-   Prompt Cache = Lower cost.
-   Managed Agents = Hosted agent loop.
-   Claude Code = AI coding assistant.
-   Context Management keeps costs low and avoids token limits.
