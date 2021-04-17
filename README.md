# Latex-config
Personal LaTeX setup: style sheet for packages, fonts, etc. and config-file for variables and custom title pages etc. to fit my whims and needs. 
I mainly write musicological essays, therefore I have devised a way to include short music examples with the wonderful `lyluatex`-package. 
Since most of my research focuses on the early modern period and since I like my typography to match my subject, I am using the lovely humanist open source font [EB Garamond](http://www.georgduffner.at/ebgaramond/index.html), based on [Claude Garamond’s](https://en.wikipedia.org/wiki/Claude_Garamond) 16th century cuts. 
So far, I have not needed another font, if I come into the situation, I might outsources the font setup in its own dedicated setup file.
The defaults of this setup are set for German meta information (i.e. the stuff on the cover page and the plagiarism statement) and a language for the body text, typically German or English, that can be specified in the `config.tex` file.

## Explanation 
The `custom-style.sty` file contains commonly loaded packages, a font configuration for EB Garamond, the hyperref-setup, etc.

The `config.tex` file contains all the variables for handing in an academic term paper, as well as setups for custom titlepage, anti-plagiarism declaration, works cited etc.

The command `\mylilypond` calls for the `lyluatex` package, which requires an installation of [Lilypond](https://lilypond.org/) in order to work. If Lilypond is not installed in the expected location, the path can be specified as follows: `\usepackage[program=/path/to/executable]{lyluatex}` (line 6 in `mylilypond.sty`).

The setup assumes that a koma document class is used, such as `scrartcl`.

Custom fonts should be saved in a subfolder called **fonts** and invoked as follows: `\setmainfont[Path=fonts/]{fontname.otf}`
`\setmonofont[Path=fonts/,Scale=MatchLowercase]{fontname.otf}`
The 'scale' option can match the lower/upper case font, or accept a factor, i.e. 0.8

Graphics should be saved in a subfolder called **images**.

The commands and environments (re-)defined so far are:
- `\maketitle` – creates a title and author info on the first page
- `\maketitlepage` – creates a dedicated titlepage
- `\workscited` – creates a works cited list on a new page
- `\tableofcontentspage` – creates a table of contents on a new page
- `\plagiat` – creates a plagiarism statement
- `\mylilypond[#1 #2]` (#1 is the file(path) and #2 is the caption) – embeds musical examples with lilypond files
- block quotes are handled as follows:

    ```tex
      \begin{aquote}{\autocite[Pages]{citation.key}}
        A block quote goes in here,
        the attribution is placed intelligently
        either in the last line or the following, flushright.
      \end{aquote}
    ```
- figures are inserted as follows:

    ```tex
      \begin{figure}
        \centering
      	\includegraphics[width=\textwidth]{nameofgraphic.png}
      	\caption{My Caption}
      	\label{figure n}
      \end{figure}
    ```
- `\autocite` is assumed as the default for citations and is used as follows: `\autocite[Text before the citation, such as qtd. in][the pagerange]{citation.key}`

## A List of All Required Packages:
All packages are loaded via `custom-style.sty`, unless they require user input, such as babel, in which case they are loaded via `config.tex` – lyluatex being the obvious exemption.
### In `custom-style.sty`
- fontspec
- tgcursor
- ebgaramond
- nth
- microtype
- setspace
- geometry
- changepage
- graphicx (graphics should be saved in an images/-subfolder)
- hyperref
- cleveref
- caption

### In `config.tex`
- babel
- csquotes
- biblatex

### In `mylilypond.sty`
- lyluatex

## Sample Project

A project could have the following structure:

  ```tex
    .                     % your root directory
    |
    +-- config.tex
    +-- custom-style.sty
    +-- mylilypond.sty
    |
    +-- fonts             % your fonts
    |   +-- mymainfont.otf
    |   +-- mymonospacedfont.otf
    +-- images            % your images
    |   +-- image1.png
    |   +-- image2.png
    +-- music             % your music examples
    |   +-- musicexample1.ly
    |   +-- musicexample2.ly
    +-- content           % your actual text
    |   +-- introduction.tex
    |   +-- mainpart.tex
    |   +-- conclusion.tex
    |
    +-- sources.bib       % your bibliography
    +-- main.tex          % master document
  ```

The `main.tex` file could then look like this:

  ```tex
    \documentclass[a4paper]{scrarticle} % your document class

    \include{config}
    \usepackage{custom-style}

    \begin{document}
      \maketitlepage                    % if you want a full titlepage
      \tableofcontents                  % if you want a TOC

      \input{content/introduction}      % your body text
      \input{content/mainpart}
      \input{content/conclusion}

      \workscited                       % if you want a bibliography
      \plagiat                          % if you want a plagiarism statement
    \end{document}
  ```
## Credit
The `.gitignore` files for both TeX and Lilypond auxiliary files are copied from [Github's .gitignore repository](https://github.com/github/gitignore)
The `aquote` environment follows [this StackExchange answer](https://tex.stackexchange.com/a/13761)