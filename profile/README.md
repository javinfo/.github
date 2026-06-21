# javinfo

**Metadata and magnet search for JAV releases.** Send a DVD ID, get back one clean JSON object — title, cast, maker, series, cover art, runtime, and (on paid plans) download / magnet links.

**[javinfo.eu.org](https://javinfo.eu.org)** · search the web app, or use the API below.

## API

One endpoint: `POST /search`. Query by code (`SSIS-001`, `CAWD-001`), optionally pin which providers to try.

```bash
curl -X POST 'https://javinfo-search.p.rapidapi.com/search' \
  -H 'Content-Type: application/json' \
  -H 'X-RapidAPI-Key: YOUR_RAPIDAPI_KEY' \
  -H 'X-RapidAPI-Host: javinfo-search.p.rapidapi.com' \
  -d '{ "q": "SSIS-001" }'
```

**[→ Get a key on RapidAPI](https://rapidapi.com/iamrony777/api/javinfo)**

## Providers

| Provider | Returns | Available on |
|---|---|---|
| `r18` | Bilingual metadata + actress images, covers, gallery | all tiers |
| `javdb` | Metadata plus download / magnet links | Pro / Max |
| `javlibrary`, `javdatabase`, `missav` | _coming soon_ | upcoming |

Results are cached server-side, so repeated lookups are fast. Requested providers outside your plan are ignored.
