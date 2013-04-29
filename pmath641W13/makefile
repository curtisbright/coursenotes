SHELL = /bin/bash
COURSE = pmath641
TERM = W13
all: notes clean
pdf: notes
notes: $(COURSE)-notes.tex
	pdflatex -jobname $(COURSE)$(TERM)-notes $(COURSE)-notes.tex
$(COURSE)-notes.tex:
	echo -e '\\documentclass{article}\n\\input $(COURSE)-preamble.tex\n\\begin{document}' > $(COURSE)-notes.tex
	shopt -s extglob
	for f in $(COURSE)-[0-9]*.tex; do date -d$${f:(-10):6} +'\date{%B %-d, %Y}%' >> $(COURSE)-notes.tex; echo -e "\\maketitle\n\\input $$f" >> $(COURSE)-notes.tex; done
	echo '\end{document}' >> $(COURSE)-notes.tex
clean:
	rm -f $(COURSE)$(TERM)-notes.log $(COURSE)$(TERM)-notes.aux $(COURSE)-notes.tex
clear: clean
	rm -f $(COURSE)$(TERM)-notes.pdf
