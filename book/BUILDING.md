# Building the site and the audio

This repository publishes the book as a chapter reader on GitHub Pages.

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

1. Add the chapter as `book/chapters/NN-short-title.md`. The file starts with `CHAPTER <numeral>` and the title on the next line, followed by the text.
2. Rebuild the audio for that chapter, then rebuild the site:

```bash
pip install kokoro-onnx soundfile markdown
python3 scripts/make_audio.py 06        # or no number for all chapters
python3 scripts/build_site.py
```

3. Commit the chapter, its audio, and the rebuilt `docs/index.html`.

The title and subtitle on the site are set at the top of `scripts/build_site.py` (`BOOK_TITLE`, `BOOK_SUBTITLE`).

The narration uses [Kokoro-82M](https://huggingface.co/hexgrad/Kokoro-82M) (Apache 2.0) through [kokoro-onnx](https://github.com/thewh1teagle/kokoro-onnx). The model downloads to `~/.cache/book-tts/` on first run. Audio is generated from the book text only.
