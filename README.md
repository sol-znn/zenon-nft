![Header image from the Zenon Network article "The New NFT Standard"](assets/article-header.png)

# zenon-nft

A one-page explainer and live demo of **threshold release**, the way the
unlockable content of the Zenon NFT standard would open: the content key is
sealed once to a committee of Sentinels, and whoever the ledger says holds the
item can open it. A transfer is a plain send.

**Live page:** https://nft.zenon.foo/

The standard comes from the Zenon Network article
[The New NFT Standard: when cryptography meets steganography](https://medium.com/@zenon.network/the-new-nft-standard-when-cryptography-meets-steganography-9e356007dcaa)
(Medium, 2022-05-01). It asks for a Virtual Hologram embedded in the media and
for content that only the holder can reveal. This page covers the second part,
and lets you try the first on your own file.

## What the page does

| Section | What it is |
|---|---|
| How an item opens | A 13-step sequence: mint, seal, open, transfer, a refused request, the next holder opening the same file |
| Try it with a file | Drop any file, or pick a sample. The proof of concept's Go code, compiled to WebAssembly, wraps it in your browser: placement chosen from the bytes, a byte-layout map and a hex view of exactly what was inserted, a before-and-after preview, the hologram, the pointer-only record, and downloads of the results |
| Ask the committee | A 3-of-5 committee and a ledger live in the module. Open as the holder, a stranger or the previous holder; take Sentinels offline or make them collude; send the item; reshare to 4-of-7 and open the untouched file again |
| What Zenon needs | The contract, node and client changes, each marked spork or release |
| What it costs | Collusion, liveness, privacy, and why not proxy re-encryption |
| Sources | 19 numbered citations |

**Nothing you load leaves your browser.** The site is static files on GitHub
Pages; there is no server-side code and nothing is stored. The file you drop is
read into memory, wrapped by the WebAssembly module, shown, and offered back as
a download. Reloading the page discards it.

It is a design explainer. Nothing on the page talks to a Zenon network.

## Run it locally

The demo loads a WebAssembly module, which browsers refuse from `file://`, so
serve the folder:

```console
python -m http.server 8137
```

Then open http://localhost:8137.

## Build

The page, the module and the samples are generated from the research project
this site belongs to (`zenon-nft/web/build.py`, `zenon-nft/poc/`). Edit there
and rebuild; this repository holds only the output.

## Files

| Path | What it is |
|---|---|
| `index.html` | The whole page: markup, styles, script and the two fonts inlined |
| `znft.wasm` | The proof-of-concept library (Go, `filippo.io/edwards25519`) compiled for the browser |
| `wasm_exec.js` | Go's WebAssembly loader, copied from the Go distribution |
| `samples/` | 17 small files of 17 types for the demo |
| `assets/article-header.png` | The article's header image, from the Medium post above |
| `assets/licenses/` | SIL Open Font License 1.1 for Space Grotesk and JetBrains Mono (embedded in `index.html`), and the Go licence for `wasm_exec.js` |

## Publish on GitHub Pages

Pages serves the `main` branch from the root folder. The `.nojekyll` file tells
Pages to serve the files as they are.
