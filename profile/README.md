![javinfo](https://javinfo.dev/apple-touch-icon.png/?ref=github.com)

**JAV metadata search.** Send a DVD ID like `SSIS-001`, get back a JSON object: title, cast, maker, cover art, download links, HLS streams, the works.

**[javinfo.dev](https://javinfo.dev?ref=github.com)** · web app, or hit the API directly.

## API

Two endpoints at `https://api.javinfo.dev`:

| Endpoint | Returns |
|---|---|
| `POST /movie` | Single best match |
| `POST /query` | Ranked list of matches |

Pass a code and optionally pin which providers to try. Auth via `x-javinfo-key` header. No charge on non-200 responses.

```bash
curl -X POST 'https://api.javinfo.dev/movie' \
  -H 'Content-Type: application/json' \
  -H 'x-javinfo-key: YOUR_KEY' \
  -d '{ "q": "SSIS-001" }'
```

```js
const res = await fetch("https://api.javinfo.dev/movie", {
  method: "POST",
  headers: {
    "Content-Type": "application/json",
    "x-javinfo-key": "YOUR_KEY",
  },
  body: JSON.stringify({ q: "SSIS-001", providers: "javdb" }),
});
const data = await res.json();
```

```python
import requests

res = requests.post(
    "https://api.javinfo.dev/movie",
    headers={"x-javinfo-key": "YOUR_KEY"},
    json={"q": "CAWD-001", "providers": "javdb"},
)
data = res.json()
```

**[→ Get a free key](https://app.javinfo.dev?ref=github.com)**

## MCP

Model Context Protocol server (stdio) for AI agents. Look up releases by code, title, or actress; fetch metadata, download links, or stream URLs; open a local LAN HLS play session via the CLI.

Install from [npm](https://www.npmjs.com/package/@javinfo/mcp):

```json
{
  "mcpServers": {
    "javinfo": {
      "command": "npx",
      "args": ["-y", "@javinfo/mcp"],
      "env": { "JAVINFO_API_KEY": "YOUR_KEY" }
    }
  }
}
```

Tools: `javinfo-search`, `javinfo-movie`, `javinfo-random`, `javinfo-open`, `javinfo-serve`.

## CLI

Production-oriented [Rust CLI](https://github.com/javinfo/cli) — API client plus local tools. Install:

```bash
curl -fsSL https://javinfo.dev/install.sh | bash
```

```bash
javinfo login                                   # save your API key
javinfo movie SSIS-001 --json                   # code lookup
javinfo nfo ~/Videos/JAV --write                # Kodi/Jellyfin NFO + artwork
javinfo open EBOD-391 --with vlc                # LAN HLS play session
```

Commands: `movie`, `nfo`, `login`, `status`, `serve` / `open`.

## Providers

| Provider | Returns |
|---|---|
| `fanza` | Richest structured metadata: bilingual title, cast, maker, label, series, covers, trailer, gallery |
| `dmm` | Richest structured metadata: bilingual title, cast, maker, label, series, covers, trailer, gallery |
| `javdb` | Metadata plus magnet / PikPak download links and community score |
| `missav` | Metadata plus HLS stream URLs (`.m3u8`) |
| `javdatabase` | Metadata plus description, sample images, and a trailer URL |
| `javlibrary` | Catalog data: title, cast, genres, runtime, release date, studio, cover, and sample images |

All providers work on every request. No tier gating. Results cache server-side, so repeated lookups are fast.

**Join other hundreds of developers building on [javinfo.dev](https://javinfo.dev?ref=github.com) now.**
