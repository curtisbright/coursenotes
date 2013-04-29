SHELL = /bin/bash
COURSE = pmath944
TERM = F09
.PHONY: $(COURSE)-notes.tex
all: notes clean
pdf: notes
notes: $(COURSE)-notes.tex
	latex $(COURSE)-notes.tex
	if grep "LaTeX Warning: There were undefined references." $(COURSE)-notes.log; then latex $(COURSE)-notes.tex; fi
	if grep "LaTeX Warning: Label(s) may have changed. Rerun to get cross-references right." $(COURSE)-notes.log; then latex $(COURSE)-notes.tex; fi
	dvipdfm -o $(COURSE)$(TERM)-notes.pdf $(COURSE)-notes.dvi
$(COURSE)-notes.tex:
	echo -e '\\documentclass{article}\n\\input $(COURSE)-preamble.tex\n\\begin{document}' > $(COURSE)-notes.tex
	shopt -s extglob
	for f in $(COURSE)-[0-9]*.tex; do date -d$${f:(-10):6} +'\date{%B %-d, %Y}%' >> $(COURSE)-notes.tex; echo -e "\\maketitle\n\\input $$f" >> $(COURSE)-notes.tex; done
	echo '\end{document}' >> $(COURSE)-notes.tex
clean:
	rm -f *.log *.aux $(COURSE)-notes.tex $(COURSE)-notes.dvi $(COURSE)-notes.ps
clear: clean
	rm -f $(COURSE)$(TERM)-notes.pdf
