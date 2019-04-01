# Integrating data science tools with Wrattler

Wrattler is an interactive, smart and polyglot notebook system for doing
data science. It aims to be highly extensible, allowing a wide range of
other data science tools to plug into various parts of the system. This is
made possible because Wrattler architecture differs from most other notebook
systems in two ways:

 - **Browser-based.** Wrattler handles evaluation of notebook cells in the browser, which makes
   it possible to add rich, interactive browser-based components to Wrattler.
   Standard code editor (as known from Jupyter) are one such built-in plugin,
   but it's equally possible to implement a spreadsheet plugin that lets users
   add a spreadsheet as one of their cells or implement an interactive data
   visualization plugin or data cleaning tool.

 - **Dependency tracking.** Wrattler keeps a dependency graph between cells and takes care of passing
   of data between cells. It manages evaluation and state of the notebook,
   which makes it possible to mix multiple languages in a single notebook.
   Language support can also be added via plugins and can either run code on
   a server (for languages like R or Python) or in the browser (for languages
   that compile to JavaScript).

## Where to find more about Wrattler

Before discussing ways of integrating data science tools into Wrattler, here
are a couple of ways of seeing what Wrattler looks like:

 * **Overview slides.** If you have less than 5 minutes, check out [Wrattler demo slides
   (PDF)](demo.pdf). This is a slide deck with screenshots, showing
   the main features of Wrattler.
 * **Architecture paper.** If you have more time, you can also review [our TPS workshop poster
   (PDF)](poster.pdf), which adds some more information on the architecture.  
 * **Running Wrattler.** If you have more than 15 minutes and Docker installed, you can run Wrattler
   easily on your computer by following [instructions here](https://github.com/wrattler/wrattler/blob/demo-mar-2019/Running_Wrattler_via_Docker.md). This
   comes with several sample notebooks showing the key features.

If you have even more time and prefer to read academic papers, the following
are good resources for learning even more:

 * [Wrattler: Reproducible, live and polyglot notebooks (PDF)](tapp2018.pdf)
   is a paper outlining the architecture, evaluation of notebooks and tracking
   of dependencies (published in a workshop on provenance).
 * [AI assistants: A framework for semi-automated, accountable, tooling-rich
   data wrangling (PDF)](ai-assistants.pdf) is a draft that talks about
   "AI assistants", which are plugins that assist data analyst with tedious
   data cleaning tasks by suggesting possible cleaning scripts.

## Ways of integrating new tools into Wrattler

There are several ways in which other data science tools can be integrated into
Wrattler already. However, we are very keen on adapting the architecture so that
it allows other kinds of integrations that are not listed below. If you can think
of something that does not fit into any of the models below, let us know! We
might be missing something important.

#### 1. Ordinary R or Python library

Wrattler already has bindings for R and Python, so any R or Python library can
be loaded into Wrattler. This is not particularly "deep integration", but it
has benefits already - for example, Wrattler makes it possible to call your R
library from Python! There is also more that could be done here if your library
needs a more interactive user interface or richer outputs.

#### 2. Ordinary JavaScript library

Wrattler also supports JavaScript and JavaScript libraries can be directly
loaded. Wrattler can pass R or Python data frames to JavaScript cells, so
you can use JavaScript library in a Python/R data analysis without having any
explicit bindings. Again, if you have a more interactive output or interface,
Wrattler can support that.

#### 3. Julia, F#, Racket, Lua, STAN and more

If you are creating tools for other languages, it's quite easy to create a new
language plugin for Wrattler which will make it possible to use your favourite
language and also any libraries that you create for it in bigger data analyses
that use other languages. The fact that a library in some less main-stream
language can be easily mixed with code in Python or R is very nice, because it
lowers the barrier for trying a new tool!

#### 4. Semi-automatic AI assistants

We've been working on a range of semi-automatic tools that help data scientist
with some tedious task (filling missing values, parsing data, reconciling
structure of multiple datasets). Such tasks are hard to fully automate, because
they often need some human insight or hint. In Wrattler, we're working on an
infrastructure for "AI assistants" which are semi-automatic tools that interact
with the analyst by offering best solution, but then let the analyst provide
feedback or constraints that refine this. This is still in early stage, but
there is more information about this in the above "AI assistants" paper.
Any semi-automatic tool might be able to reuse our infrastructure though!

#### 5. Adding custom cell types

Standard Wrattler cells have editor for modifying code and output tabs showing
exported data frames and other outputs. However, it's possible to create custom
cells that do something completely different (you can write your own JavaScript
to do whatever you want). The cell gets access to data frames defined earlier in
the notebook and can export new data frames. This could be used for various
visualization tools, graphical workflow systems, spreadsheet-like systems and
various other systems.

#### 6. Exploiting data store or dependency graph

Finally, Wrattler also exposes some interesting information about the notebooks
it works with. You can get access to all data in the notebook (including
intermediate steps and soon also past versions of data) and you can get access
to the dependency graph (soon also past versions) that Wrattler maintains. This
might be interesting for doing analysis on notebooks (e.g. to make
recommendations based on past actions) or building refactoring tools that turn
notebooks into production-ready code.

