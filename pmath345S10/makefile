SHELL = /bin/bash
COURSE = pmath345
TERM = S10
.PHONY: $(COURSE)-notes.tex
all: notes clean
pdf: notes
notes: $(COURSE)-notes.tex
	pdflatex -jobname $(COURSE)$(TERM)-notes $(COURSE)-notes.tex
	if grep "LaTeX Warning: There were undefined references." $(COURSE)$(TERM)-notes.log; then pdflatex -jobname $(COURSE)$(TERM)-notes $(COURSE)-notes.tex; fi
	if grep "LaTeX Warning: Label(s) may have changed. Rerun to get cross-references right." $(COURSE)$(TERM)-notes.log; then pdflatex -jobname $(COURSE)$(TERM)-notes $(COURSE)-notes.tex; fi
$(COURSE)-notes.tex:
	echo -e '\\documentclass{article}\n\\input $(COURSE)-preamble.tex\n\\begin{document}' > $(COURSE)-notes.tex
	shopt -s extglob
	for f in $(COURSE)-[0-9]*.tex; do date -d$${f:(-10):6} +'\date{%B %-d, %Y}%' >> $(COURSE)-notes.tex; echo -e "\\maketitle\n\\input $$f" >> $(COURSE)-notes.tex; done
	echo '\end{document}' >> $(COURSE)-notes.tex
clean:
	rm -f *.log *.aux $(COURSE)-notes.tex
clear: clean
	rm -f $(COURSE)$(TERM)-notes.pdf
