0️⃣ GLOBAL GUARDRAILS PROMPT (RUN FIRST)

👉 Paste this once at the start of the Copilot chat.

🛡️ SYSTEM / GUARDRAILS PROMPT

You are operating in Agent Mode as a Principal Engineer in an enterprise environment.

Hard rules you must follow:

No assumptions

If information is missing, create explicit extension configuration or TODOs.

Never invent org mappings or libraries.

Deterministic-first

Prefer AST parsing, static analysis, config inspection.

Use MCP (Confluence / Copilot) only when required.

Incremental output

Generate code phase-by-phase only when asked.

Do NOT jump ahead.

Enterprise safety

Never overwrite files without preview logic.

Always support dry-run.

Always mark unsupported migrations.

Code quality

Production-grade TypeScript.

Explicit types.

Clear separation of concerns.

Acknowledge these rules internally and wait for Phase 1 instructions.

Why this matters

This forces Claude Opus to:

Slow down

Stop hallucinating mappings

Respect phase boundaries
(It makes a huge difference.)

1️⃣ PHASE 1 — EXTENSION SCAFFOLD & COMMANDS

👉 Run after guardrails prompt.

🔹 PHASE 1 PROMPT — VS CODE EXTENSION FOUNDATION

Phase 1 Objective

Generate only the VS Code extension foundation.

Scope (DO NOT EXCEED):

package.json

extension.ts

Command registration

Activation events

Configuration schema

Empty folder structure

DO NOT generate:

AST logic

MCP calls

Migration logic

Functional Requirements

Commands:

angularToReact.startMigration

angularToReact.dryRun

User inputs:

Target React version (enum + custom)

Migration scope (app | module | folder)

Dry-run toggle

Configuration:

Enable/disable MCP usage

Mapping cache path

Folder structure:

src/
├─ extension.ts
├─ commands/
├─ agents/
├─ mcp/
├─ utils/
└─ ui/


Output rules

Generate real code

One file at a time

Explain file purpose briefly before each file

Begin Phase 1 now.

✅ Stop here after Phase 1 completes
Don’t proceed until code looks clean.

2️⃣ PHASE 2 — ANGULAR ANALYSIS & DEPENDENCY CLASSIFICATION

👉 Run only after Phase 1 is done.

🔹 PHASE 2 PROMPT — ANGULAR INTELLIGENCE LAYER

Phase 2 Objective

Implement read-only analysis agents for Angular projects.

Scope

Implement the following agents:

1. AngularAnalyzerAgent

Uses TypeScript Compiler API

Detects:

Components

Modules

Services

Pipes

Directives

Extracts:

selector

templateUrl / inline template

inputs / outputs

injected services

2. DependencyClassifierAgent

Classifies imports as:

INTERNAL_COMPONENT

INTERNAL_LIBRARY

THIRD_PARTY_ANGULAR

THIRD_PARTY_GENERIC

Signals to use:

package.json

node_modules resolution

tsconfig path aliases

workspace-relative imports

Rules

No code generation or file writing

Analysis only

No MCP calls yet

Output

Agent classes

Shared types/interfaces

Example JSON output of analysis

Generate Phase 2 code now.

Why Phase 2 is isolated

This guarantees:

You know exactly what the app contains

No premature React assumptions

Clean boundary before MCP reasoning

3️⃣ WHAT COMES NEXT (FYI)

When you’re ready, next phases would be:

Phase 3 — Confluence MCP Mapping Resolver
Phase 4 — React Code Generator
Phase 5 — Validation, Diff & Safety
Phase 6 — Enterprise Enhancements (Nx, MFE, SSR)

Each phase gets its own prompt.

🔥 Pro tip (important)

If Copilot starts drifting, reset with:

“You violated phase scope. Roll back to Phase X and regenerate only missing pieces.”

Claude Opus responds very well to this.

If you want, next I can:

Write Phase 3 MCP mapping prompt

Design a standard org mapping schema

Add Angular → Next.js vs CRA decision logic

Just tell me what’s next.

Write propmts till phase 5

You got it. Below are clean, enterprise-safe prompts for Phase 3 → Phase 5, written to minimize hallucination, enforce boundaries, and keep Claude Opus 4.5 fully under control in Copilot Agent mode.

These are drop-in prompts — run them sequentially only after the previous phase is complete and reviewed.

3️⃣ PHASE 3 — CONFLUENCE MCP MAPPING RESOLVER

👉 Run only after Phase 2 is stable

🔹 PHASE 3 PROMPT — ORG KNOWLEDGE & MAPPING INTELLIGENCE

Phase 3 Objective

Implement a Mapping Resolver layer that uses Atlassian / Confluence MCP as the source of truth for Angular → React mappings.

Scope

Implement:

1. MappingResolverAgent

Responsibilities:

Query Confluence MCP to resolve:

Internal Angular libraries → React libraries

Internal Angular components → React components

Pipes → hooks / utilities

Return structured mapping results

2. Mapping Cache

Local JSON cache:

Read-through cache

Write only on confirmed MCP responses

No hardcoded org mappings

3. MCP Client (Confluence)

Abstracted MCP client

Explicit query methods

Typed responses

MCP Query Rules

Queries must be explicit and verifiable

Example:

“Is @org/ui-button an internal Angular library?
If yes, what is its React equivalent and package name?”

If MCP returns no answer:

Mark mapping as UNRESOLVED

Require manual intervention

Rules

DO NOT generate React code

DO NOT assume mappings

DO NOT modify files

No Copilot MCP usage in this phase

Output

MappingResolverAgent.ts

confluenceClient.ts

mappingCache.ts

Typed mapping interfaces

Example MCP queries & responses

Generate Phase 3 code now.

Why this phase is critical

This ensures:

Org knowledge is authoritative

No silent wrong migrations

Clear auditability for compliance

4️⃣ PHASE 4 — REACT CODE GENERATION (CONTROLLED)

👉 Run only after mappings are verified

🔹 PHASE 4 PROMPT — REACT MIGRATION ENGINE

Phase 4 Objective

Implement React code generation agents using Copilot MCP, guided strictly by:

Angular analysis output

Confirmed mappings from Phase 3

User-selected React version

Scope

Implement:

1. ReactGeneratorAgent

Responsibilities:

Convert Angular components → React function components

Use mapping registry for internal components

Generate idiomatic React per selected version

2. Template Converter

Convert:

Angular templates → JSX

Structural directives:

*ngIf → conditional rendering

*ngFor → .map()

3. Logic Mapping

Convert:

@Input() → props

@Output() → callbacks

Angular services → hooks or context

RxJS → useEffect, useMemo, or retained observables

Copilot MCP Usage Rules

Use Copilot MCP only for:

JSX generation

Hook best practices

All prompts must include:

React version

Strict mode preference

Safety Rules

If mapping is UNRESOLVED:

Insert TODO comments

Do NOT generate incorrect code

Unsupported Angular patterns:

Flag explicitly

Skip generation

Output

ReactGeneratorAgent.ts

Template conversion utilities

Example generated React component

Inline TODO markers

Generate Phase 4 code now.

Why this is safe

React generation is mapping-driven

No hallucinated replacements

Explicit manual escape hatches

5️⃣ PHASE 5 — VALIDATION, DIFF & SAFETY LAYER

👉 Run after React generation works

🔹 PHASE 5 PROMPT — ENTERPRISE SAFETY & VERIFICATION

Phase 5 Objective

Implement a Validation & Safety layer that ensures:

No destructive changes

Full auditability

Clear developer control

Scope

Implement:

1. ValidationAgent

Responsibilities:

Verify:

All imports resolve

No unresolved mappings

React version compatibility

2. Dry-Run Engine

Compute:

File additions

File deletions

File modifications

No filesystem writes

3. Diff Viewer

Show unified diffs

Group by module / feature

4. Error & Warning Reporter

Unsupported Angular features

Missing mappings

Manual steps required

Rules

DO NOT auto-apply changes

All writes must be user-approved

No MCP calls in this phase

Output

ValidationAgent.ts

DryRunEngine.ts

Diff utilities

Example validation report

Generate Phase 5 code now.

🧠 What you have after Phase 5

You now own:

A safe Angular → React migration engine

MCP-powered org intelligence

Deterministic analysis + controlled LLM generation

Enterprise-grade audit trail

This is exactly how large companies would build this internally.

Next (optional but powerful)

If you want, I can:

Add Nx / monorepo intelligence

Add Angular Universal → Next.js routing

Add telemetry & migration metrics

Design a CI-driven migration mode

Just tell me what phase you want next.
