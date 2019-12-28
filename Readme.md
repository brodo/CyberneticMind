# Personal Knowledge Base
This documents lines out a vision for a personal knowledge base.

## Inspiration

- [David Allen - Getting Things Done](https://gettingthingsdone.com/)
- [Lion Kimbro - How to Make a Complete Map of Every Thought you Think](https://users.speakeasy.net/~lion/nb/html/)
- [Niklas Luhmann - Zettelkasten](https://niklas-luhmann-archiv.de/nachlass/zettelkasten)
- Ted Nelson - Hypertext
- [Semantic Note Taking System](Semantic Note Taking System)

## Use Case

I am interested in the Paper "A Plea for lean software." by Nicolas With. I have used the browser plugin to automatically download the paper and add it and some meta information to the system. I can view this information as a graph:
![Image of a graph created by importing a paper](./example1.svg)

Next, I read through the paper in the included PDF viewer. I find an interesting quote: 'Software expands to fill the available memory.'. I can mark the quote in the viewer and the systems automatically adds it to the graph:

![Image of a graph after adding a quote](./example2.svg)

The system allows me to link to specific positions in PDFs, text files and images.

Next, we want to find all quotes from Nicolas Wirth and view them in a Table. For that I define a view called quotes_by_autor that finds all quotes by any author:

```
quotes_by_autor AUTOR := QOUTE 'source' DOCUMENT & AUTOR 'is author of' DOCUMENT
```
(made up syntax)

I can call this view with any autor as a parameter. The result is a table with all the matching entries. The system includes a table viewer.

The system automatically generates BibTeX files which can be used later to write papers in LaTeX.

## User Interface
The user interface is made up of a REPL, a graph viewer and a table viewer. The REPL is aware of the current state of the graph and can operate easily on the visible nodes. The interface is optimized for keyboard use.

## Architecture
![Diagram of the overall architecture](./architecture.svg)

The system is made up of a number of applications which can be categorized into three parts. The data is stored in an RDF database (Triplestore). The GUI implemented as a Desktop App in Rust. It is scriptable using LISP. Collectors can be written in any language and are adding data to the RDF store.

## Transformers

A core component of the system is a __transformer__ that converts data from one format into another.
These can be connected to add new information to the system or generate views on existing information.i

Like edges in a knowledge graph they connect different data formats and sources.

### Example Setup

1. word list 
2. english word -> definition (as structured data)
3. definition -> flashcards
4. all flashcards -> list of flashcards due for review
