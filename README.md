# summcr-website

The source of <https://summcr.com> — the homepage for
[summ](https://github.com/summcr/summ), an OCI container registry.

Four files and no build step, for the same reason the registry's own UI has
none: `index.html`, `style.css`, `logo.svg`, and whatever lands in `assets/`.
Open `index.html` in a browser, or serve the directory:

```sh
python3 -m http.server 8000
```

`install.sh` is here too and is not part of the page: it is the installer the
domain publishes, and it is a copy of the one in the summ repository. See **The
installer** below before changing it.

## Layout

| Path | What it is |
|---|---|
| `index.html` | The whole page |
| `style.css` | The whole visual system. The palette is summ's own UI palette |
| `logo.svg` | A copy of `summ-server/ui/logo.svg` from the summ repository — keep them in step |
| `install.sh` | A copy of `scripts/install.sh` from the summ repository, served at `summcr.com/install.sh`. CI keeps them in step |
| `assets/` | The demo recording and the Open Graph image |
| `CNAME` | The custom domain GitHub Pages serves this on |
| `.nojekyll` | Serve the files as they are; no Jekyll pass |

## The installer

`https://summcr.com/install.sh` is the one-liner in the README, in `docs/setup.md`
and twice on the page above, so the file this repository serves at the root is
product surface rather than an asset. It is nonetheless a **copy**:
`scripts/install.sh` in [summ](https://github.com/summcr/summ) is the source —
it is the reviewable one, it sits beside the release workflow whose asset names
it depends on, and it is what `./scripts/install.sh` runs from a checkout.

GitHub Pages serves static files and cannot redirect, and an HTML redirect piped
to `sh` is not a shell script, so a pointer was not available and a copy it is.
Update it by copying, never by editing here:

```sh
cp ../summ/scripts/install.sh install.sh
```

`.github/workflows/install-drift.yml` diffs the two byte-for-byte on every push
and once a day, because drift begins with a commit in the *other* repository and
what it leaves behind — an older release installing perfectly well from the
domain every documented one-liner points at — fails silently otherwise.

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
