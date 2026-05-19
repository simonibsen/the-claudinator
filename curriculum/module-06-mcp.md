# Module 6 — MCP: Use, Then Build a Server

**Frame:** Model Context Protocol is how an agent reaches outside its sandbox — to your tools, your data, your APIs. Using an MCP server is easy; building one teaches you how agents *actually* work.

## Objectives

1. Explain what MCP is, what problem it solves, and how it differs from "just call an API."
2. Know the three server primitives: **tools** (actions), **resources** (read-only data), **prompts** (parameterized prompt templates).
3. Know the two transports: **stdio** (local subprocess) and **Streamable HTTP** (remote, with OAuth 2.1 auth).
4. Install and use at least 2 existing reference MCP servers productively.
5. Build a small MCP server in Python or TypeScript exposing real functionality.
6. Design tool schemas that the model can actually use (vs. ones that confuse it).
7. Understand the security model: tools are *capabilities* you grant.

## Readings

- `modelcontextprotocol.io` — the spec and quickstart at `modelcontextprotocol.io/quickstart/server`.
- `modelcontextprotocol.io/docs/learn/architecture` — server primitives (tools / resources / prompts) and client primitives (sampling / elicitation / logging).
- `modelcontextprotocol.io/examples` — current reference servers list.
- One reference server source (e.g. Filesystem, Fetch, Git) — read it.
- "How to write a good function schema" — Anthropic's tool-use docs.

## Exercises

**1. Install + use.** Install 2-3 of the current reference servers: Everything, Fetch, Filesystem, Git, Memory, Sequential Thinking, or Time. Use them for real tasks. Notice latency, where it shines, where it's awkward.

> Note: GitHub and Postgres are no longer maintained as reference servers — they're in `modelcontextprotocol/servers-archived`. GitHub now has an official integration maintained by GitHub itself; database access typically goes through specialized servers.

**2. Server design sketch.** Pick a tool/API you wish Claude could use natively — your school's API, a personal API, Strava, Anki, whatever. Sketch the tool surface on paper: what 4-6 tools should it expose? What's each tool's name, args, returns? Consider whether any belong as **resources** (read-only data) or **prompts** (templates) instead of tools.

**3. Build the server.** Implement the sketch using:
- **Python:** `uv add "mcp[cli]"`, build with the `FastMCP` class from `mcp.server.fastmcp` (the high-level pattern shown in the official quickstart).
- **TypeScript:** `npm install @modelcontextprotocol/sdk zod`, build with the official SDK.

Start with 2 tools. Test by wiring into Claude Code and using it. Default to **stdio transport** for local development.

**4. Schema iteration.** Watch how the model uses your tools. Where does it get confused? Refine descriptions, arg names, return shapes. This is the real work.

**5. Auth & permissions.** For stdio servers: env vars or a token file, never hardcoded. For HTTP-transport (remote) servers: implement **OAuth 2.1** per the MCP spec. Document the install flow.

## Deliverable

- A public GitHub repo: MCP server with README, install instructions, and example usage
- The server wired into your local Claude Code, used in at least 3 real sessions
- A short writeup: "things the model got wrong with my tools, and how I fixed the schemas"

## Self-assessment

1. Why MCP and not "just call the API"? What does the protocol give you?
2. What's the difference between a tool, a resource, and a prompt in MCP? Give an example of each from your server.
3. What makes a tool schema *the model can use* vs. *the model gets confused by*?
4. How should you write a tool description so the model picks it for the right tasks?
5. Your server returns 50KB of JSON for one call. What's wrong? What do you do?
6. stdio vs. Streamable HTTP — when do you pick which? What auth pattern goes with HTTP?
7. What's the security risk of an MCP server with write access, and how do you mitigate it?

## Common pitfalls

- **Too many tools.** 20 micro-tools confuse the model. 5 well-shaped tools work better.
- **Vague descriptions.** "Get data" — get what data, when?
- **Returning everything.** Page, filter, summarize. The model has limited context.
- **No idempotency.** If a tool can be retried, it should be safe to retry.

## Stretch

Write a Claude Desktop / Claude Code config that auto-installs your server for a teammate (a one-line install). Bonus points: publish to a registry if one exists for your language.
