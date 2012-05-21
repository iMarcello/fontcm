# fontcm

This package contains the Computer Modern font with Paul Murrell's symbol extensions, and is to be used with the extrafont package.

The fonts are a subset of the [cm-lgc font package](http://www.ctan.org/tex-archive/help/Catalogue/entries/cm-lgc.html).
The faces with small caps and italics using old-style numerals (which can hang below the baseline) are not included with this package.


# Installation

First, make sure that you have [extrafont](https://github.com/wch/extrafont) installed.

Then, to install `fontcm`:

```R
install_github('fontcm', 'wch')

library(extrafont)
font_addpackage('fontcm')
```

You can check to see if they're properly installed:

```R
fonts()
# "CM Roman"               "CM Roman Asian"         "CM Roman CE"
# "CM Roman Cyrillic"      "CM Roman Greek"         "CM Sans"
# "CM Sans Asian"          "CM Sans CE"             "CM Sans Cyrillic"
# "CM Sans Greek"          "CM Symbol"              "CM Typewriter"
# "CM Typewriter Asian"    "CM Typewriter CE"       "CM Typewriter Cyrillic"
# "CM Typewriter Greek"

# For more detailed font information:
font_load_table()
```


## Use example

Here is an example of using Computer Modern fonts with math symbols.

```R
library(ggplot2)
library(extrafont)

setupPdfFonts()

pdf('fontcm.pdf', width=4, height=4)

# Base plot
p <- qplot(c(1,5), c(1,5)) +
  xlab("Made with extrafont") + ylab("Made with extrafont") +
  opts(title = "Made with extrafont")


# Without the new fonts
p + annotate("text", x=3, y=3, parse=TRUE,
             label="frac(1, sqrt(2 * pi)) * e ^ {-x^2 / 2}")

# With the new fonts
p + annotate("text", x=3, y=3, parse=TRUE, family="CM Roman",
             label="frac(1, sqrt(2 * pi)) * e ^ {-x^2 / 2}") +
  opts(plot.title = theme_text(size=16, family="CM Roman")) +
  opts(axis.title.x = theme_text(size=16, family="CM Roman", face="italic")) +
  opts(axis.title.y = theme_text(size=16, family="CM Sans", face="bold", angle=90))

dev.off()

# Embed the fonts
embedExtraFonts('fontcm.pdf', outfile='fontcm-embed.pdf')
```
