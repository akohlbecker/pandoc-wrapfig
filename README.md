# pandoc-wrapfig: A pandoc filter for pdf/LaTeX export with the wrapfig package

pandoc-wrapfig is a simple [pandoc][] filter written in python 3. It simply
allows use of the [wrapfig][] package so that (specified) figures will have text
wrapped around them.

## Installation

Obviously, the wrapfig package must be installed.

A pandoc template must be used that contains `\usepackage{wrapfig}`. The
included template is the default pandoc LaTeX template with this line added.

## Usage

Simply include ` {x}` at the end of the captions for figures that are to be
wrapped. `x` is a number that specifies the width of the wrap in inches. Setting
it to 0 will cause the width of the figure to be used (as per the wrapfig
package instructions). Figures without the tag will float as usual. Optionally
precede x with a character in the set {l,r,i,o} to set wrapfig's placement
parameter, or the uppercase variants {L,R,I,O} to let the image flow in the
wrapfig box. By using the float feature images hanging over page breakes can
be avoided. default is 'L'. . Optionally follow ?  with a '-' and another width
specification to set wrapfig's overhang parameter and push the figure that far
into the margin.

To use a specific length, you may also add `cm`,`pt`or `in` like `{5cm}`.

Also, wrapfig allows optional specification of the "number of narrow lines" that
are aquivalent to height of the image. Though guessed by wrapfig, this sometimes
has to be adjusted. This is possible by adding a second number to the `{}`
argument like: `{5cm,28}`.

Wrapping is specific to pdf/LaTeX output. For other formats, the tag is simply
removed.

### vertical align wrapfig with text

Set the `\intextsep` globally, but only for the wrap figure environemnt and
declare `\usepackage{wrapfig}` as usaually. In pandoc markdown this can be done
by using the  header-includes option in the metadata header:

~~~
 header-includes:
 - \usepackage{wrapfig}
 - |
     \BeforeBeginEnvironment{wrapfigure}{\setlength{\intextsep}{0pt}}
~~~

see https://tex.stackexchange.com/questions/415398/adjust-intextsep-for-wrapfigure-only
for more options of vertical alignment with text.

### Tufte-latex margin figures

For users of the [tufte-latex](https://ctan.org/pkg/tufte-latex?lang=en)
package, pandoc-wrapfig can produce margin figures with tufte-latex's
marginfigure environment. Example:

```markdown
![Image caption {m0}](image.png)
```

You must have tufte-latex and its dependencies installed and your document class
must of course be set to `tufte-handout` or `tufte-book`.

[pandoc]: http://pandoc.org
[wrapfig]: https://www.ctan.org/pkg/wrapfig?lang=en
[tufte-latex]: https://ctan.org/pkg/tufte-latex?lang=en
