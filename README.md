# pubdomo
### the stupid assistant for displaying bibliographies

	Usage: pubdomo [options] file.bib
        --sort [TYPE]                Sort output by year/keywords/project/subject.
        --pubs DIR                   pubs directory (Default: ./pubs).
        --styles DIR                 CSL styles directory (Default: ./styles).
        --bibs DIR                   .bib files  directory (Default: ./bibs).
        --splitbib                   Split file.bib into multiple files stored into --bibs folder.
    -h, --help                       Display this screen

## main purpose
To take a list of publications (in BibTeX format), and thanks to
bibtex-ruby and citeproc-ruby, display the bibliography in
YAML, ready to be fed to a YAML-hungry display tool, such as
jekyll.

## dependencies
- Ruby
- bibtex-ruby
- citeproc-ruby (which needs Ruby >= v1.9.2)

## example
Input:

	@inproceedings{bergman_hpec07,
		author = "Keren Bergman and Luca P. Carloni",
		title = "On-Chip Photonic Communication for High-Performance Multi-Core Processors",
		month = sep,
		year = 2007,
		booktitle = "Proceedings of the Eleventh Annual Workshop on High Performance Embedded Computing (HPEC)",
		editor = {},
		pages = {},
		address = {Lexington, MA},
		publisher = {},
		note = {(Best paper award)},
		keywords = {networks-on-chip, photonics, optical communication},
		affiliation = {Columbia},
		entered = {Luca Carloni, 6/9/07}
	}

Output:

	[ omitting submenu and some bells and whistles ]
	publications
		- entry:
		  authors: "Keren Bergman and Luca P. Carloni"
		  title: "On-Chip Photonic Communication for High-Performance Multi-Core Processors"
		  venue: "in Proceedings of the Eleventh Annual Workshop on High Performance Embedded Computing (HPEC)"
		  details: "2007"
		  year: 2007
		  month: sep
		  mon: 9
		  keywords: networks-on-chip, photonics, optical communication
		  note: (Best paper award)
		  pdf: bergman_hpec07.pdf
		  bib: bergman_hpec07.bib

NB. Of course `$pubs/bergman_hpec07.pdf` and $bibs/bergman_hpec07.bib exist.

## sorting
Apart from the explicit sorting, second-level sorting is done by publication
date in descending order (more recent first)--in case two publications have
the same year/month, no guarantees wrt their ordering are provided. If the
month of a publication is not filled out in the BibTeX file, the publication
gets assigned month "0", ie it gets shown last (within its year's publications).

## formatting
The trick is to use CSL styles to generate each of the subfields (authors, title,
venue and details), one separate file for each of them.
