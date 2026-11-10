# Select Naija Link Test (diagnostic addon)

A static Stremio-protocol addon that answers three questions on the real Fire TV before
Select Naija is built:

1. Do `externalUrl` streams open the right app or browser from Nuvio TV?
2. Do they survive AIOStreams (your "Select" config)?
3. Does a catalogue item with our own ID (`snaija-linktest`, no TMDB/IMDb entry) open and resolve streams?

## Host it (GitHub Pages, ~3 minutes)

1. Create a new public repo, e.g. `Ajnesss/select-naija-linktest` (separate from Select DE).
2. Upload every file in this folder, keeping the folders and the empty `.nojekyll` file.
3. Settings → Pages → Deploy from branch → `main` / root.
4. Manifest URL: `https://ajnesss.github.io/select-naija-linktest/manifest.json`

## Streams it returns

| Test | Type | Target | Pass if |
| --- | --- | --- | --- |
| T1 | `url` (direct MP4) | Big Buck Bunny sample | Plays in Nuvio's own player |
| T2 | `externalUrl` | Tubi UK title page | Tubi app or a browser opens that film |
| T3 | `externalUrl` | kava.tv | Browser or Kava app opens |
| T4 | `externalUrl` | netflix.com/browse | Netflix app opens (browser acceptable) |
| T5 | `externalUrl` | Plex title page | Plex app or browser opens |
| T6 | `externalUrl` | `tubitv://` app scheme | Diagnostic only: note what happens |

Streams are served for two IDs: `snaija-linktest` (custom catalogue row "Select Naija Link Test")
and `tt0118799` (a normal TMDB/IMDb film, *Life Is Beautiful*, to test the Xperience path).

## Test matrix (record in the Fire TV results table in the spec doc)

Run each of T1–T6 in these four paths:

- A. Nuvio TV on Fire TV, addon installed directly, opened from the "Select Naija Link Test" catalogue row
- B. Nuvio TV on Fire TV, addon installed directly, opened from *Life Is Beautiful* via Xperience
- C. Nuvio TV on Fire TV, addon added inside AIOStreams "Select" (custom addon), same title as B
- D. Stremio on Windows, addon installed directly (control: known-correct reference behaviour)

For each, note: shown in list (Y/N), what happened on click, and the Nuvio TV version
(Settings → About). Before testing, check whether a browser (Silk or another) is installed on the
Fire TV: if none, Nuvio TV falls back to its external-player route, which is itself a finding.
