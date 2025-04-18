###############################################################################
## Makefile for Occitan--French
###############################################################################

LANG1=oci
LANG2=fra
PREFIX1=$(LANG1)-$(LANG2)
PREFIX2=$(LANG2)-$(LANG1)

VAR1=_gascon

BASENAME=apertium-$(PREFIX1)

# CHANGES : ici on indique que deux fichiers de règles seront à générer par le make
# l'un (biprefs.rlx) est pour les préférences du dico bilingue
# l'autre (genprefs.rlx) est généré à partir du fichier de règles du dico monolingue (oci.prefs.rlx.bin)

TARGETS_COMMON =		\
	$(PREFIX1).automorf.bin	\
	$(PREFIX1).prob		\
	$(PREFIX1).rlx.bin	\
	$(PREFIX1).autobil.bin	\
	$(PREFIX1).n_a_adv.autolex.bin	\
	$(PREFIX1).np.autolex.bin	\
	$(PREFIX1).v.autolex.bin	\
	$(PREFIX1).other.autolex.bin	\
	$(PREFIX1).autosep1.bin \
	$(PREFIX1).autosep2.bin \
	$(PREFIX2).autosep1.bin \
	$(PREFIX2).autosep2.bin \
	$(PREFIX1).autogen.bin	\
	$(PREFIX1).autopgen.bin	\
	$(PREFIX1).t1x.bin	\
	$(PREFIX1).t1x			\
	$(PREFIX1).t2x_temps.bin	\
	$(PREFIX1).t2ax.bin	\
	$(PREFIX1).t2ax2.bin	\
	$(PREFIX1).t2ax			\
	$(PREFIX1).t2ax2			\
	$(PREFIX1).t2bx.bin	\
	$(PREFIX1).t2bx			\
	$(PREFIX1).t2cx.bin	\
	$(PREFIX1).t2cx			\
	$(PREFIX1).t2dx.bin	\
	$(PREFIX1).t2ex.bin	\
	$(PREFIX1).t3x.bin	\
	$(PREFIX1).t4x.bin	\
	$(PREFIX1).t4x			\
	$(PREFIX2).automorf.bin	\
	$(PREFIX2).prob		\
	$(PREFIX2).rlx.bin	\
	$(PREFIX2).genprefs.rlx.bin	\
	$(PREFIX2).biprefs.rlx.bin	\
	$(PREFIX2)$(VAR1).genprefs.rlx.bin	\
	$(PREFIX2)$(VAR1).biprefs.rlx.bin	\
	$(PREFIX2).autobil.bin	\
	$(PREFIX2).n_a_adv.autolex.bin	\
	$(PREFIX2).np.autolex.bin	\
	$(PREFIX2).v.autolex.bin	\
	$(PREFIX2).other.autolex.bin	\
	$(PREFIX2).autogen.bin	\
	$(PREFIX2).autopgen.bin	\
	$(PREFIX2).t1x.bin	\
	$(PREFIX2).t1x			\
	$(PREFIX2).t2x.bin	\
	$(PREFIX2).t2x	\
	$(PREFIX2).t2x_ini.bin	\
	$(PREFIX2).t2x_bis.bin	\
	$(PREFIX2).t2x_bis	\
	$(PREFIX2).t2x_pas.bin	\
	$(PREFIX2).t2x_pro.bin	\
	$(PREFIX2).t3x.bin	\
	$(PREFIX2).t4x.bin


# This include defines goals for install-modes, .deps/.d and .mode files:
@ap_include@

###############################################################################
## Monolingual transducers
###############################################################################

# -------------------
# Occitan analysis:
# -------------------

$(PREFIX1).automorf.bin: $(AP_SRC1)/$(LANG1).automorf.bin $(PREFIX1).autobil.bin
	lt-trim $^ $@

# -------------------
# Occitan generation:
# ---------------------


$(PREFIX2).autogen.bin: $(AP_SRC1)/$(LANG1).autogen.bin
	cp $< $@

# -------------------
# French analysis:
# -------------------

$(PREFIX2).automorf.bin: $(AP_SRC2)/$(LANG2).automorf.bin $(PREFIX2).autobil.bin
	lt-trim $^ $@

# -------------------
# French generation:
# ---------------------


$(PREFIX1).autogen.bin: $(AP_SRC2)/$(LANG2).autogen.bin
	cp $< $@

###############################################################################
## Multiwords
###############################################################################

$(PREFIX1).autosep1.bin: $(BASENAME).$(PREFIX1).l1x
	lsx-comp -v "oci" lr $< $@

$(PREFIX1).autosep2.bin: $(BASENAME).$(PREFIX1).l2x
	lsx-comp -v "oci" lr $< $@

$(PREFIX2).autosep1.bin: $(BASENAME).$(PREFIX2).l1x
	lsx-comp -v "oci" lr $< $@

$(PREFIX2).autosep2.bin: $(BASENAME).$(PREFIX2).l2x
	lsx-comp -v "oci" lr $< $@


###############################################################################
## Tagger models
###############################################################################

$(PREFIX1).prob: $(AP_SRC1)/$(LANG1).prob
	cp $< $@


###############################################################################
## Disambiguation rules
###############################################################################

$(PREFIX1).rlx.bin: $(AP_SRC1)/apertium-$(LANG1).$(LANG1).rlx
	cg-comp $< $@

$(PREFIX2).rlx.bin: $(AP_SRC2)/apertium-$(LANG2).$(LANG2).rlx
	cg-comp $< $@

###############################################################################
## Bilingual dictionaries
###############################################################################

.deps/$(PREFIX2).dix: $(BASENAME).$(PREFIX1).dix .deps/.d
	xsltproc --stringparam alt $(LANG1) alt.xsl $(BASENAME).$(PREFIX1).dix >$@

$(PREFIX1).autobil.bin: .deps/$(PREFIX2).dix .deps/.d
	apertium-validate-dictionary $<
	lt-comp lr $< $@

$(PREFIX2).autobil.bin: .deps/$(PREFIX2).dix .deps/.d
	apertium-validate-dictionary $<
	lt-comp rl $< $@

###############################################################################
## Variant preferences
###############################################################################

# CHANGES : on compile le fichier de règles de préférences du dico bilingue

$(PREFIX2).biprefs.rlx.bin: $(BASENAME).$(PREFIX2).biprefs.rlx
	cg-comp $< $@

$(PREFIX2)$(VAR1).biprefs.rlx.bin: $(BASENAME).$(PREFIX2)$(VAR1).biprefs.rlx
	cg-comp $< $@

# CHANGES : on compile le fichier de règles de préférences du  dico monolingue

$(PREFIX2).genprefs.rlx.bin: $(AP_SRC1)/$(LANG1).prefs.rlx.bin
	cp $< $@

$(PREFIX2)$(VAR1).genprefs.rlx.bin: $(AP_SRC1)/$(LANG1)$(VAR1).prefs.rlx.bin
	cp $< $@

###############################################################################
## Lexical selection rules
###############################################################################

.deps/$(PREFIX1).n_a_adv.lrx: $(BASENAME).$(PREFIX1).n_a_adv.lrx .deps/.d
	apertium-filter-rules oci $< >$@

.deps/$(PREFIX1).np.lrx: $(BASENAME).$(PREFIX1).np.lrx .deps/.d
	apertium-filter-rules oci $< >$@

.deps/$(PREFIX1).v.lrx: $(BASENAME).$(PREFIX1).v.lrx .deps/.d
	apertium-filter-rules oci $< >$@

.deps/$(PREFIX1).other.lrx: $(BASENAME).$(PREFIX1).other.lrx .deps/.d
	apertium-filter-rules oci $< >$@

.deps/$(PREFIX2).n_a_adv.lrx: $(BASENAME).$(PREFIX2).n_a_adv.lrx .deps/.d
	apertium-filter-rules oci $< >$@

.deps/$(PREFIX2).np.lrx: $(BASENAME).$(PREFIX2).np.lrx .deps/.d
	apertium-filter-rules oci $< >$@

.deps/$(PREFIX2).v.lrx: $(BASENAME).$(PREFIX2).v.lrx .deps/.d
	apertium-filter-rules oci $< >$@

.deps/$(PREFIX2).other.lrx: $(BASENAME).$(PREFIX2).other.lrx .deps/.d
	apertium-filter-rules oci $< >$@

$(PREFIX1).n_a_adv.autolex.bin: .deps/$(PREFIX1).n_a_adv.lrx
	apertium-validate-lrx $<
	lrx-comp $< $@

$(PREFIX1).np.autolex.bin: .deps/$(PREFIX1).np.lrx
	apertium-validate-lrx $<
	lrx-comp $< $@

$(PREFIX1).v.autolex.bin: .deps/$(PREFIX1).v.lrx
	apertium-validate-lrx $<
	lrx-comp $< $@

$(PREFIX1).other.autolex.bin: .deps/$(PREFIX1).other.lrx
	apertium-validate-lrx $<
	lrx-comp $< $@

$(PREFIX2).n_a_adv.autolex.bin: .deps/$(PREFIX2).n_a_adv.lrx
	apertium-validate-lrx $<
	lrx-comp $< $@

$(PREFIX2).np.autolex.bin: .deps/$(PREFIX2).np.lrx
	apertium-validate-lrx $<
	lrx-comp $< $@

$(PREFIX2).v.autolex.bin: .deps/$(PREFIX2).v.lrx
	apertium-validate-lrx $<
	lrx-comp $< $@

$(PREFIX2).other.autolex.bin: .deps/$(PREFIX2).other.lrx
	apertium-validate-lrx $<
	lrx-comp $< $@

###############################################################################
## Structural transfer rules
###############################################################################

$(PREFIX1).t1x: $(BASENAME).$(PREFIX1).t1x
	apertium-filter-rules oci $(BASENAME).$(PREFIX1).t1x >$@

$(PREFIX1).t1x.bin: $(PREFIX1).t1x
	apertium-validate-transfer $<
	apertium-preprocess-transfer $< $@

$(PREFIX1).t2x_temps.bin: $(BASENAME).$(PREFIX1).t2x_temps
	apertium-validate-interchunk $<
	apertium-preprocess-transfer $< $@

$(PREFIX1).t2ax: $(BASENAME).$(PREFIX1).t2ax
	apertium-filter-rules oci $(BASENAME).$(PREFIX1).t2ax >$@

$(PREFIX1).t2ax.bin: $(PREFIX1).t2ax
	apertium-validate-interchunk $<
	apertium-preprocess-transfer $< $@

$(PREFIX1).t2ax2: $(BASENAME).$(PREFIX1).t2ax2
	apertium-filter-rules oci $(BASENAME).$(PREFIX1).t2ax2 >$@

$(PREFIX1).t2ax2.bin: $(PREFIX1).t2ax2
	apertium-validate-interchunk $<
	apertium-preprocess-transfer $< $@

$(PREFIX1).t2bx: $(BASENAME).$(PREFIX1).t2bx
	apertium-filter-rules oci $(BASENAME).$(PREFIX1).t2bx >$@

$(PREFIX1).t2bx.bin: $(PREFIX1).t2bx
	apertium-validate-interchunk $<
	apertium-preprocess-transfer $< $@

$(PREFIX1).t2cx: $(BASENAME).$(PREFIX1).t2cx
	apertium-filter-rules oci $(BASENAME).$(PREFIX1).t2cx >$@

$(PREFIX1).t2cx.bin: $(PREFIX1).t2cx
	apertium-validate-interchunk $<
	apertium-preprocess-transfer $< $@

$(PREFIX1).t2dx.bin: $(BASENAME).$(PREFIX1).t2dx
	apertium-validate-interchunk $<
	apertium-preprocess-transfer $< $@

$(PREFIX1).t2ex.bin: $(BASENAME).$(PREFIX1).t2ex
	apertium-validate-interchunk $<
	apertium-preprocess-transfer $< $@

$(PREFIX1).t3x.bin: $(BASENAME).$(PREFIX1).t3x
	apertium-validate-postchunk $<
	apertium-preprocess-transfer $< $@

$(PREFIX1).t4x: $(BASENAME).$(PREFIX1).t4x
	apertium-filter-rules oci $(BASENAME).$(PREFIX1).t4x >$@

$(PREFIX1).t4x.bin: $(PREFIX1).t4x
	apertium-validate-transfer $<
	apertium-preprocess-transfer $< $@

$(PREFIX2).t1x: $(BASENAME).$(PREFIX2).t1x
	apertium-filter-rules oci $(BASENAME).$(PREFIX2).t1x >$@

$(PREFIX2).t1x.bin: $(PREFIX2).t1x
	apertium-validate-transfer $<
	apertium-preprocess-transfer $< $@

$(PREFIX2).t2x: $(BASENAME).$(PREFIX2).t2x
	apertium-filter-rules oci $(BASENAME).$(PREFIX2).t2x >$@

$(PREFIX2).t2x.bin: $(PREFIX2).t2x
	apertium-validate-interchunk $<
	apertium-preprocess-transfer $< $@

$(PREFIX2).t2x_bis: $(BASENAME).$(PREFIX2).t2x_bis
	apertium-filter-rules oci $(BASENAME).$(PREFIX2).t2x_bis >$@

$(PREFIX2).t2x_bis.bin: $(PREFIX2).t2x_bis
	apertium-validate-interchunk $<
	apertium-preprocess-transfer $< $@

$(PREFIX2).t2x_ini.bin: $(BASENAME).$(PREFIX2).t2x_ini
	apertium-validate-interchunk $<
	apertium-preprocess-transfer $< $@

$(PREFIX2).t2x_pas.bin: $(BASENAME).$(PREFIX2).t2x_pas
	apertium-validate-interchunk $<
	apertium-preprocess-transfer $< $@

$(PREFIX2).t2x_pro.bin: $(BASENAME).$(PREFIX2).t2x_pro
	apertium-validate-interchunk $<
	apertium-preprocess-transfer $< $@

$(PREFIX2).t3x.bin: $(BASENAME).$(PREFIX2).t3x
	apertium-validate-postchunk $<
	apertium-preprocess-transfer $< $@

$(PREFIX2).t4x.bin: $(BASENAME).$(PREFIX2).t4x
	apertium-validate-transfer $<
	apertium-preprocess-transfer $< $@

###############################################################################
## Postgeneration dictionaries
###############################################################################

$(PREFIX1).autopgen.bin: $(AP_SRC2)/$(LANG2).autopgen.bin
	cp $< $@

$(PREFIX2).autopgen.bin: $(AP_SRC1)/$(LANG1).autopgen.bin
	cp $< $@

###############################################################################
## Distribution
###############################################################################

EXTRA_DIST=					\
		$(BASENAME).$(PREFIX1).dix	\
		$(BASENAME).$(PREFIX1).l1x	\
		$(BASENAME).$(PREFIX1).l2x	\
		$(BASENAME).$(PREFIX2).l1x	\
		$(BASENAME).$(PREFIX2).l2x	\
		$(BASENAME).$(PREFIX1).lrx	\
		$(BASENAME).$(PREFIX2).lrx	\
		$(BASENAME).$(PREFIX1).t1x	\
		$(BASENAME).$(PREFIX1).t2x_temps	\
		$(BASENAME).$(PREFIX1).t2ax	\
		$(BASENAME).$(PREFIX1).t2ax2	\
		$(BASENAME).$(PREFIX1).t2bx	\
		$(BASENAME).$(PREFIX1).t2cx	\
		$(BASENAME).$(PREFIX1).t2dx	\
		$(BASENAME).$(PREFIX1).t2ex	\
		$(BASENAME).$(PREFIX1).t3x	\
		$(BASENAME).$(PREFIX1).t4x	\
		$(BASENAME).$(PREFIX2).t1x	\
		$(BASENAME).$(PREFIX2).t2x	\
		$(BASENAME).$(PREFIX2).t2x_ini	\
		$(BASENAME).$(PREFIX2).t2x_bis	\
		$(BASENAME).$(PREFIX2).t2x_pas	\
		$(BASENAME).$(PREFIX2).t2x_pro	\
		$(BASENAME).$(PREFIX2).t2x_supersn	\
		$(BASENAME).$(PREFIX2).t2x_enon	\
		$(BASENAME).$(PREFIX2).t3x	\
		$(BASENAME).$(PREFIX2).t4x	\
		modes.xml \
		alt.xsl

###############################################################################
## Installation
###############################################################################

apertium_oci_fradir=$(prefix)/share/apertium/$(BASENAME)/

# Files which should be installed to $(prefix)/share/apertium/$(BASENAME)/:
apertium_oci_fra_DATA=	\
	$(TARGETS_COMMON)				\
	$(BASENAME).$(PREFIX1).t1x			\
	$(BASENAME).$(PREFIX1).t2x_temps			\
	$(BASENAME).$(PREFIX1).t2ax			\
	$(BASENAME).$(PREFIX1).t2ax2			\
	$(BASENAME).$(PREFIX1).t2bx			\
	$(BASENAME).$(PREFIX1).t2cx			\
	$(BASENAME).$(PREFIX1).t2dx			\
	$(BASENAME).$(PREFIX1).t2ex			\
	$(BASENAME).$(PREFIX1).t3x			\
	$(BASENAME).$(PREFIX1).t4x			\
	$(BASENAME).$(PREFIX2).t1x			\
	$(BASENAME).$(PREFIX2).t2x			\
	$(BASENAME).$(PREFIX2).t2x_ini			\
	$(BASENAME).$(PREFIX2).t2x_bis			\
	$(BASENAME).$(PREFIX2).t2x_pas			\
	$(BASENAME).$(PREFIX2).t2x_pro			\
	$(BASENAME).$(PREFIX2).t2x_supersn			\
	$(BASENAME).$(PREFIX2).t2x_enon			\
	$(BASENAME).$(PREFIX2).t3x			\
	$(BASENAME).$(PREFIX2).t4x

# All modes are created by the same goal, listing several will just give problems with make -j2
noinst_DATA=modes/$(PREFIX1).mode

install-data-local: install-modes

###############################################################################
## Cleanup
###############################################################################

CLEANFILES = $(TARGETS_COMMON)
clean-local:
	-rm -rf .deps modes

###############################################################################
## Test
###############################################################################

test: all
	apertium-regtest test
