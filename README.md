<p align="center">
  <img src="assets/banner.svg" alt="Parthenogenisis 13" width="100%">
</p>

# Parthenogenisis 13

A book in progress. Each chapter is published as text and as a narrated audio version, on one page.

<img src="assets/divider.svg" alt="" width="100%">

## Repository map

```
README.md
assets/
  banner.svg
  divider.svg
book/
  00-book-plan.md      the outline the book follows
  chapters/            the manuscript, one file per chapter (NN-title.md)
docs/
  index.html           the published site (built by scripts/build_site.py)
  cover.svg
  audio/               chapter narration (built by scripts/make_audio.py)
scripts/
  build_site.py        builds docs/index.html from the chapter files
  make_audio.py        narrates each chapter into docs/audio/NN.mp3
.github/workflows/
  static.yml           publishes docs/ to GitHub Pages
  jekyll-gh-pages.yml  manual-only alternative; not used for deploys
```

## Adding a chapter

1. Add the chapter as `book/chapters/NN-short-title.md` (for example `01-first-chapter.md`). The first line is the chapter title: `# Chapter 1: Title`.
2. Rebuild the audio for that chapter, then rebuild the site:

```bash
pip install kokoro-onnx soundfile markdown
python3 scripts/make_audio.py 01        # or no number for all chapters
python3 scripts/build_site.py
```

3. Commit the chapter, its audio, and the rebuilt `docs/index.html`.

The title and subtitle on the site are set at the top of `scripts/build_site.py` (`BOOK_TITLE`, `BOOK_SUBTITLE`).

The narration uses [Kokoro-82M](https://huggingface.co/hexgrad/Kokoro-82M) (Apache 2.0) through [kokoro-onnx](https://github.com/thewh1teagle/kokoro-onnx). The model downloads to `~/.cache/book-tts/` on first run. Audio is generated from the book text only; the draft banner and any "Review notes" section are skipped.

## Status

Set-up stage. No chapters have been added yet.
