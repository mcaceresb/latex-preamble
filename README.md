## LaTeX Preambles v1.0.0

The main files here are `mcpreamble.sty` for LaTeX and `mcbeamerpreamble.sty` for beamer. They are my prefered preambles (and I add some options I like) and are meant for personal use. Copy at your own risk. Suggestions are appreciated. **PLEASE NOTE I AM JUST DESCRIBING `mcpreamble` HERE AND NOT `mcbeamerpreamble`**

## Quickstart

Make sure the `.sty` files are in your global or local [`texmf`](https://www.google.com/search?q=where+is+texmf) directory. Alternatively you can keep this file in the same directory as the `.tex` file you want to compile, but that would defeat the purpose of making a preamble into a package. Anyway, then add `\usepackage[summary]{mcpreamble}` to the preamble and `\displayoptions` to the main text.
```tex
\documentclass{article}
\usepackage[summary]{mcpreamble}
\begin{document}
\displayoptions
Hello. This is a very simple file. Here is some math:
\[ \alpha(n) = \sum^{n}_{i = 0} i^2 \]
\end{document}
```

You might want to edit
```tex
\renewcommand\sectiontype{\thesection\ } % Before section text
\renewcommand\mcauthor{First Last}       % Author (header right)
\renewcommand\mccustomll{Header left}    % Left header is \mccustomll -- \mccustomlr
\renewcommand\mccustomlr{Header right}   % Ibid.
```

and edit accordingly, as the defaults in `mcpreamble` contain my name and such.

## Vim amd UltiSnips

I use [`vim`](http://www.vim.org/) for editing text with the excellent [`UltiSnips`](http://github.com/sirver/UltiSnips) plugin. I include the snippet definitions I use for document templates in the repository, as they are an important complement to this package. Without them switching between styles would be rather difficult.

## Description

I turned my preferred LaTeX preamble into a `.sty` file so it could be loaded as a package. Why?

1. I can load almost my preferred defaults just with `\useackage[option]{mcpeamble}`
2. The difference between my template for a recitation or a summary or a homework almost always amounts to nothing more than some slight changes to title and header style and definitions. In an `.sty` file I can specify package options and change between these easily. Further, I can actually make relatively significant format changes without that much of a hustle while keeping all the packages and definitions I would like to keep.
3. Often I find that not all the commands I expect are there. Then I have to go hunting for a particular version of `preamble.tex` and it becomes messy.

I recommend doing this for your own LaTeX preamble, but if you have a better idea do let me know (:

## Features

For a complete list of packages loaded see the `.sty` files. The features each of these packages provide are better explained in their own documentations. Here I just summarize how I use them, if relevant. The following are particularly important

* [TikZ](http://sourceforge.net/projects/pgf/) is an excellent package for drawing vector graphics. I load several libraries and define some styles for making it easier to draw trees.
* [PGFPlots](http://pgfplots.net) complements TikZ beautifully and allows drawing functions very easily.
* [The AMS packages](http://ams.org/publications/authors/tex/amslatex) are always good to have for nice math addons.
* [`hyperref`](http://www.tug.org/applications/hyperref/manual.html). By default links are colored a shade of purple and have no border.
* [`listings`](http://ctan.org/tex-archive/macros/latex/contrib/listings/) for making code look pretty. By default
    * Spaces are not highlighted
    * Tabs are 4 spaces
    * `flexiblecolumns` is set to `true`
    * Comments are gray and italicized
* [`microtype`](http://ctan.org/tex-archive/macros/latex/contrib/microtype/) for generally nicer-looking text.
* [`titlesec`](http://ctan.org/tex-archive/macros/latex/contrib/titlesec/) for title format manipulation.
* [`fancyhdr`](http://ctan.org/tex-archive/macros/latex/contrib/fancyhdr/) for fancy header.

Additionally, the following are available for use

* Shades of gray `light-gray`, `normalgray`, `displaygray`
* `hidelevel` environment hides everything within it if its option is set below `SetHideLevel`.
* `tacomment` wraps text in `hidelevel` and additionally
    * Adds horizontal lines before and after the text
    * Prints text in `normalgray` and `footnotesize`
    * Corrects figure captions to print in `footnotesize`
    * Corrects footnotes and figure captions to print in `normalgray`
* `smiley` for a happy face and `sadness` for a sad face.
* `displayoptions` to pass display options to the main text.
* Various `mc*` commands used in the packages' options.

### Maths

* Declares `argmin`, `argmax`, `vect`, `pmax`, `pmin` as math operators.
* Declares symbols `toto` (correspondence), `indep` (orthogonal).
* Declares commands `diag` (diagonal matrix), `ind` (indicator function).
* Declares commands `set`, `norm`, `abs`, `ceil`, `floor` (self-evident).
* Declares wrappers for `\Big[char] #1 \Big[char]` and `\left[char] #1 \right[char]` to use as `\(B|F)(set|par|rac|abs|norm|ceil|floor){#1}`.
* Declares theorem environments `theorem`, `claim`, `corollary`, `definition`, `lemma`, `proposition`, `assumption`, `remark`.

### Options

Most options use the `quattrocento` font with `mathpple` math and show the author's name in the top right. Default numbering is arabic. Default space after section is `36pt`. The following options are available

* `summary` is a basic option.
    * Pre-section text is `Summary #:`
    * Left header as `\mccustomll -- \mccustomlr`
* `homework` is my preferred HW template.
    * Pre-section text is `Problem #:`
    * Left header is `\mcsemester\ \mcyear\ -- \mcclassshort\ \mccustomlr`
* `recitation` is my preferred recitation template. For this, the UltiSnips template is particularly relevant!
    * Pre-section text is `Recitation #:`
    * Left header is `\mcsemester\ \mcyear, \mcclassshort\ -- \sectiontype\ \leftmark\ \mcdate`
    * Defines a subsection-based table of contents.
    * The snippet shows a message explaining these are recitation notes and adds `\printcontents{}{2}` for a local subsection-based ToC. Further, it labels the ToC and references it right before each section with a hyperlink reading `$\uparrow$ Up to top`. Lastly, redefines the date to be the next time the recitation is happening.
* `classnotes` is a template for class notes.
    * Pre-section text is `Lecture #:`
    * Left header is `\mcsemester\ \mcyear, \mcclassshort\ -- \sectiontype\ \mcdate`
    * The snippet defines the date to be today.
* `mcpaper` are options to go from my custom LaTeX format to a more standard format for writing serious stuff.
    * Title, author, and date are typeset using LaTeX's `\maketitle`
    * No fancy header. We use `\pagestyle{plain}`
    * Titles are understated and go back to `#. Section`

The following options are identical to `mcpaper` but use a particular font. Why create an entire option just for fonts? Because switching fonts in LaTeX is not trivial. Also, the following must be loaded after fonts are declared: `\usepackage{bm}` for bold math symbols and  `\usepackage[italic]{mathastext}` for rendering text in math to match text outside of math. Anyway:
* `fancypaper` is `mcpaper` using `palatino`
* `normalpaper` is `mcpaper` using computer modern and default math.
* `fancypaperalt` is `mcpaper` using `quattrocento` and `mathpple`

## TODO

* Figure out math environments (theorems, proofs, etc.) Mainly numbering and style.
* How to set XeLaTeX math font?
* Does setlist work with nested lists the way I like?
* Set up a default ToC style.
* Figure out how to use references (with natbib?) and default citation style.
* Check that lstlistings works as expected.
* Decide if using `dot` and `ddot` is worth the extra font hassle.
* Figure out beamer styles.
* Delete "paper" options and add a font selection to snippet instead.

## Copyright and License

Choose a license. Recall the `\smiley` and `\sadness` code you got online.
