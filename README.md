# mdtopdf

[![GoDoc](https://godoc.org/github.com/mandolyte/mdtopdf?status.svg)](https://godoc.org/github.com/mandolyte/mdtopdf)

## Introduction: Markdown to PDF

This package depends on two other packages:

- The BlackFriday v2 parser to read the markdown source
- The `gofpdf` packace to generate the PDF

Both of the above are documented at Go Docs [http://godocs.org].

The tests included here are from the BlackFriday package.
See the "testdata" folder.
The tests create PDF files and thus while the tests may complete
without errors, visual inspection of the created PDF is the
only way to determine if the tests _really_ pass!

The tests create log files that trace the BlackFriday parser
callbacks. This is a valuable debug tool showing each callback
and data provided in each while the AST is presented.

## Supported Markdown

The supported elements of markdown are:

- Emphasized and strong text
- Headings 1-6
- Ordered and unordered lists
- Nested lists
- Images
- Tables (but see limitations below)
- Links
- Code blocks and backticked text

## Limitations and Known Issues

1. It is common for Markdown to include HTML. HTML is treated as a "code block". _There is no attempt to convert raw HTML to PDF._
2. Github-flavored Markdown permits strikethough using tildes. This is not supported at present by `gofpdf` as a font style.
3. The markdown link title, which would show when converted to HTML as hover-over text, is not supported. The generated PDF will show the actual URL that will be used if clicked, but this is a function of the PDF viewer.
4. Currently all levels of unordered lists use a dash for the bullet.
   This is a planned fix; [see here](https://github.com/mandolyte/mdtopdf/issues/1).
5. Definition lists are not supported (not sure that markdown supports them -- I need to research this)
6. The following text features may be tweaked: font, size, spacing, styile, fill color, and text color. These are exported and available via the `Styler` struct. Note that fill color only works if the text is ouput using CellFormat(). This is the case for: tables, codeblocks, and backticked text.
7. Tables are supported, but no attempt is made to ensure fit. You can, however, change the font size and spacing to make it smaller. See example

## Installation

To install the package, run the usual `go get`:

```
go get github.com/mandolyte/mdtopdf
```

## Quick start

In the `cmd` folder is an example using the package. It demonstrates
a number of features. The test PDF was created with this command:

```
go run convert.go -i test.md -o test.pdf
```
