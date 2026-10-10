Personal site

[![Netlify Status](https://api.netlify.com/api/v1/badges/c74b6216-637e-4dbb-aab7-4f7c313cb31e/deploy-status)](https://app.netlify.com/sites/sharp-neumann-8ff22c/deploys)

## Image export sizes

For sharp images on 3× Retina displays, export at **three times the largest
displayed width**, with height scaled proportionally. These sizes are image
pixels; the layout's displayed widths are CSS pixels. Use the image's **width**,
not its longest edge, when setting export dimensions, including for portrait
photos.

| Kind of image | Recommended export for 3× displays |
| --- | --- |
| Blog cover | **2200px wide**, cropped to approximately **3.5:1 (width:height)**; about **2200 × 630px**. |
| Full-width photo within an article | **2200px wide**, keeping the intended aspect ratio. |
| Article photo that floats beside text on desktop | **2200px wide**: these photos expand to the article width on smaller screens. |
| Chart, diagram, or illustration that can expand to the article width | **2200px wide** when exporting a raster image; render from a vector original when available. |
| Compact illustration that stays small on every screen | **3× its maximum displayed width**; for example, export 450px wide for a 150px illustration. |
| Navigation portrait | **480 × 480px** for the largest 160 × 160px display size. |

**2200px wide is a convenient default for covers and regular article images.**
The current article column reaches 700 CSS pixels on desktop and is capped at
640 CSS pixels on mobile. A 700px slot needs 1400 source pixels at 2× or 2100
at 3×; rounding up to 2200 also leaves a little room for layout adjustments.
Recalculate from the largest displayed width if the layout changes.

Blog covers and images using the `img` shortcode get smaller responsive
versions automatically, so only one source export is needed. The browser
selects a suitable size for the displayed width and screen density. Separate
manual 1×, 2×, and 3× exports are unnecessary for those images. For small icons
and badges, use vector artwork where supported or apply the same 3× rule to
both displayed dimensions.

### Image shortcode examples

Use `img` in the article's Markdown, with the image in the same page bundle
as `index.md`. Its arguments are the filename, caption, CSS classes, optional
displayed width in CSS pixels, and optional alt text. The width controls the
layout, not the source export size. Captions are read by screen readers; alt
text defaults to empty and can be supplied as a fifth argument when it adds
information beyond the caption.

For a full-width photo, omit the width and use `fullwidth`:

```go-html-template
{{< img "yanagiba-saya.jpg" "Yanagiba and saya" "fullwidth" >}}
```

For photos that float beside text on desktop, set a displayed width and choose
the side:

```go-html-template
{{< img "IMG_3906.jpg" "Hanuman, pointing the way" "floatleft" "300" >}}
{{< img "000057270012.jpg" "linen, text, art" "floatright" "300" >}}
```

For a compact illustration that stays small and lets text wrap beside it,
combine `compact` with `floatright` or `floatleft` and supply a width:

```go-html-template
{{< img "132.png" "Ditto ©Pokémon" "floatright compact" "125" >}}
```

This displays at up to 125px wide, so aim for a **375px-wide source** for 3×
displays. On narrow screens it can shrink to fit, while keeping the wrapped
layout. For a 150px illustration, use `"150"` and export at 450px wide.
