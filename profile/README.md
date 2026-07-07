![javinfo](https://javinfo.dev/apple-touch-icon.png/?ref=github.com)

**JAV metadata search.** Send a DVD ID like `SSIS-001`, get back a JSON object: title, cast, maker, cover art, download links, HLS streams, the works.

**[javinfo.dev](https://javinfo.dev)** · web app, or hit the API directly.

> **Product launch promo: top-ups of $50+ get a 5–50% bonus. Sign up today!**

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

**[→ Get a free key](https://app.javinfo.dev)**

## Providers

| Provider | Returns |
|---|---|
| `r18` | Bilingual metadata: title, cast, maker, label, series, covers, trailer, gallery |
| `javdb` | Metadata plus magnet / PikPak download links and community score |
| `missav` | Metadata plus HLS stream URLs (`.m3u8`) |
| `javdatabase` | Metadata plus description, sample images, and a trailer URL |
| `javlibrary` | _coming soon_ |

All providers work on every request. No tier gating. Results cache server-side, so repeated lookups are fast.
