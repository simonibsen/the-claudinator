# Week 6 — MCP: Use, Then Build a Server

**Frame:** Model Context Protocol is how an agent reaches outside its sandbox — to your tools, your data, your APIs. Using an MCP server is easy; building one teaches you how agents *actually* work.

## Objectives

1. Explain what MCP is, what problem it solves, and how it differs from "just call an API."
2. Install and use at least 2 existing MCP servers productively.
3. Build a small MCP server in Python or TypeScript exposing real functionality.
4. Design tool schemas that the model can actually use (vs. ones that confuse it).
5. Understand the security model: tools are *capabilities* you grant.

## Readings

- `modelcontextprotocol.io` — the spec and quickstart.
- One reference server (e.g. `github`, `filesystem`, `postgres`) — read its source.
- Anthropic's posts on MCP, if available.
- "How to write a good function schema" — search Anthropic's docs.

## Exercises

**1. Install + use (1.5 hrs).** Install 2-3 MCP servers (filesystem, GitHub, a database one). Use them for real tasks. Notice latency, where it shines, where it's awkward.

**2. Server design sketch (1 hr).** Pick a tool/API you wish Claude could use natively — your school's API, a personal API, Strava, Anki, whatever. Sketch the tool surface on paper: what 4-6 tools should it expose? What's each tool's name, args, returns?

**3. Build the server (4 hrs).** Implement the sketch in Python (`mcp` SDK) or TypeScript. Start with 2 tools. Test by wiring it into Claude Code and using it.

**4. Schema iteration (1.5 hrs).** Watch how the model uses your tools. Where does it get confused? Refine descriptions, arg names, return shapes. This is the real work.

**5. Auth & permissions (1 hr).** If your server needs credentials: don't hardcode. Use env vars or a token file. Document the install flow.

## Deliverable

- A public GitHub repo: MCP server with README, install instructions, and example usage
- The server wired into your local Claude Code, used in at least 3 real sessions
- A short writeup: "things the model got wrong with my tools, and how I fixed the schemas"

## Self-assessment

1. Why MCP and not "just call the API"? What does the protocol give you?
2. What makes a tool schema *the model can use* vs. *the model gets confused by*?
3. How should you write a tool description so the model picks it for the right tasks?
4. Your server returns 50KB of JSON for one call. What's wrong? What do you do?
5. What's the security risk of an MCP server with write access, and how do you mitigate it?

## Common pitfalls

- **Too many tools.** 20 micro-tools confuse the model. 5 well-shaped tools work better.
- **Vague descriptions.** "Get data" — get what data, when?
- **Returning everything.** Page, filter, summarize. The model has limited context.
- **No idempotency.** If a tool can be retried, it should be safe to retry.

## Stretch

Write a Claude Desktop / Claude Code config that auto-installs your server for a teammate (a one-line install). Bonus points: publish to a registry if one exists for your language.
