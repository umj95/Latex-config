# Latex-config
Personal LaTeX setup: style-file for packages, fonts, etc. and config-file for variables and custom title pages etc. to fit my whims and needs

The custom-style.sty file contains commonly loaded packages, the hyperref-setup, etc.

The config.tex-file contains all the variables for handing in an academic term paper, as well as setups for custom titlepage, anti-plagiarism declaration, works cited etc.

The commands (re-)defined so far are:
- `\maketitle` – creates a title and author info on the first page
- `\maketitlepage` – creates a dedicated titlepage
- `\workscited` – creates a works cited list on a new page
- `\tableofcontents` – creates a table of contents on a new page
- `\plagiat` – creates a plagiarism statement
- `\mylilypond[#1 #2]` (#1 is the file(path) and #2 is the caption) – embeds musical examples with lilypond files
