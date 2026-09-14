# Nano Studio Pro — MCP server

Connect AI agents to [Nano Studio Pro](https://nanostudiopro.com), a personal
asset search engine. Every photo and video you make or upload is
detection-scanned, so an agent can find it again by the objects, colors,
textures and scenes inside it instead of hunting through folders. The same
server generates, restyles, cuts out, upscales and animates images, and builds
sprite, sticker and icon sheets with frame coordinates.

The server itself is hosted — there is nothing to build or run from this
repository. This repo carries the install manifests and pointers.

- Full documentation: https://nanostudiopro.com/docs/mcp
- Server card: https://nanostudiopro.com/.well-known/mcp/server-card.json
- Official registry entry: `com.nanostudiopro/studiopro` (0.9.0)
- Glama connector: https://glama.ai/mcp/connectors/com.nanostudiopro/studiopro

## Remote server (recommended)

Endpoint: `https://nanostudiopro.com/api/mcp` — Streamable HTTP with
OAuth 2.1 (dynamic client registration). OAuth-capable hosts open a browser
approval on first use; you choose the permissions and an optional daily
credit cap. No keys to copy.

**Claude Code**

```sh
claude mcp add --transport http --scope user nanostudio https://nanostudiopro.com/api/mcp
```

or install this repository as a plugin:

```sh
claude plugin install nanostudio --from-url https://github.com/spaceshiplabs1/nanostudio-mcp
```

**claude.ai / Claude Desktop** — Settings → Connectors → Add custom
connector, paste `https://nanostudiopro.com/api/mcp` as the server URL.

**Cursor** — [Add to Cursor](cursor://anysphere.cursor-deeplink/mcp/install?name=nanostudio&config=eyJ1cmwiOiJodHRwczovL25hbm9zdHVkaW9wcm8uY29tL2FwaS9tY3AifQ==)
(one-click), add `https://nanostudiopro.com/api/mcp` as a Streamable HTTP
server in MCP settings, or install this repository as a Cursor plugin (it
ships `.cursor-plugin/plugin.json` and `mcp.json`).

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

35 tools. 27 search, scan, organize and keep the books; 8 generate, edit,
cut out or animate.

- `search` — detection-aware search across everything you have made or
  imported: text, color, similar-image, browse, with item bounding boxes.
  Search before regenerating.
- `scan_image` / `get_detections` — free detection scans: what items,
  colors and regions are in any image.
- `import_image` / `upload_asset` — bring existing artwork in; every
  import is scanned and becomes searchable.
- `sheet_options` / `plan_sheet` / `generate_sheet` / `get_sheet_atlas` —
  sprite sheets, sticker packs, icon sets and animation cycles as one
  image, then the frame rectangles to cut them.
- `generate_image`, `restyle`, `expand_image`, `upscale_image` — create
  and transform imagery (these cost credits; `get_pricing` tells you how
  much).
- `cutout` / `get_cutout` — background removal and layer extraction.
- `generate_video` / `get_video` — image-to-video; quote with `dry_run`
  first.
- Projects, assets, favorites, tasks, credits, storage — the bookkeeping
  around it.

The full tool table with parameters lives at
[nanostudiopro.com/docs/mcp](https://nanostudiopro.com/docs/mcp).

## Manifests in this repo

| File | Host |
| --- | --- |
| `server.json` | Official MCP Registry |
| `gemini-extension.json` | Gemini CLI extension |
| `.cursor-plugin/plugin.json` + `mcp.json` | Cursor plugin |
| `.claude-plugin/plugin.json` + `.mcp.json` | Claude Code plugin |
| `glama.json` | Glama connector metadata |

## Support

- Docs: https://nanostudiopro.com/docs
- Contact: https://nanostudiopro.com/contact · support@nanostudiopro.com
