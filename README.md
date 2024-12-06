# pandoc-tex-numbering
This is an all-in-one pandoc filter especially for LaTeX files to keep **numbering, hyperlinks, caption prefixs and cross references in (maybe multi-line) equations, figures, and tables**.

With `pandoc-tex-numbering`, you can convert your LaTeX source codes to any format pandoc supported, especially `.docx`, while **keep all your auto-numberings and cross references**. 

`pandoc-tex-numbering` even supports **multi-line environments** in LaTeX math block such as `align`, `cases` etc.

# Installation

1. Install `pandoc` and `python3` if you haven't.
2. Install python package `panflute` and `pylatexenc` if you haven't:
    ```bash
    pip install panflute pylatexenc
    ```
3. Download the `pandoc-tex-numbering.py` and put it in your PATH or in the same directory as your LaTeX source file.

# Usage

Take `.docx` as an example:

```bash
pandoc --filter pandoc-tex-numbering.py input.tex -o output.docx
```

# Details

## Figures and Tables

All the figures and tables are supported. All references to figures and tables are replaced by their numbers, and all the captions are added prefixs such as "Figure 1.1: ".

You can determine the prefix of figures and tables by changing the variables `figure_prefix` and `table_prefix` in the metadata, default values are "Figure" and "Table" respectively.

## Equations

Single-line equations are auto-numbered. At the end of every equation, a label is added such as `(1.1)`.

Multi-line equations are:

- numbered for each line if there's at least one `\label{}` command inside the environment.
- numbered for the whole block if there's no `\label{}` command inside the environment.

Therefore, if you want to reference a multi-line equation as a whole, you should put a `\label{}` command outside the environment. While if you want to reference a specific line, you should put a `\label{}` command at the corresponding line.

For example, in the following code:
    
```latex
\begin{equation}
\begin{align}
    a &= b \label{eq:1} \\
    c &= d \label{eq:2}
\end{align}
\end{equation}
```

The filter will numbering the first line as (1.1) and the second line as (1.2). While in the following code:

```latex
\begin{equation}
\begin{align}
    a &= b \\
    c &= d
\end{align}
\label{eq:1}
\end{equation}
```

The filter will numbering the whole block as (1.1).

# Examples

With the testing file `testing_data/test.tex`, you can run:

```bash
pandoc --filter pandoc-tex-numbering.py testing_data/test.tex -o testing_data/test.docx
```

The results are shown as follows:

![alt text](https://github.com/fncokg/pandoc-tex-numbering/blob/main/images/output-page1.jpg?raw=true)
![alt text](https://github.com/fncokg/pandoc-tex-numbering/blob/main/images/output-page2.jpg?raw=true)