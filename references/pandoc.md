
## Getting Started

### Pandoc Usage

Syntax

```shell script
$ pandoc -s [source file] -o [output file]
```

## Pandoc examples

### LaTeX to MS Word {.col-span-2}

Simple .tex to .docx

```shell script
$ pandoc -s file.tex -o file.docx
```

.tex to .docx with default citations

```shell script
$ pandoc -s file.tex --citeproc --bibliography=bib_library.bib -o file.docx
```

.tex to .docx with specific citations

```shell script
$ pandoc -s file.tex --citeproc --bibliography=bib_library.bib --csl=apa.csl -o file.docx
```

Get `.csl` file from [here](https://github.com/citation-style-language/styles)

.tex to .docx with cross references

```shell script
$ pandoc -s file.tex --filter pandoc-crossref -o file.docx
```

Get the filter `pandoc-crossref` from [here](https://github.com/lierdakil/pandoc-crossref/releases)

## Also see {.cols-1}

- [pandoc examples](https://pandoc.org/demos.html)
