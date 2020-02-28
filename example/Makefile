.PHONY: clean all

COLBIBTEX=../colbibtex

all: example_mcite.pdf example_colbibtex.pdf example_mcitemode.pdf example_colbibtex_invalid.pdf

clean:
	@rm -f *.aux *.fdb_latexmk *.fls *.log *~ *.bbl *.blg *.out flycheck_*

example_mcite.pdf: example_mcite.tex example.bib
	pdflatex example_mcite
	bibtex example_mcite
	pdflatex example_mcite
	pdflatex example_mcite

example_colbibtex.pdf: example_colbibtex.tex example.bib
	pdflatex example_colbibtex
	${COLBIBTEX} example_colbibtex
	pdflatex example_colbibtex
	pdflatex example_colbibtex

example_colbibtex_invalid.pdf: example_colbibtex_invalid.tex example.bib
	pdflatex example_colbibtex_invalid
	${COLBIBTEX} example_colbibtex_invalid
	pdflatex example_colbibtex_invalid
	pdflatex example_colbibtex_invalid

example_mcitemode.pdf: example_mcitemode.tex example.bib
	pdflatex example_mcitemode
	${COLBIBTEX} example_mcitemode
	pdflatex example_mcitemode
	pdflatex example_mcitemode

latexmk:
	latexmk example_mcite
	latexmk -e "\$$bibtex='${COLBIBTEX}'" example_colbibtex
	latexmk -e "\$$bibtex='${COLBIBTEX}'" example_mcitemode
