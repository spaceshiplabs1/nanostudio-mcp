# Nano Studio Pro — MCP server

Connect AI agents to [Nano Studio Pro](https://nanostudiopro.com), an AI
product-photography studio: generate, restyle, cut out, upscale, animate,
import, and search product images, organized into projects.

The server itself is hosted — there is nothing to build or run from this
repository. This repo carries the install manifests and pointers.

- Full documentation: https://nanostudiopro.com/docs/mcp
- Server card: https://nanostudiopro.com/.well-known/mcp/server-card.json
- Official registry entry: `com.nanostudiopro/studiopro`

## Remote server (recommended)

Endpoint: `https://nanostudiopro.com/api/mcp` — Streamable HTTP with
OAuth 2.1 (dynamic client registration). OAuth-capable hosts open a browser
approval on first use; you choose the permissions and an optional daily
credit cap. No keys to copy.

**Claude Code**

```sh
claude mcp add --transport http --scope user nanostudio https://nanostudiopro.com/api/mcp
```

**claude.ai / Claude Desktop** — Settings → Connectors → Add custom
connector, paste `https://nanostudiopro.com/api/mcp` as the server URL.

**Cursor** — [Add to Cursor](cursor://anysphere.cursor-deeplink/mcp/install?name=nanostudio&config=eyJ1cmwiOiJodHRwczovL25hbm9zdHVkaW9wcm8uY29tL2FwaS9tY3AifQ==)
(one-click), or add `https://nanostudiopro.com/api/mcp` as a Streamable
HTTP server in MCP settings.

**Gemini CLI**

```sh
gemini extensions install https://github.com/spaceshiplabs1/nanostudio-mcp
```

**Any other MCP host** — connect to the URL above. Hosts without OAuth can
send a personal access token instead: create one at
[Settings → API Tokens](https://nanostudiopro.com/settings?tab=api-tokens)
and pass `Authorization: Bearer sk_sf_live_...`.

## Local stdio server

The `nsp` CLI bundles the same tools plus local-filesystem support
(save results to disk, upload local files):

```sh
curl -fsSL https://nanostudiopro.com/cli/nsp -o /usr/local/bin/nsp && chmod +x /usr/local/bin/nsp
claude mcp add --scope user nanostudio nsp mcp
```

Signed out? Fine — the first tool call starts a browser sign-in (device
flow) and hands the approval link to the agent. Approve, retry, done.

## What the tools do

31 tools. Highlights:

- `generate_image`, `restyle`, `expand_image`, `upscale_image` — create and
  transform product imagery (these cost credits; `get_pricing` tells you
  how much).
- `cutout` / `get_cutout` — background removal and layer extraction.
- `scan_image` / `get_detections` — free detection scans: what items,
  colors, and regions are in any image.
- `generate_video` / `get_video` — animate a product shot.
- `search` — detection-aware search across everything you have made or
  imported (text, color, similarity, browse). Search before regenerating.
- `import_image` / `upload_asset` — bring existing artwork in; every
  import is scanned and becomes searchable.
- Projects, assets, favorites, tasks, credits — the bookkeeping around it.

The full tool table with parameters lives at
[nanostudiopro.com/docs/mcp](https://nanostudiopro.com/docs/mcp).

## Support

- Docs: https://nanostudiopro.com/docs
- Contact: https://nanostudiopro.com/contact
