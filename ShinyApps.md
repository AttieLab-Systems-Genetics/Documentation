# Shiny Apps

Shiny apps are cool, but they can get complicated, and frustrating to debug.
Complicated apps--longer than 100-150 lines of code--can
have subtle paradoxes caused by reactive elements.
It is helpful to think carefully about how to modularize apps,
much as we do with functions, so that we can debug piece by piece.

Apps developed by [Brian Yandell](https://github.com/byandell)
illustrate an evolution of design over time
that make them easier
to use, understand and debug.
They include some lessons learned that hopefully will
help others as they design and evolve apps for this project.

The best reference for building shiny apps is
[Mastering Shiny](https://mastering-shiny.org),
with particular attention to Ch 19 on
[Shiny modules](https://mastering-shiny.org/scaling-modules.html).
See also
[Modularizing Shiny app code](https://shiny.rstudio.com/articles/modules.html).
Yandell's key working repos that inform this document are 

- [Shiny Geyser App with and without Modules](https://github.com/byandell/geyser)
- [Founder Shiny App](https://github.com/AttieLab-Systems-Genetics/foundrShiny)
- [Shiny app for R/qtl2](https://github.com/byandell-sysgen/qtl2shiny)
- [Learning about Shiny Modules](https://github.com/byandell/shiny_module)

These are listed in reverse chronological order.
That is, Yandell's most recent work is in the
[geyser](https://github.com/byandell/geyser)
repo, using a simple app (Old Faithful) to illustrate the components of
a shiny app, and how to build up more complicated apps using shiny modules.
It starts with creating one shiny module around this classic example,
and builds out to a half-dozen shiny modules in the
[geyser/R](https://github.com/byandell/geyser/tree/main/R)
folder,
which can be interconnected to build more complicated apps, such as
[inst/connect_modules/app.R](https://github.com/byandell/geyser/blob/main/inst/connect_modules/app.R)
deployed as
<https://connect.doit.wisc.edu/geyserDemo/>.
For more information, see the
[Geyser Shiny Modules](https://connect.doit.wisc.edu/geyserShinyModules)
slide deck, as well as the 
[11 Dec 2024 Presentation](https://drive.google.com/file/d/1BGSIhihpBc-2TfRza5RGeXBCB55EC6-l).

The
[foundrShiny](https://github.com/AttieLab-Systems-Genetics/foundrShiny)
repo is the basis of three tools actively used by the Attie Lab

- <https://connect.doit.wisc.edu/FounderCalciumStudy/>
- <https://connect.doit.wisc.edu/FounderDietStudy/> (requires password)
- <https://connect.doit.wisc.edu/FounderLiverDietStudy/> (requires password)

This is an R package, with each code file in the
[founderShiny/R](https://github.com/AttieLab-Systems-Genetics/foundrShiny/tree/main/R)
folder itself a shiny module with a
server function, UI functions, and an app function.
These ~30 shiny modules are interconnected as described in the
[Foundr App Developer Guide](https://docs.google.com/presentation/d/171HEopFlSTtf_AbrA28YIAJxJHvkzihB4_lcV6Ct-eI),
in various ways to build the tools cited above.
Some of those modules could be used (almost) directly for creating new shiny modules.
For instance, the
[download.R](https://github.com/AttieLab-Systems-Genetics/foundrShiny/blob/main/R/download.R)
module takes a list containing filename, plot, and table objects and
arranges downloads.
There are also ideas about creating and visualizing plots and tables that could prove useful.
Further, there was a lot of work on figuring out how to organize input parameters
across shiny modules to share inputs without duplication of code.

The
[qtl2shiny](https://github.com/byandell-sysgen/qtl2shiny)
repo was designed about a decade ago,
and is not currently working.
However, one can view screenshots and the User's Guide.
This repo has ~25 shiny modules in
[qtl2shiny/R](https://github.com/byandell-sysgen/qtl2shiny/tree/main/R),
although they do not (yet) follow the conventional naming of
server and UI functions, and they do not have app functions.
Nevertheless, they have many features that are being considered in current development;
these could be usefully retooled for a modernized qtl2 shiny app.

Finally, the
[shiny_module](https://github.com/byandell/shiny_module)
repo has some early learnings about reactivity.
It is perhaps useful as a reference when trying to figure out
why reactive code is not working.
However, it is rather dated at this point.
