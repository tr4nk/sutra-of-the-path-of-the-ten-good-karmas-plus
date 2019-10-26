
# Convert `markdown` to `pdf`

## Convert `markdown` to `epub` using `pandoc`

```bash
pandoc contents/* -o book.epub --toc
```

<!-- ### Use `calibre`

#### Prepare the `markdown` files

Create the `markdown` files and concat them into one file.

- In windows
```batch
type *.md > content.md
```

- In linux
```bash
touch content.md
cat *.md > content.md
```

#### Convert to `epub`

```bash
ebook-convert content.md out.epub [options]
```

* Input options
    - `--formatting-type`: markdown

* Output options
    - `--epub-inline-toc` (or `--epub-toc-at-end`): Add table of contents.
    - `--no-default-epub-cover`
    - `--toc-title` -->

## Convert `epub` to `pdf` using `calibre`

Edit the `epub` file before convertion.

### Look & feel

- Text
    - Text justification (`--change-justification`): Justify text (`justify`)
- Layout
    - Insert blank line between paragraphs (`--insert-blank-line`)
        - Line size (`--insert-blank-line-size`) 0.7em
- Styling (Extra css `--extra-css`)
```css
.calibre-pdf-toc{
    font-family: 'DFKai-SB';
    font-size: 0.8em;
}
```

### PDF Output

- `--uncompressed-pdf`: Generate an uncompressed pdf for debugging.
<!-- - "Use the pager size set in output profile" (`--use-profile-size`) -->
- "Add a printable Table of Contents at the end" (`--pdf-add-toc`)
<!-- - "Use page margins from the document being converted" (`--pdf-use-document-margins`) -->
- TOC title (`--toc-title`): 【索引】
- Font size (`--pdf-default-font-size`): 32px (28-32px)
- Page size (`--paper-size`): A5
- Page margin (`--pdf-page-margin-top`, `--pdf-page-margin-bottom`, `--pdf-page-margin-left`, `--pdf-page-margin-right`):
    - left, right: 1.7cm (48pt) (standard: 1.7cm 2.5cm)
    - top, bottom: 1.7cm (48pt) (standard: 2cm)

- Header (`--pdf-header-template`)

```html
<header style="justify-content: flex-end; font-size:0.5em;padding-right: 1em;">
    <div class="even-page"><i>_SECTION_</i></div>
    <div class="odd-page"><i>_TOP_LEVEL_SECTION_</i></div>
    <script>
        if ([1,2,3,6,25,39,40,56,65,95,102,117,127,132].includes(_PAGENUM_)) {
            var container = document.currentScript.parentNode;
            if (_PAGENUM_ % 2 === 0) {
                container.querySelector('.even-page').style.display = 'none';
            } else {
                container.querySelector('.odd-page').style.display = 'none';
            }
        }
    </script>
</header>
```

- Footer (`--pdf-footer-template`)

```html
<footer>
    <div class="page-num" style="margin: auto; font-size:0.4em;"><!-- _PAGENUM_ --></div>
    <script>
        var container = document.currentScript.parentNode.querySelector("div");
        if (
            ! ([1,2,39,102,117,127,132].includes(_PAGENUM_))
        ) {
            container.innerHTML = _PAGENUM_;
        }
    </script>
</footer>
```

## Reference

- Calibre:
    - Convert system: https://manual.calibre-ebook.com/conversion.html
    - `ebook-convert` command: https://manual.calibre-ebook.com/generated/en/ebook-convert.html
- Pandoc:
    - https://pandoc.org/MANUAL.html
