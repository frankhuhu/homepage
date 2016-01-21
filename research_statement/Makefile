TEX      := latex
PDFTEX   := pdflatex
BIBTEX   := bibtex
RM       := rm -f
OPTIONS  = -o
PDFTEXOPTIONS = --interaction batchmode

DVI     = research_statement.dvi
TARGET  = research_statement.pdf
BIBSRC  = $(shell ls *.bib)
BIBFILE = $(shell ls *.bbl)
EPSES = # $(shell ls figs/*.eps)
AUTOGEN_PDFS = $(addsuffix .pdf, $(basename $(EPSES)))
LDIFF	= latexdiff
PAPERTEX = research_statement.tex
DIFFTEX	= diff.tex
LAST = last.tex


all: $(TARGET)


research_statement.pdf:  $(DVI) 
	clear
	echo Running $(PDFTEX)
	$(PDFTEX) $(PDFTEXOPTIONS) $(basename $(DVI));\


research_statement.dvi: $(AUTOGEN_PDFS) $(shell ls *.tex) 
	clear
	echo Running $(PDFTEX)
	echo $(basename $@) 
	$(PDFTEX) $(basename $@)
	clear
	echo Running $(BIBTEX);\
	$(BIBTEX) $(basename $@) ;\
	clear;\
	for i in 1 2; do\
	   echo Running $(PDFTEX);\
	   $(PDFTEX) $(basename $@) ;\
	done

figs/%.pdf : figs/%.eps
	cd figs/  && GS_OPTIONS=-dAutoRotatePages=/None epstopdf $*.eps 

pdfs: $(AUTOGEN_PDFS)

clean: 
	$(RM) $(TARGET_PDF) $(TARGET_PS)  $(DVI) $(BIBFILE) *.aux *.log *blg *~ semantic.cache $(basename $(TARGET)).out $(AUTOGEN_PDFS) .cache.*

