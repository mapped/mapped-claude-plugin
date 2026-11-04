# Mapped Plugin for Claude

Connects Claude to [Mapped](https://www.mapped.com)'s building data graph
through Mapped's hosted MCP server, so you can ask about your sites, buildings,
floors, spaces, equipment, sensors and points in plain language and get answers
from your own data.

## What it does

The plugin adds one remote MCP server, `mapped`, with six tools:

| Tool | What it does |
| --- | --- |
| `graphql_gen` | Turns a natural-language request into a Mapped GraphQL query without running it |
| `graphql_gen_with_results` | Generates the query and runs it against the Mapped API, returning both the query and its data |
| `get_all_children_types` | Lists every descendant of an entity type in the Mapped ontology |
| `search_entity_types` | Finds entity types by the tags in their names |
| `get_entity_type_details` | Returns a type's description, parents, properties and relationships |
| `list_user_orgs` | Lists the orgs in your Mapped account |

Everything runs as you. The server can read, and through GraphQL mutations
write, only what your Mapped account is already allowed to.

## Install and sign in

Install it from the Claude plugin directory, or in Claude Code:

```
/plugin install mapped-mcp --marketplace mapped/mapped-claude-plugin
```

Then run `/mcp`, select the `mapped` server and choose **Authenticate**. A
browser window opens for Mapped sign-in; once you approve, the tools above are
available. **Clear authentication** in the same menu signs you out.

## Sign-in and what the plugin sends

- **Authentication** is OAuth 2.1 through Mapped SSO (`https://sso.mapped.com`)
  with PKCE and a Client ID Metadata Document. The plugin ships no credential
  and asks for none: no API key, client secret or client registration. Claude
  stores and refreshes the token.
- **Every tool call** goes over HTTPS to `https://mcp.mapped.com/mcp` with your
  OAuth token. That includes the text of your request, any generated GraphQL
  and its variables, and the tool's result comes back the same way. The server
  calls Mapped's GraphQL API on your behalf and returns the data to Claude.
- **Nothing else.** The plugin has no hooks, scripts or executables, runs
  nothing on your machine, and sends data to no destination other than
  Mapped's servers.

Mapped's [privacy policy](https://www.mapped.com/legal/privacy-policy) and
[customer agreement](https://www.mapped.com/legal/CustomerAgreement) apply to
the data the server handles.

## Prerequisites

A Mapped account with access to at least one org.

## License

[MIT](./LICENSE).

Claude is a trademark of Anthropic, PBC. Mapped is not affiliated with or
endorsed by Anthropic.
