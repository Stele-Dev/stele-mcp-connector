# Stele — MCP connector plugin

[Stele](https://stele-ai.dev) is shared project memory and work tracking for AI
agents and the people who work with them. It keeps decisions, lessons, risks,
documents, components, and tasks in one durable knowledge graph, so work can
continue across agent clients without losing the project's history.

This repository is the plugin that connects an agent client to Stele. It follows
the [Agent Plugins](https://agent-plugins.org) open standard and contains
configuration and documentation only.

## What's in here

```
plugin.json          Agent Plugins manifest
mcp.json             Stele's hosted MCP server, over Streamable HTTP
skills/stele/        Guidance on when and how an agent should use Stele
```

There is no build step, no bundled binary, and no executable code. Stele itself
runs as a hosted service; this plugin only points at it.

## What the connector does

Once connected, an agent can:

- **Recall** what a project already knows before it acts, instead of starting cold.
- **Trace** why a decision was made, what caused it, and what it replaced.
- **Capture** decisions, lessons, risks, and gaps as they happen, so they survive
  the conversation that produced them.
- **Coordinate** tasks — create, claim, and complete them — so two agents don't
  duplicate each other's work.
- **Hand off** cleanly to the next agent, session, or teammate.

The bundled skill tells the agent when reaching for these tools is appropriate
and when it isn't, which matters on a surface where the agent chooses for itself.

## Requirements

A Stele account and at least one project. Signing in through the connector
creates the account if you don't already have one, and no paid plan is required
to connect.

## Authentication

OAuth 2.1 with dynamic client registration ([RFC 7591](https://datatracker.ietf.org/doc/html/rfc7591)).
Your client registers itself on first connection and opens Stele's sign-in page.
Access is limited to the projects you own or belong to.

**No credentials, tokens, or secrets are stored in this repository**, and none
are needed to install it.

## Tool safety

Stele's tools are split so a client can tell safe operations from unsafe ones.
Read-only tools are annotated as such and never modify data. Write tools are
separate. Every consequential operation — cancelling, force-claiming, unlinking,
retiring, merging — lives in a single `destructive` tool that always prompts
before acting. No tool mixes these tiers.

## Links

- [Documentation](https://stele-ai.dev/docs)
- [Privacy policy](https://stele-ai.dev/privacy)
- [Support](https://stele-ai.dev/support)

## License

MIT — see [LICENSE](LICENSE).
