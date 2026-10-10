# Hugo Lithium

A simple responsive blog theme for [Hugo](https://gohugo.io/) forked from https://github.com/jrutheiser/hugo-lithium-theme with modifications to make it work better with [**blogdown**](https://github.com/rstudio/blogdown).

The easiest way to get started is to create a new (empty) RStudio project, then

```r
devtools::install_github('rstudio/blogdown')  # install blogdown
blogdown::new_site(theme = 'yihui/hugo-lithium')
```

Then you should be able to see an example website launched in the RStudio Viewer.

For the full documentation, please see this section in the **blogdown** book: https://bookdown.org/yihui/blogdown/themes.html

## Features

- Blog
- Responsive
- Disqus
- Google Analytics
- Google web fonts (Merriweather and Lato)
- MathJax
- highlight.js

## Changes

The main changes I made to the original hugo-lithium-theme are:

1. Added support for [MathJax](https://bookdown.org/yihui/blogdown/output-format.html) (for rendering LaTeX math expressions) and highlight.js (for syntax highlighting).

    - For both libraries, you can specify the CDN host (e.g., CloudFlare, BootCDN, ...).

    - For highlight.js, you can specify additional languages (e.g., `r`, `yaml`, `tex`, ...).

1. Added Google web fonts (embedded in the theme so that visitors from countries where Google is banned can still see the typefaces).

1. Improved Hugo's built-in Disqus template, so that you can actually the comments even when you are previewing the website locally.

1. Replaced the variable `.Permalink` with `.RelPermalink`, and function `absURL` with `relURL` where necessary. It is a bad idea to use full absolute links (with the protocol and domain) in general. For example, `.Permalink` and `absURL` may generate URLs of the form `http://www.example.com/foo/bar.html`, but `/foo/bar.html` is more portable.

## Site image maintenance

Blog covers and the `img` shortcode use `partials/responsive-image.html` to
generate width-based candidates and intrinsic dimensions without upscaling.
The portrait uses compressed JPEG variants of the original static PNG.
`partials/image-sizes.html` and the shortcode's floated-image slots must stay
in sync with the column and figure breakpoints in `static/css/mobile.css`.
The `compact` figure class retains small illustrations with text wrapping,
including on phones. Use the `badge` shortcode for small licensing images.
Images remain eager; lazy loading and asynchronous decoding are deferred.

The sharper fingerspelling PNG can be regenerated from the vector PDF by
running this command from the repository root (requires Poppler):

```sh
pdftoppm -singlefile -scale-to-x 2200 -scale-to-y -1 -png 'content/older projects/Asl_alphabet_gallaudet.pdf' static/images/Asl_alphabet_gallaudet
```

## License

The original hugo-lithium-theme was released by Jonathan Rutheiser under [the MIT License](https://github.com/jrutheiser/hugo-lithium-theme/blob/master/LICENSE.md). The modified version in this repository is also released under MIT.
