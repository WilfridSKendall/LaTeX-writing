# ----------------------------------------------
# Makefile for latex package.


# ----------------------------------------------
# Shell:
SHELL := /bin/bash
WSKLIB := $(HOME)/lib
export PYTHONPATH=/home/wilfrid/lib/python
export DISPLAY=:0.0

# ----------------------------------------------
# Title:
title := WSKtracking

# ----------------------------------------------
# Utilities and flags:
ACROPRINT := "$(ACROREAD)" /p
SCP := /bin/scp
START := '/usr/bin/xdg-open'

# ----------------------------------------------
# Internal variables:
sourcefiles := Makefile VERSION $(title).dtx
targets := $(title).sty $(title).pdf

# ----------------------------------------------
# Special targets:
phonytargets := checkin clean virgin help gui products
.PHONY: $(phonytargets)
.SILENT: $(phonytargets)

# ----------------------------------------------
# Principal targets:
# ===================
# GUI STARTS HERE
package: $(title).sty

document: $(title).pdf ; $(START) $(title).pdf

# ----------------------------------------------
clean: ; -rm *.aux *.blg *.dvi *.glo *.hd *.idx *.ilg *.ind *.log *.loi *.out 

virgin: clean ; -rm README.txt $(title).sty $(title).pdf $(title).ins $(title).bbl $(title).toc

# ----------------------------------------------
# Checkin targets:
checkin: ; -git commit -a

# ===================
# GUI ENDS HERE
# ----------------------------------------------

# ----------------------------------------------
$(title).sty: $(title).dtx ; tex $(title).dtx
$(title).pdf: $(title).dtx VERSION.txt
	pdflatex $(title).dtx
	bibtex ${title}
	makeindex -s gind.ist $(title)
	pdflatex $(title).dtx
	pdflatex $(title).dtx

# ----------------------------------------------
# Automatic help:
.SILENT: products.txt
products.txt: Makefile
	echo "(targets)  " $(targets) | sed s\/^\/\\t\/ >> $@

# ----------------------------------------------
# Automatic help (textual):
help: products.txt ; $(PYTHON) "$(PYTHONPATH)/make/browser.py"

# ----------------------------------------------
# Automatic help (graphical):
gui: products.txt ; $(PYTHON) "$(PYTHONPATH)/make/browser.py" --gui &
