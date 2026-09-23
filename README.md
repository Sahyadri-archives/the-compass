# The Compass — website

Online magazine of the Community Mathematics Centre, Schools of the Krishnamurti Foundation India (KFI).

The whole site is one file, `index.html`. It needs no build step and runs on GitHub Pages as is.

## Folder layout

```
the-compass/
├── index.html
├── README.md
├── pdfs/                         ← magazine PDFs go here
│   ├── The-Compass-Vol-3-3.pdf
│   ├── The-Compass-Vol-3-2.pdf
│   └── …
└── covers/                       ← optional cover images
    └── vol-3-3.jpg
```

PDF file names must match the `file` entries in the `ISSUES` list near the bottom of `index.html`.

## Publishing on GitHub Pages

1. Create a new public repository on GitHub (for example `the-compass`).
2. Add `index.html`, `README.md` and the `pdfs` folder to it (see the note on large files below).
3. In the repository, open **Settings → Pages**. Under "Build and deployment", choose **Deploy from a branch**, select `main` and `/ (root)`, then **Save**.
4. After a minute or two the site is live at `https://<your-username>.github.io/the-compass/`.

## Large PDF files: important

GitHub has file-size limits that matter for a magazine archive:

- **Uploading through the GitHub website is limited to 25 MB per file.** A 45 MB PDF must be added with **GitHub Desktop** or the `git` command line instead.
- GitHub warns about files over 50 MB and **refuses files over 100 MB**.
- Don't use Git LFS for the PDFs: GitHub Pages doesn't serve LFS files.
- A GitHub Pages site should stay under about 1 GB in total.

If issues grow past 100 MB, or the archive gets close to 1 GB, attach the PDFs to a **GitHub Release** instead (each file there can be up to 2 GB) and put the release download link in the `file` field. Downloads still work; the progress bar just changes to a "Starting download…" indicator, because the browser can't measure files hosted on a different address.

## Adding a new issue

Open `index.html`, find `const ISSUES = [` and add the new issue at the **top** of the list. The first entry automatically becomes the current issue (including the hero line), and the previous one moves into the archive.

```js
{ id:"3-4", volume:3, number:4, month:"October", year:2026, file:"pdfs/The-Compass-Vol-3-4.pdf", size:"", cover:"" },
```

- `size` — leave empty and the site reads the real file size once it's online, or type it yourself (`"45 MB"`).
- `cover` — leave empty for a generated cover, or give an image path such as `"covers/vol-3-4.jpg"` (an A4-shaped image around 600 × 850 px works well).

## Testing on your own computer

Opening `index.html` by double-clicking works, but file sizes and the download progress bar only appear when the site is served from a web address. To preview properly, run this in the folder and open `http://localhost:8000`:

```
python3 -m http.server 8000
```

## What's inside

- 3D brass compass: three.js. The case turns as you scroll, and the needle swings and settles back to north.
- Antique world map: d3 and Natural Earth data, drawn with engraved coastlines and portolan rhumb lines.
- Fonts: Cormorant Garamond (headings) and Source Sans 3 (body text), from Google Fonts.
- Accessibility: works with keyboard and screen readers, and respects the "reduce motion" setting. If 3D isn't available, a flat compass is shown instead.
