# Morphe MCP server

Morphe captures what your experts know, through voice conversations with an AI interviewer, and
turns it into living knowledge bases your organization keeps when they retire or move on.

The Morphe MCP server brings that knowledge into GitHub Copilot and any other MCP client. Ask
questions and get answers grounded in what your experts actually said, with every answer citing the
chapter and section it came from.

This repository describes the hosted server. Morphe's source code is not public.

## What it can do

The server is **read-only** and scoped to **one organization**, the one you approve when you sign in.

| Tool | What it does |
| --- | --- |
| `whoami` | Shows which organization and user the connection acts for. |
| `list_knowledge_bases` | Lists the organization's knowledge bases, or finds the ones about a subject or a person. |
| `get_knowledge_base_outline` | Shows a knowledge base's chapters, with a summary of each. |
| `search_sections` | Searches the chapters by keyword (in the knowledge base's language). |
| `read_chapter` | Reads one chapter in Markdown, images included. |
| `list_capture_plans` | Lists each expert's capture plan and how far along it is. |
| `get_capture_plan` | Shows one plan's topics and which ones are covered. |
| `list_plan_sessions` | Lists a plan's sessions and the topics each one discussed. |
| `get_session_transcript` | Returns the verbatim transcript of one session. |

Topics that are planned but not captured yet are reported as open questions, never as answers, so
the assistant tells you what isn't documented instead of guessing.

## Requirements

- A Morphe account in an organization where MCP connections are enabled. Your Morphe
  administrator can check this under **Connectors** in the account menu.
- An MCP client that supports remote servers over streamable HTTP with OAuth, such as GitHub
  Copilot in VS Code or the Copilot CLI.

## Set it up

The server URL is the same for every organization:

```text
https://morphe.vooban.com/api/mcp
```

### GitHub Copilot in VS Code

Install Morphe from the GitHub MCP Registry, or add it to `.vscode/mcp.json` (or your user
configuration):

```json
{
  "servers": {
    "morphe": {
      "type": "http",
      "url": "https://morphe.vooban.com/api/mcp"
    }
  }
}
```

Start the server. Morphe's sign-in opens in your browser: sign in, pick the organization, and
approve read-only access. Then use Copilot Chat in **Agent** mode.

### GitHub Copilot CLI

```bash
copilot mcp add --transport http morphe https://morphe.vooban.com/api/mcp
```

The first time Copilot uses Morphe, it asks you to sign in.

### Other clients

Any client that supports remote MCP servers with OAuth works the same way: add the server URL and
sign in when prompted. The [setup guide](https://morphe.vooban.com/docs/en/guides/connect-ai-assistants/)
covers Claude, ChatGPT, Codex and Microsoft 365 Copilot.

## Use it

Talk to Copilot as usual. It decides when to look in Morphe, and you can ask it things like:

- "Which knowledge bases do we have on equipment maintenance?"
- "What did our expert say about the spring shutdown procedure?"
- "Which experts' capture plans are at risk of not finishing before they leave?"

Answers cite their source as « Chapter › Section », so you can open it in Morphe.

## Security and privacy

- **Read only:** the server can't change anything in Morphe.
- **Your access, nothing more:** it sees exactly the knowledge bases you can open in Morphe, in the
  organization you picked. To use another organization, connect again and pick it.
- **Disconnect at any time:** in Morphe, open your account menu, then **Connectors**, and select
  **Disconnect**. The assistant loses access immediately.

## Links

- Website: <https://morphe.vooban.com/en>
- Setup guide: <https://morphe.vooban.com/docs/en/guides/connect-ai-assistants/>
- FAQ: <https://morphe.vooban.com/docs/en/faq/>
- Support: <morphe-support@vooban.com>
- Privacy policy: <https://vooban.com/en/privacy-policy>
- Terms of service: <https://morphe.vooban.com/en/terms>

Morphe is built by [Vooban](https://vooban.com).
