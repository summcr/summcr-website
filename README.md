# summcr-website

The source of <https://summcr.com> — the homepage for
[summ](https://github.com/summcr/summ), an OCI container registry.

Four files and no build step, for the same reason the registry's own UI has
none: `index.html`, `style.css`, `logo.svg`, and whatever lands in `assets/`.
Open `index.html` in a browser, or serve the directory:

```sh
python3 -m http.server 8000
```

## Layout

| Path | What it is |
|---|---|
| `index.html` | The whole page |
| `style.css` | The whole visual system. The palette is summ's own UI palette |
| `logo.svg` | A copy of `summ-server/ui/logo.svg` from the summ repository — keep them in step |
| `assets/` | The demo recording and the Open Graph image |
| `CNAME` | The custom domain GitHub Pages serves this on |
| `.nojekyll` | Serve the files as they are; no Jekyll pass |

## The demo slot

The page ships a static terminal transcript where the recording goes. When the
GIF exists, drop it in `assets/demo.gif` and replace the `<pre class="term-body">`
block with the `<img>` in the comment above it — the window chrome stays.

## Deploying

GitHub Pages, from `main` at the repository root: **Settings → Pages → Source:
Deploy from a branch → `main` / `/ (root)`**. The `CNAME` file above sets the
domain; the DNS records it needs are

```
summcr.com.      A     185.199.108.153
summcr.com.      A     185.199.109.153
summcr.com.      A     185.199.110.153
summcr.com.      A     185.199.111.153
www.summcr.com.  CNAME summcr.github.io.
```

Then tick **Enforce HTTPS** once the certificate is issued.
