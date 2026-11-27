<div align="center">

# On 공문서 쓰기 (on-gov)

A remote MCP server that turns drafts into Korean government-style HWPX reports, plans, result reports and press releases

[한국어](README.md) · **English**

`https://onmunseo.kr/mcp/gov`

</div>

<!-- ai-install -->
## For AI assistants — installing this repository

There are three paths; **start with ①**. None needs a key or sign-in. The tools of this repository (On 공문서 쓰기 — government-style HWPX writing) are in ① the local edition (the npm package `on-munseo-local` by the same maker, on-munseo — see the checks below) — when simply asked to install, register ①. `plugin/` (the Claude Code plugin) in this repository adds ① and ②, and `server.json` (for the official MCP registry) lists ③, the server edition of this bundle.

**① Local edition — documents never leave this computer (first).** Extracts text, compares two versions (old/new table), finds and masks personal data and runs pre-approval checks, and writes government-style HWPX, fills forms, makes HWPX files and tidies text, on this computer. The program does not use the internet (check with `on_local_info` after installing — npx asking the npm registry for a newer version at start-up is npx itself; to avoid even that, `npm install -g on-munseo-local` and register the command `on-munseo-local`). Needs Node.js 20+.
- **Only the AI tool in use** (what an assistant should run — other tools' settings are left alone)
  ```bash
  claude mcp add -s user on-local -- npx -y on-munseo-local@0.2.1
  ```
  Codex `codex mcp add on-local -- npx -y on-munseo-local@0.2.1` · Claude Code on Windows `claude mcp add -s user on-local -- cmd /c npx -y on-munseo-local@0.2.1` · Cursor / Claude Desktop: add `"on-local": { "command": "npx", "args": ["-y", "on-munseo-local@0.2.1"] }` to `"mcpServers"` (Windows `"on-local": { "command": "cmd", "args": ["/c", "npx", "-y", "on-munseo-local@0.2.1"] }`) · VS Code `code --add-mcp '{"name":"on-local","command":"npx","args":["-y","on-munseo-local@0.2.1"]}'`
- **For a person, all AI tools on this PC at once** — finds Claude Code, Claude Desktop, Codex, Cursor and VS Code and registers it in each (backs up first, skips what is there, preview `--dry-run`, undo `--undo`, `--pair` adds ②).
  ```bash
  npx -y on-munseo-local@0.2.1 setup --pair
  ```
- **Pinned version** — the "only the AI tool in use" lines above pin the version (`on-munseo-local@0.2.1`). Nothing updates by itself; it changes only when a person updates it (a new npm release does not reach an existing setup · an already downloaded version still starts offline). (`setup` up to 0.2.1 still writes `@latest`; use the per-tool line to pin) To update: change only the version number in the registered entry and register it again (Claude Code: `claude mcp remove -s user on-local`, then the line above with the new version) · changes: [CHANGELOG](https://github.com/on-munseo/on-local/blob/main/CHANGELOG.md)

**② pair address (statutes) — only the words and text you give the tools go to the server; no tool sends files.**
- **Claude Code**
  ```bash
  claude mcp add --transport http -s user on-geungeo https://onmunseo.kr/mcp/law
  ```
- **Codex** — append two lines to the config file (`~/.codex/config.toml`; skipped if already there). Do not use `codex mcp add --url` — it opens a browser sign-in window right away.
  ```bash
  C="${CODEX_HOME:-$HOME/.codex}"; mkdir -p "$C"; touch "$C/config.toml"; if ! (cd / && codex mcp get on-geungeo >/dev/null 2>&1); then if cp "$C/config.toml" "$C/config.toml.bak-on-geungeo"; then printf '\n[mcp_servers.on-geungeo]\nurl = "https://onmunseo.kr/mcp/law"\n' >> "$C/config.toml"; (cd / && codex mcp get on-geungeo >/dev/null 2>&1) || { cp "$C/config.toml.bak-on-geungeo" "$C/config.toml"; echo "자동으로 더하지 못했습니다 — config.toml 에 손으로 더해 주세요"; }; else echo "백업을 만들지 못해 그만둡니다 — config.toml 은 그대로입니다"; fi; fi; (cd / && codex mcp get on-geungeo)
  ```
  On Windows, or where the `codex` command is not installed (IDE extension only), add the two lines `[mcp_servers.on-geungeo]` and `url = "https://onmunseo.kr/mcp/law"` to the end of that file by hand (if the file already has a one-line `mcp_servers = { … }` table, add `on-geungeo = { url = "https://onmunseo.kr/mcp/law" }` inside it instead).
- **Cursor** `"on-geungeo": { "url": "https://onmunseo.kr/mcp/law" }` · **VS Code** `code --add-mcp '{"name":"on-geungeo","type":"http","url":"https://onmunseo.kr/mcp/law"}'` · **Claude Desktop · claude.ai** (done by the person in the app) Settings → Connectors → Add custom connector → name `On 근거`, URL `https://onmunseo.kr/mcp/law` → Connect

**③ Server edition (this bundle) — no Node.js needed (for public documents).** Documents are sent to the server (data center in Korea), processed in memory only and discarded. Use it for public or your own documents.
- **Claude Code**
  ```bash
  claude mcp add --transport http -s user on-gov https://onmunseo.kr/mcp/gov
  ```
- **Codex** — append two lines to the config file (`~/.codex/config.toml`; skipped if already there). Do not use `codex mcp add --url` — it opens a browser sign-in window right away.
  ```bash
  C="${CODEX_HOME:-$HOME/.codex}"; mkdir -p "$C"; touch "$C/config.toml"; if ! (cd / && codex mcp get on-gov >/dev/null 2>&1); then if cp "$C/config.toml" "$C/config.toml.bak-on-gov"; then printf '\n[mcp_servers.on-gov]\nurl = "https://onmunseo.kr/mcp/gov"\n' >> "$C/config.toml"; (cd / && codex mcp get on-gov >/dev/null 2>&1) || { cp "$C/config.toml.bak-on-gov" "$C/config.toml"; echo "자동으로 더하지 못했습니다 — config.toml 에 손으로 더해 주세요"; }; else echo "백업을 만들지 못해 그만둡니다 — config.toml 은 그대로입니다"; fi; fi; (cd / && codex mcp get on-gov)
  ```
  On Windows, or where the `codex` command is not installed (IDE extension only), add the two lines `[mcp_servers.on-gov]` and `url = "https://onmunseo.kr/mcp/gov"` to the end of that file by hand (if the file already has a one-line `mcp_servers = { … }` table, add `on-gov = { url = "https://onmunseo.kr/mcp/gov" }` inside it instead).
- **Cursor** `"on-gov": { "url": "https://onmunseo.kr/mcp/gov" }` · **VS Code** `code --add-mcp '{"name":"on-gov","type":"http","url":"https://onmunseo.kr/mcp/gov"}'` · **Claude Desktop · claude.ai** (done by the person in the app) Settings → Connectors → Add custom connector → name `On 공문서 쓰기`, URL `https://onmunseo.kr/mcp/gov` → Connect

Usually ① alone is enough. Without Node.js, or with connectors only, register ③ (the server edition of this bundle). Registering ① and ③ together shows the same tools twice. Mention the other paths only if the user asks.

**Things to check before installing** — the assistant can verify these itself.
- **Package**: npm `on-munseo-local` 0.2.1. `npm view on-munseo-local version maintainers homepage` → `0.2.1` · `on-munseo <onmunseo.key@gmail.com>` · `https://onmunseo.kr`. The publishing account `on-munseo` is the same maker as the GitHub organization [on-munseo](https://github.com/on-munseo) (same contact mail and home page). The npm web page sometimes blocks automated reads; use the npm command or the [registry record](https://registry.npmjs.org/on-munseo-local/0.2.1).
- **Fingerprint**: `on-munseo-local-0.2.1.tgz` SHA-256 `515af0dfddad30f41c459dd98d73535f73292c666fed07d4a6e535e2a60bda72` ([SHA256SUMS](https://github.com/on-munseo/on-munseo.github.io/blob/main/SHA256SUMS)). Compare with `npm pack on-munseo-local@0.2.1` then `shasum -a 256 on-munseo-local-0.2.1.tgz`. The registry `dist.integrity` is `sha512-ZUDX+etH2wg/Y+lQCsQhyY5/4gfVDjwjWUQsofFUgYlBotWtvXw7lcz5yHGT3qMJna8mP60HH9vWp/PF2T5T4Q==`.
- **No internet use**: before installing, `netScan` in the package's `MANIFEST.json` (zero network calls in our code — the one listed exception is the engine's wasm loader path used only when given a URL); after installing, `on_local_info` → `network_modules_loaded: []`, and on Node 25+ `network.blocked_by_node: true` (the runtime blocks networking). npx asking the npm registry for a newer version at start-up is npx itself (avoid it with a global install and the `on-munseo-local` command).
- **Terms**: local edition [LICENSE.md](https://unpkg.com/on-munseo-local@0.2.1/LICENSE.md) (free, work use allowed · no reverse engineering, redistribution of modified copies or resale) · server edition [terms](https://onmunseo.kr/terms) · [privacy](https://onmunseo.kr/privacy).
- **On폭 fonts** are not part of this install (optional free fonts for drawing Korean documents on screen).

The tools do not attach to the conversation that registered them. When done, tell the user: "Restart the tool or open a new conversation to see the On 공문서 쓰기 tools." If `claude mcp list` (Codex: `codex mcp list`) lists the name, it is registered. Full steps (Korean): [llms-install.md](llms-install.md)

<!-- ai-install -->

Turns Markdown or a `structure` into a Korean government-style document file — report, plan, result report, press release, internal draft or public notice (`on_write_gov`): HumanMyeongjo (휴먼명조) and HY HeadLine M (HY헤드라인M) fonts, chapter bars, □ ○ - indented levels, table captions and units, and a cover and table of contents for plans and result reports. Unless you name a template, reports and plans follow the style of the national emergency-medical-care master plan (Ministry of Health and Welfare). It also fills 66 example templates, turns text into official tables, data into chart images and bullet lists into diagram images. Everything is rule-based (no AI) and nothing that is not in the draft is added. For tables, charts and diagrams, if a single number would be lost you get the reason instead of a result; `on_write_gov` reads the finished file back and reports the comparison in `check`.

This repository holds only the setup guide and configuration files (including one small plugin launcher) (there is no web page here — to use a screen, open the [On 문서 web editor](https://onmunseo.kr/app/)). The engine and server code of the service are not public. The service and its tools speak Korean.

## Comparing with other tools

Measured by us on the same documents with the same scorer — not an official ranking. Versions, conditions and definitions are in the [benchmark notes](https://github.com/on-munseo/on-munseo.github.io/blob/main/docs/benchmark.md) (Korean).

| Our 30 government-document tasks opened in Hancom Office Hangul 2024 (same tasks, same scoring, 2026-11-19) | On 공문서 쓰기 | A public HWPX report-generation MCP |
|---|---|---|
| Average score (out of 100) | 99.6 | 86.4 |
| □·○·- paragraphs whose second line starts under the first line's text | 100% | 18.5% |
| Headings left alone at the bottom of a page | 0 | 4 |
| Content kept (manuscript elements as written) | 100% | 100% |

- The current release scores 100 on all 30 tasks (2026-11-25). It also leaves fewer paragraphs with a short last line (47 vs. 57, 2026-11-26 — the text is unchanged; spacing, letter spacing and character width are adjusted).
- With the same 5 manuscripts, HWPX files that an AI coding tool built by writing its own code (no MCP) averaged 57.1 (3 of them showed no body text in Hancom, as made on the first try); On 공문서 쓰기 scored 100 (2026-11-26). Five is a small sample.
- Charts, diagrams, cover and table of contents come from the same tool; the result can then be checked before approval and its statute citations verified (On 근거). Tables, charts, diagrams and form filling return the reason instead of a result if a single source number would be lost, and `on_write_gov` returns a `check` made by re-reading the file it wrote.
- **Where documents go:** documents sent to this address are processed only in memory on the On 문서 server (a data centre in Korea) and discarded afterwards; they are not sent to any outside AI company. Send only public documents or your own to this server-side address; handle internal documents of your organisation with the browser-only features of the [web editor](https://onmunseo.kr/app/) (open, edit and save HWP/HWPX, the pre-approval check, masking personal data) — attachment text extraction, OCR and HWPX creation in the web editor still go through the server.

**Jump to:** [Comparing](#comparing-with-other-tools) · [Why](#in-short--why-use-it) · [Tools](#what-it-does) · [Connect](#connect) · [Examples](#examples) · [Measured results](#measured-results) · [Guest and key](#guest-and-key) · [Safety](#safety) · [Good to know](#good-to-know)

## In short — why use it

| Common pain | With On 공문서 쓰기 |
|---|---|
| An HWP file made by an AI chat opens as a blank page in Hancom | From the same 5 drafts, 3 files made by an AI chat alone showed no text at all in Hancom; files made with this tool: 0 (see results) |
| You align □ ○ - levels, chapter bars, the cover and the contents by hand | The engine does the layout — second lines align with the first line’s text, and no heading is left alone at the bottom of a page |
| You make tables, charts and diagrams separately and paste them in | `on_table`, `on_chart` and `on_diagram` draw only from the numbers and words given, and return a reason instead of an image if anything does not match |
| You are not sure what layout to use | Pick one of 66 example templates (plans, reports, events, notices, press releases) and fill it with your material (`on_list_templates`, `on_fill_template`) |

**When you do not need it:** If your organisation gives you a form file, fill that form instead (`on_fill` in [On HWPX 만들기](https://github.com/on-munseo/on-hwpx)). A plain one-page memo only needs `on_write`.

## What it does

| Tool | What it does | Guest |
|---|---|---|
| `on_write_gov` | Markdown or a structure to a government-style HWPX (report, plan, result report, press release, draft, notice). The result lists fixes (`quality`), short second lines (`short_last_lines`), the read-back comparison (`check`) and a page preview (`preview`) | yes |
| `on_list_templates` | The 66 example templates (plans, reports, events, notices, press releases): number, group, name, pages | yes |
| `on_fill_template` | Places the paragraphs and tables of your material into the matching chapters of one template; blocks with no clear place are not inserted but listed in `unplaced` | yes |
| `on_table` | Turns “item: value” lines, tabs, commas or pipes into an official table, checks every number and the totals; Markdown table plus HWPX | yes |
| `on_chart` | Draws bar, line, pie or horizontal-bar charts (PNG) from table data and checks numbers and bar lengths | yes |
| `on_diagram` | Draws step flows, organisation charts and structure diagrams (PNG) from □ ○ - bullets or “A → B → C”, keeping the original words in the boxes | yes |

- The 6 guest tools were checked on 2026-11-26 by calling `tools/list` on the live server as a guest.
- Limits: `on_table` 20,000 characters, 200 rows, 20 columns · `on_chart` 20,000 characters · `on_diagram` 4,000 characters, 8 main items with up to 8 sub-items · `on_fill_template` 300,000 characters of material and 4 files (25 MB each). Download links last 15 minutes.

## Connect

Of the three paths at the top ([For AI assistants](#for-ai-assistants--installing-this-repository): ① local edition · ② pair address · ③ server edition), this section details ③, the server edition of this bundle, for each tool.

**Claude Code** — one line in the terminal (`-s user` makes it available in every folder):

```bash
claude mcp add --transport http -s user on-gov https://onmunseo.kr/mcp/gov
```

**Claude Code plugin** — adds ① the local edition + ② the statute pair (Node.js 20+; works on Windows too — the small launcher `plugin/run-local.mjs` starts npx). Installing several of these product plugins starts the local edition several times and shows the same tools more than once, so install just one. One line (Claude Code 2.1.275 or later):

```bash
claude plugin install on-gov --marketplace on-munseo/on-gov
```

In every app, the conversation in which you register the server does not get the tools yet. Restart the app once (Claude Code: `/exit`, then `claude`; VS Code: a new chat) or open a new conversation, and the tools are there from then on. Without a key, skip the sign-in step and use it as a guest.

> To use all document tools and the law tools (On 근거) together, add `https://onmunseo.kr/mcp` instead of this bundle (recommended — [On 문서](https://github.com/on-munseo/on-munseo.github.io)). If you add both, the same tools appear twice.

### Claude Code — more

- With a key: in Claude Code open `/mcp` → `on-gov` → Authenticate, and the On 문서 sign-in page opens. Enter your key there.
- To pass the key as a header: `claude mcp add --transport http -s user on-gov https://onmunseo.kr/mcp/gov --header "Authorization: Bearer <key>"`. This stores the key in `~/.claude.json`, so the sign-in page is the better way.
- Two-step plugin install (older versions): `claude plugin marketplace add on-munseo/on-gov`, then `claude plugin install on-gov@on-gov`. In a Claude Code chat: `/plugin marketplace add on-munseo/on-gov` → `/plugin install on-gov@on-gov`.
- Check: `claude mcp list` · remove: `claude mcp remove on-gov`.

### claude.ai · Claude Desktop (connectors)

Settings → Connectors → “Add custom connector”: name `On 공문서 쓰기`, URL `https://onmunseo.kr/mcp/gov`, then Connect. With a key, enter it on the On 문서 sign-in page that opens; without one you are a guest. Menu names differ by plan and version, and some plans may not have this menu.

To add it to Claude Desktop through the config file, use the `mcp-remote` bridge (needs Node.js). macOS `~/Library/Application Support/Claude/claude_desktop_config.json` · Windows `%APPDATA%\Claude\claude_desktop_config.json`:

```json
{
  "mcpServers": {
    "on-gov": {
      "command": "npx",
      "args": [
        "-y",
        "mcp-remote",
        "https://onmunseo.kr/mcp/gov"
      ]
    }
  }
}
```

To send a key as a header, append `"--header", "Authorization:${ON_AUTH}"` to `"args"` and add `"env": { "ON_AUTH": "Bearer <key>" }` (no space after the colon, so Windows does not split the argument). Restart Claude Desktop after saving.

### ChatGPT

1. Settings → Apps & Connectors → Advanced settings: turn on Developer mode (wording may differ by version).
2. Create a custom MCP server: name `On 공문서 쓰기`, URL `https://onmunseo.kr/mcp/gov`, authentication “OAuth” if you have a key, otherwise “None”.
3. Enter your key on the On 문서 sign-in page, then turn the connector on from the tools (+) menu of a chat.

- ChatGPT receives a separate pass instead of your key (same permissions and daily quota). Revoking the key blocks the pass at once.

### Codex

Without a key, add two lines to `~/.codex/config.toml`:

```toml
[mcp_servers.on-gov]
url = "https://onmunseo.kr/mcp/gov"
```

- `codex mcp add` opens the On 문서 sign-in window right away. With a key, enter it there; without one, close it (Ctrl-C) and use the two lines above.

### Cursor

`~/.cursor/mcp.json` (all projects) or `.cursor/mcp.json` in a project:

```json
{
  "mcpServers": {
    "on-gov": {
      "url": "https://onmunseo.kr/mcp/gov"
    }
  }
}
```

If your Cursor version cannot sign in to remote MCP servers (OAuth), add `"headers": { "Authorization": "Bearer <key>" }` (the key is then stored in the file).

### VS Code

`.vscode/mcp.json` in the workspace:

```json
{
  "servers": {
    "on-gov": {
      "type": "http",
      "url": "https://onmunseo.kr/mcp/gov"
    }
  }
}
```

To send a key as a header without writing it in the file, let VS Code ask for it on first start:

```json
{
  "inputs": [
    {
      "type": "promptString",
      "id": "on-key",
      "description": "On 문서 key",
      "password": true
    }
  ],
  "servers": {
    "on-gov": {
      "type": "http",
      "url": "https://onmunseo.kr/mcp/gov",
      "headers": {
        "Authorization": "Bearer ${input:on-key}"
      }
    }
  }
}
```

### Try it with curl

List the tools (add `-H "Authorization: Bearer <key>"` if you have a key):

```bash
curl -s https://onmunseo.kr/mcp/gov \
  -H "Content-Type: application/json" -H "Accept: application/json, text/event-stream" \
  -d '{"jsonrpc":"2.0","id":1,"method":"tools/list"}'
```

Call `on_write_gov` — sending the request from a file keeps quotes and line breaks intact:

```bash
cat > call.json <<'EOF'
{"jsonrpc": "2.0", "id": 1, "method": "tools/call", "params": {"name": "on_write_gov", "arguments": {"style": "결과보고서", "markdown": "# ○○ 회의 결과보고\n\n## Ⅰ. 회의 개요\n\n○ 일시: 2026. 11. 20.(금) 14:00\n○ 장소: ○○ 회의실\n\n## Ⅱ. 주요 내용\n\n○ 교육 과정 8회 운영, 수료 214명\n"}}}
EOF
curl -s https://onmunseo.kr/mcp/gov \
  -H "Content-Type: application/json" -H "Accept: application/json, text/event-stream" \
  --data-binary @call.json
```

The reply had a 3-page result report, `check.same: true`, a 15-minute link in `file.url`, and messages for the user in `tell_user` (2026-11-26, guest). The answer is the text in `result.content`. The server is stateless (Streamable HTTP, POST), so a single `tools/call` works without `initialize`. Opening the URL in a browser shows a short guide page.

## Examples

| If you say | This tool |
|---|---|
| “Make a result report HWP file from this material” | `on_write_gov` |
| “Which press-release templates are there?” | `on_list_templates` |
| “Fill this into an event-plan template” | `on_fill_template` |
| “Turn the yearly numbers below into an official table” | `on_table` |
| “Draw a bar chart from this table” | `on_chart` |
| “Draw the implementation structure as a diagram” | `on_diagram` |

The AI decides which tool to call; these are typical cases.

## Measured results

| What | Test set | Result | Build · date · machine |
|---|---|---|---|
| Opened in Hancom Office Hangul 2024 | 30 self-made official-document tasks (12 reports · 6 plans · 6 result reports · 6 press releases; agencies and numbers are made up) | all 30 opened · all 30 scored 100 (layout 40 · line and page drift 20 · content kept 40) · second-line alignment 153/153 · paragraphs with only 1–2 characters on the last line 0/153 | On 한글엔진 2.2.1 and 공문서 쓰기 as deployed at the time · Hangul 2024 (9.1.1) · Windows i7-14700 · 2026-11-25 |
| This tool vs AI chat alone | The same 5 drafts made both ways and opened in Hangul 2024 | draft elements (titles, paragraphs, table cells) shown as written 169/169 (100%) vs 60/169 (35.5%) · documents showing no text at all 0/5 vs 3/5 · score with the same rubric 100 vs 57.1 | 2026-11-26 (the AI-chat files are the ones made on 2026-11-22) |

<sub>All values were measured by us, with engine 2.2.1; since 2026-11-26 the live engine is 2.2.3 (not re-measured yet). The 30 tasks are our own. Five drafts is a small sample, and “AI chat alone” means a general AI coding tool without MCP, asked once with the same request, result kept as is (no picking, no retries). That result can vary with the AI and the moment, and may improve if a person checks it in Hancom and asks again. The rubric is in the [measurement notes](https://github.com/on-munseo/on-munseo.github.io/blob/main/docs/benchmark.md#4-만들기--한컴-한글-2024-로-연-공문서-30과제) (Korean).</sub>

Weak spots: many paragraphs end with a short last line — in 89 of the 153 multi-line □·○·- paragraphs of the 30 tasks the last line is under a third of the line width (none with only 1–2 characters). Reducing it further needs rewording.

## Guest and key

|  | Guest (no key) | Key |
|---|---|---|
| How to connect | Add the URL with no authentication | Enter the key on the On 문서 sign-in page (OAuth), or send `Authorization: Bearer <key>` |
| Tools at this endpoint | 6 | 6 |
| Daily quota | 50 calls a day and 6 a minute (the statute tools `law_`·`med_` have their own 100 a day and 20 a minute) per internet address (IP), counted across all On 문서 endpoints and the web editor. When the shared guest quota for the day runs out, guest access closes until midnight Korea time | A daily quota and concurrency limit set per key |
| Size | 6 MB per request (base64 included) | 25 MB per file |
| Needs a key | — | none (the key must include this bundle — first-issued keys do not) |

- To use it with a key, the key must include this bundle. First-issued keys do not, so mention it when you apply. Guests can use it right away.
- To get a key, write to `onmunseo.key [at] gmail.com` (subject “On 문서 열쇠 신청”), with what you will use it for and which bundle you need (e.g. On 공문서 쓰기).
- A wrong or revoked key gives **401**; a bundle that is not in your key gives **403**. Too many calls in a short time give “too many requests” (429) — wait about a minute.
- Never append the key to the URL; it would end up in chat and access logs.

## Safety

1. **Nothing is kept.** Documents and text you send are handled in server memory only and discarded when done. No document files are stored; the access log holds only the key alias, tool name, request size, time taken and success (no contents, no file names).
2. **Rule-based, no AI.** No facts or numbers beyond the draft are added; charts and diagrams use only the numbers and words given.
3. **Lost numbers are reported.** Tables, charts and diagrams (`on_table`, `on_chart`, `on_diagram`) return the reason instead of a result if any number would be lost; `on_write_gov` reads the file back and returns `check` (`check.same: false` means something was lost — see `check.examples`).
4. **Send only public material or your own to this server-side address.** Handle internal documents of your organisation with the browser-only features of the [web editor](https://onmunseo.kr/app/) (open, edit and save HWP/HWPX, the pre-approval check, masking personal data).
5. **Safety limits stay on.** Size limits against attacks such as zip bombs, and refusal of distribution-only documents, are never lifted for convenience.
6. **Result files last 15 minutes.** Files are returned as links that work for 15 minutes.

Report security problems as described in [SECURITY.md](SECURITY.md).

## Good to know

- **This is a free trial service.** Features, quotas and URLs may change or stop. Changes are noted in [CHANGELOG.md](CHANGELOG.md).
- **Results are for reference.** Have a person check them before approval.
- Output is HWPX only (for .hwp, open the HWPX in Hancom Hangul and use “Save As”).
- Internet only — it cannot be used from closed government networks.
- Menus differ by app and version, so screens may not match the steps above. If something fails, see [SUPPORT.md](SUPPORT.md).

## Terms, privacy and notices

- Bulk collection of results and use of results to train other AI models are not allowed. Automated abuse (several keys to get around limits, non-stop calls, scraping results) leads to the key being cut off without notice. Extracting or reverse-engineering the engine, rules or code is not permitted.
- Summary: [terms in the MCP guide](https://github.com/on-munseo/on-munseo.github.io/blob/main/MCP.md#5-이용-조건약관-요약) (Korean). Full text: [terms of use](https://onmunseo.kr/terms) and [privacy policy](https://onmunseo.kr/privacy) (Korean).
- “Hangul”, “Hancom”, “HWP” and “HWPX” are trademarks or registered trademarks of Hancom Inc. On 문서 is an independent service with no affiliation, sponsorship or endorsement by Hancom Inc.
- Claude, ChatGPT, Cursor, VS Code and other names belong to their owners and are used only to explain how to connect. Full notices: [notices in the MCP guide](https://github.com/on-munseo/on-munseo.github.io/blob/main/MCP.md#고지) (Korean).

## Glossary

- **MCP** — Model Context Protocol, an open standard for AI tools to call outside tools. Add this URL as an MCP server and the AI calls these tools inside the chat.
- **Remote MCP server** — An MCP server reached over the internet; nothing to install on your computer.
- **Bundle endpoint** — A URL that carries one On 문서 feature set (`/mcp/text` and so on). Everything is at `/mcp`.
- **Key (열쇠)** — The access value issued by On 문서, with a daily quota and a set of bundles. Keep it secret.
- **Guest (손님)** — Use without a key: some tools and a small daily quota, right away.
- **OAuth (sign-in page)** — You enter the key on the On 문서 sign-in page when connecting; the app receives a separate pass instead of the key.
- **HWPX** — The XML format of Korean Hangul documents (KS X 6101 OWPML); .hwp is the older format.
- **base64** — A way of writing a file as text, used to put a file inside JSON.
- **Gaejo (개조식)** — The bullet style of Korean official documents: □ ○ - marks and short “~함/~임” endings, one idea per line.
- **structure** — A draft given as fields (chapters, sections, items) instead of Markdown.

## Other On 문서 bundles

| Product | Repository | Endpoint (after `https://onmunseo.kr`) |
|---|---|---|
| **On 문서 (all)** | [on-munseo.github.io](https://github.com/on-munseo/on-munseo.github.io) — web editor and every MCP tool | `/mcp` |
| On 글꺼내기 | [on-text](https://github.com/on-munseo/on-text) | `/mcp/text` |
| On 결재점검 | [on-check](https://github.com/on-munseo/on-check) | `/mcp/check` |
| On 개인정보 가리기 | [on-mask](https://github.com/on-munseo/on-mask) | `/mcp/mask` |
| On HWPX 만들기 | [on-hwpx](https://github.com/on-munseo/on-hwpx) | `/mcp/hwpx` |
| On 공문서 쓰기 | this repository | `/mcp/gov` |
| On 글 다듬기 | [on-tidy](https://github.com/on-munseo/on-tidy) | `/mcp/tidy` |
| On 근거 | [on-geungeo](https://github.com/on-munseo/on-geungeo) | `/mcp/law` |
| On폭 글꼴 (fonts) | [napurrin/onpok-fonts](https://github.com/napurrin/onpok-fonts) — free fonts (SIL OFL 1.1) · not needed for the MCP install (optional) | — |

## License

Text is [CC BY 4.0](https://creativecommons.org/licenses/by/4.0/); configuration files (`server.json`, `.claude-plugin/`, `plugin/`) are MIT. The names “On 문서” and “On 공문서 쓰기” and the logo are not covered by these licenses. The engine and server code of the service are not in this repository and are not public. See [LICENSE](LICENSE).

---

Made by [napurrin](https://github.com/napurrin), who builds and maintains it while learning from Coco.
