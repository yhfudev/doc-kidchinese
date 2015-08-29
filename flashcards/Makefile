# use latex's option -jobname to control the compiling of multiple language text.
# Author: Yunhui Fu <yhfudev@gmail.com>
# License: GPL v3.0

#LANG=en zh tw
LANG=zh
SRC_PREFIX= \
    fc-ts300 \
    fc-gsxxs100 \
    fc-sanzijing1 \
    fc-sanzijing2 \
    fc-siwukuaidu1 \
    fc-siwukuaidu2 \
    fc-siwukuaidu3 \
    fc-siwukuaidu4 \
    fc-siwukuaidu5 \
    fc-siwukuaidu6 \
    $(NULL)

define SRC_FROM_PREFIX
	$(addsuffix .tex, $(foreach file, $(SRC_PREFIX), $(basename $(notdir $(file)))))
endef
SOURCES=$(SRC_FROM_PREFIX)

#define OBJ_FROM_SRC
	#$(addsuffix .o, $(foreach file, $(SOURCES), $(basename $(notdir $(file)))))
#endef
#OBJECTS=$(OBJ_FROM_SRC)

define OUTPREFIX_FROM_SRC
	$(foreach suffix, $(LANG), $(addsuffix .$(suffix), $(foreach file, $(SOURCES), $(basename $(notdir $(file))))))
endef
OUTPREFIXS=$(OUTPREFIX_FROM_SRC)

define PDF_FROM_PREFIX
	$(addsuffix .pdf, $(foreach file, $(OUTPREFIXS), $(notdir $(file))))
endef
OUTPDFS=$(PDF_FROM_PREFIX)

define LATEXTMP_FROM_PREFIX
	$(foreach suffix, log out aux, $(addsuffix .$(suffix), $(foreach file, $(SOURCES), $(basename $(notdir $(file))))))
endef
LATEXTMP=$(LATEXTMP_FROM_PREFIX)

DEFAULT: $(OUTPDFS)
#	@echo OUTPDFS=$(OUTPDFS)

$(OUTPDFS): $(OUTPREFIXS)

$(OUTPREFIXS): $(SOURCES) fc-setup.tex
	@touch $@
	xelatex -jobname lang-$(shell echo $@ | awk -F. '{print $$2 }') $(shell echo $@ | awk -F. '{print $$1 }')
	#bibtex lang-$(shell echo $@| awk -F. '{print $$2 }')
	#xelatex -jobname lang-$(shell echo $@ | awk -F. '{print $$2 }') $(shell echo $@ | awk -F. '{print $$1 }')
	xelatex -jobname lang-$(shell echo $@ | awk -F. '{print $$2 }') $(shell echo $@ | awk -F. '{print $$1 }')
	mv lang-$(shell echo $@ | awk -F. '{print $$2 }').pdf $@.pdf
	@echo ""

clean:
	@rm -f $(OUTPREFIXS) $(OUTPDFS) $(LATEXTMP) lang-*
