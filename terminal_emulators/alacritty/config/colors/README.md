# `[colors]`

## Location and format

The `[colors]` table is part of the main configuration file. The colours are specified via hexadecimal values in the form `#RRGGBB`.

For example:

```toml
[colors]
# … etc …
```

---

## High‐level structure

Within the `[colors]` table you will find several nested subtables. Important ones include:

* `[colors.primary]`; defines the primary foreground/background colours.
* `[colors.cursor]`; colours for the cursor text and cursor cell.
* `[colors.vi_mode_cursor]`; when vi-mode is active, the cursor colours can differ.
* `[colors.selection]`; colours used when text is selected.
* `[colors.search]`, `[colors.hints]`; for search highlights and hint labels respectively.
* `[colors.normal]`, `[colors.bright]`, `[colors.dim]`; these subtables define the ANSI-style colour palette (normal and bright variants, and dimmed variants).
* `indexed_colors`; an array for extended colour indices (from 16-255).
* Misc flags, e.g. `transparent_background_colors`, `draw_bold_text_with_bright_colors`.

---

## Key fields and their semantics

### `primary`

In `[colors.primary]`, you typically see:

* `foreground = "<hex colour>"` → the default text colour.
* `background = "<hex colour>"` → the terminal background colour.
* `dim_foreground = "<hex colour>"` → a dimmed version of the foreground. If not specified, Alacritty auto-calculates one.
* `bright_foreground = "<hex colour>"` → only used when `draw_bold_text_with_bright_colors` is true.

### `cursor` and `vi_mode_cursor`

* In `[colors.cursor]`, the keys are `text` and `cursor`. `text` refers to the colour of the text under the cursor, `cursor` refers to the cursor cell. You may also use the special values `CellForeground`/`CellBackground` to reference cell’s original colours.
* `[colors.vi_mode_cursor]` works similarly when the terminal enters vi‐mode. It allows a different cursor appearance.

### `selection`, `search`, `hints`

* `[colors.selection]` defines how selected text appears: e.g. `{ text = "<hex>", background = "<hex>" }`.
* `[colors.search]` and `[colors.hints]` provide highlight colours for matches in search mode, and hint labels (e.g., clickable links or numbered hints) respectively.

### `normal`, `bright`, `dim`

* `[colors.normal]` maps the standard 8 ANSI colours: black, red, green, yellow, blue, magenta, cyan, white.
* `[colors.bright]` maps the “bright” variants of those same colours (so e.g. bright red, bright green …).
* `[colors.dim]` is for dimmed colours; if omitted the values are calculated automatically.

### `indexed_colors` and other flags

* `indexed_colors` is an array of `{ index = <integer>, color = "<hex>" }` entries, mapping to colour indices 16-255. This is useful when using full 256-colour or 24-bit schemes.
* `transparent_background_colors = true | false`: if true the window opacity applies to *all* cell backgrounds, not just default background.
* `draw_bold_text_with_bright_colors = true | false`: when true, bold text uses the bright palette instead of “just bold”.

---

## Example snippet

```toml
[colors]
  [colors.primary]
    foreground = "#ffffff"
    background = "#000000"
    dim_foreground = "#7f7f7f"

  [colors.cursor]
    text = "#000000"
    cursor = "#ffffff"

  [colors.normal]
    black   = "#000000"
    red     = "#ff5555"
    green   = "#50fa7b"
    yellow  = "#f1fa8c"
    blue    = "#bd93f9"
    magenta = "#ff79c6"
    cyan    = "#8be9fd"
    white   = "#bbbbbb"

  [colors.bright]
    black   = "#555555"
    red     = "#ff6e6e"
    green   = "#69ff94"
    yellow  = "#ffffa5"
    blue    = "#d6acff"
    magenta = "#ff92df"
    cyan    = "#a4ffff"
    white   = "#ffffff"
```

This example sets a dark background, white foreground, custom cursor colours, and a 16-colour palette.

---

## Practical tips and considerations

* Ensure you use valid hex values (`#RRGGBB`). Alacritty expects this format.
* When editing colour values, you may need to restart Alacritty (or rely on live config reload if enabled) for changes to take effect.
* If bold text appears with the same colour as non-bold text, check whether `draw_bold_text_with_bright_colors` is set appropriately, and whether your bright palette differs.
* Use `indexed_colors` only if you need extended palette beyond the standard 16 colours.
* Be aware of environmental factors: your shell, TERM variable, or remote session may influence which colours are used or how they render. For example, if you notice colours not matching expected values, it may be due to how your terminal or `TERM` reports support.

---
