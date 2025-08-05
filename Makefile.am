###############################################################################
## Makefile for Occitan--French
###############################################################################

LANG1=oci
LANG1G=oci_gascon
LANG1L=oci_lang
LANG2=fra

PREFIX1=$(LANG1)-$(LANG2)
PREFIX1G=$(LANG1G)-$(LANG2)
PREFIX1L=$(LANG1L)-$(LANG2)

PREFIX2=$(LANG2)-$(LANG1)
PREFIX2G=$(LANG2)-$(LANG1G)
PREFIX2L=$(LANG2)-$(LANG1L)

BASENAME=apertium-$(PREFIX1)

# CHANGES : ici on indique que deux fichiers de règles seront à générer par le make
# l'un (biprefs.rlx) est pour les préférences du dico bilingue
# l'autre (genprefs.rlx) est généré à partir du fichier de règles du dico monolingue (oci.prefs.rlx.bin)

TARGETS_COMMON =		\
	bin/$(PREFIX1).automorf.bin	\
	bin/$(PREFIX1).prob		\
	bin/$(PREFIX1).rlx.bin	\
	bin/$(PREFIX1).autobil.bin	\
	bin/$(PREFIX1).n_a_adv.autolex.bin	\
	bin/$(PREFIX1).np.autolex.bin	\
	bin/$(PREFIX1).v.autolex.bin	\
	bin/$(PREFIX1).other.autolex.bin	\
	bin/$(PREFIX1).autosep1.bin \
	bin/$(PREFIX1G).autosep1.bin \
	bin/$(PREFIX1L).autosep1.bin \
	bin/$(PREFIX1).autosep2.bin \
	bin/$(PREFIX1G).autosep2.bin \
	bin/$(PREFIX1L).autosep2.bin \
	bin/$(PREFIX2).autosep1.bin \
	bin/$(PREFIX2G).autosep1.bin \
	bin/$(PREFIX2L).autosep1.bin \
	bin/$(PREFIX2).autosep2.bin \
	bin/$(PREFIX2G).autosep2.bin \
	bin/$(PREFIX2L).autosep2.bin \
	bin/$(PREFIX1).autogen.bin	\
	bin/$(PREFIX1).autopgen.bin	\
	bin/$(PREFIX1).t1x.bin	\
	build/$(PREFIX1).t1x			\
	bin/$(PREFIX1G).t1x.bin	\
	build/$(PREFIX1G).t1x			\
	bin/$(PREFIX1).t2x_temps.bin	\
	bin/$(PREFIX1).t2ax.bin	\
	build/$(PREFIX1).t2ax			\
	bin/$(PREFIX1G).t2ax.bin	\
	build/$(PREFIX1G).t2ax			\
	bin/$(PREFIX1L).t2ax.bin	\
	build/$(PREFIX1L).t2ax			\
	bin/$(PREFIX1).t2ax2.bin	\
	build/$(PREFIX1).t2ax2			\
	bin/$(PREFIX1G).t2ax2.bin	\
	build/$(PREFIX1G).t2ax2			\
	bin/$(PREFIX1L).t2ax2.bin	\
	build/$(PREFIX1L).t2ax2			\
	bin/$(PREFIX1).t2bx.bin	\
	build/$(PREFIX1).t2bx			\
	bin/$(PREFIX1G).t2bx.bin	\
	build/$(PREFIX1G).t2bx			\
	bin/$(PREFIX1L).t2bx.bin	\
	build/$(PREFIX1L).t2bx			\
	bin/$(PREFIX1).t2cx.bin	\
	build/$(PREFIX1).t2cx			\
	bin/$(PREFIX1G).t2cx.bin	\
	build/$(PREFIX1G).t2cx			\
	bin/$(PREFIX1L).t2cx.bin	\
	build/$(PREFIX1L).t2cx			\
	bin/$(PREFIX1).t2dx.bin	\
	bin/$(PREFIX1).t2ex.bin	\
	bin/$(PREFIX1).t3x.bin	\
	bin/$(PREFIX1).t4x.bin	\
	build/$(PREFIX1).t4x			\
	bin/$(PREFIX2).automorf.bin	\
	bin/$(PREFIX2).prob		\
	bin/$(PREFIX2).rlx.bin	\
	bin/$(PREFIX2).genprefs.rlx.bin	\
	bin/$(PREFIX2).biprefs.rlx.bin	\
	bin/$(PREFIX2G).genprefs.rlx.bin	\
	bin/$(PREFIX2G).biprefs.rlx.bin	\
	bin/$(PREFIX2).autobil.bin	\
	bin/$(PREFIX2).n_a_adv.autolex.bin	\
	bin/$(PREFIX2G).n_a_adv.autolex.bin	\
	bin/$(PREFIX2L).n_a_adv.autolex.bin	\
	bin/$(PREFIX2).np.autolex.bin	\
	bin/$(PREFIX2G).np.autolex.bin	\
	bin/$(PREFIX2L).np.autolex.bin	\
	bin/$(PREFIX2).v.autolex.bin	\
	bin/$(PREFIX2).other.autolex.bin	\
	bin/$(PREFIX2G).other.autolex.bin	\
	bin/$(PREFIX2L).other.autolex.bin	\
	bin/$(PREFIX2).autogen.bin	\
	bin/$(PREFIX2).autopgen.bin	\
	bin/$(PREFIX2).t1x.bin	\
	build/$(PREFIX2).t1x			\
	bin/$(PREFIX2G).t1x.bin	\
	build/$(PREFIX2G).t1x			\
	bin/$(PREFIX2).t2x.bin	\
	build/$(PREFIX2).t2x	\
	bin/$(PREFIX2G).t2x.bin	\
	build/$(PREFIX2G).t2x	\
	bin/$(PREFIX2L).t2x.bin	\
	build/$(PREFIX2L).t2x	\
	bin/$(PREFIX2).t2x_ini.bin	\
	bin/$(PREFIX2).t2x_bis.bin	\
	build/$(PREFIX2).t2x_bis	\
	bin/$(PREFIX2G).t2x_bis.bin	\
	build/$(PREFIX2G).t2x_bis	\
	bin/$(PREFIX2L).t2x_bis.bin	\
	build/$(PREFIX2L).t2x_bis	\
	bin/$(PREFIX2).t2x_pas.bin	\
	bin/$(PREFIX2).t2x_pro.bin	\
	bin/$(PREFIX2).t3x.bin	\
	bin/$(PREFIX2).t4x.bin


# This include defines goals for install-modes, .deps/.d and .mode files:
@ap_include@

###############################################################################
## Monolingual transducers
###############################################################################

# -------------------
# Occitan analysis:
# -------------------

bin/$(PREFIX1).automorf.bin: $(AP_SRC1)/$(LANG1).automorf.bin bin/$(PREFIX1).autobil.bin
	lt-trim $^ $@

# -------------------
# Occitan generation:
# ---------------------

bin/$(PREFIX2).autogen.bin: $(AP_SRC1)/$(LANG1).autogen.bin
	cp $< $@

# -------------------
# French analysis:
# -------------------

bin/$(PREFIX2).automorf.bin: $(AP_SRC2)/$(LANG2).automorf.bin bin/$(PREFIX2).autobil.bin
	lt-trim $^ $@

# -------------------
# French generation:
# ---------------------

bin/$(PREFIX1).autogen.bin: $(AP_SRC2)/$(LANG2).autogen.bin
	cp $< $@

###############################################################################
## Multiwords
###############################################################################

bin/$(PREFIX1).autosep1.bin: src/multiwords/$(BASENAME).$(PREFIX1).l1x
	lsx-comp -v "oci" lr $< $@

bin/$(PREFIX1G).autosep1.bin: src/multiwords/$(BASENAME).$(PREFIX1G).l1x
	lsx-comp -v "oci" lr $< $@

bin/$(PREFIX1L).autosep1.bin: src/multiwords/$(BASENAME).$(PREFIX1L).l1x
	lsx-comp -v "oci" lr $< $@

bin/$(PREFIX1).autosep2.bin: src/multiwords/$(BASENAME).$(PREFIX1).l2x
	lsx-comp -v "oci" lr $< $@

bin/$(PREFIX1G).autosep2.bin: src/multiwords/$(BASENAME).$(PREFIX1G).l2x
	lsx-comp -v "oci" lr $< $@

bin/$(PREFIX1L).autosep2.bin: src/multiwords/$(BASENAME).$(PREFIX1L).l2x
	lsx-comp -v "oci" lr $< $@	

bin/$(PREFIX2).autosep1.bin: src/multiwords/$(BASENAME).$(PREFIX2).l1x
	lsx-comp -v "oci" lr $< $@

bin/$(PREFIX2G).autosep1.bin: src/multiwords/$(BASENAME).$(PREFIX2G).l1x
	lsx-comp -v "oci" lr $< $@

bin/$(PREFIX2L).autosep1.bin: src/multiwords/$(BASENAME).$(PREFIX2L).l1x
	lsx-comp -v "oci" lr $< $@

bin/$(PREFIX2).autosep2.bin: src/multiwords/$(BASENAME).$(PREFIX2).l2x
	lsx-comp -v "oci" lr $< $@

bin/$(PREFIX2G).autosep2.bin: src/multiwords/$(BASENAME).$(PREFIX2G).l2x
	lsx-comp -v "oci" lr $< $@

bin/$(PREFIX2L).autosep2.bin: src/multiwords/$(BASENAME).$(PREFIX2L).l2x
	lsx-comp -v "oci" lr $< $@


###############################################################################
## Tagger models
###############################################################################

bin/$(PREFIX1).prob: $(AP_SRC1)/$(LANG1).prob
	cp $< $@

bin/$(PREFIX2).prob: $(AP_SRC2)/$(LANG2).prob
	cp $< $@

###############################################################################
## Disambiguation rules
###############################################################################

bin/$(PREFIX1).rlx.bin: $(AP_SRC1)/apertium-$(LANG1).$(LANG1).rlx
	cg-comp $< $@

bin/$(PREFIX2).rlx.bin: $(AP_SRC2)/apertium-$(LANG2).$(LANG2).rlx
	cg-comp $< $@

###############################################################################
## Bilingual dictionaries
###############################################################################

.deps/$(PREFIX2).dix: src/dictionaries/$(BASENAME).$(PREFIX1).dix .deps/.d
	xsltproc --stringparam alt $(LANG1) alt.xsl src/dictionaries/$(BASENAME).$(PREFIX1).dix >$@

bin/$(PREFIX1).autobil.bin: .deps/$(PREFIX2).dix .deps/.d
	apertium-validate-dictionary $<
	lt-comp lr $< $@

bin/$(PREFIX2).autobil.bin: .deps/$(PREFIX2).dix .deps/.d
	apertium-validate-dictionary $<
	lt-comp rl $< $@

###############################################################################
## Variant preferences
###############################################################################

# CHANGES : on compile le fichier de règles de préférences du dico bilingue

bin/$(PREFIX2).biprefs.rlx.bin: src/preferences/$(BASENAME).$(PREFIX2).biprefs.rlx
	cg-comp $< $@

bin/$(PREFIX2G).biprefs.rlx.bin: src/preferences/$(BASENAME).$(PREFIX2G).biprefs.rlx
	cg-comp $< $@

# CHANGES : on compile le fichier de règles de préférences du  dico monolingue

bin/$(PREFIX2).genprefs.rlx.bin: $(AP_SRC1)/$(LANG1).prefs.rlx.bin
	cp $< $@

bin/$(PREFIX2G).genprefs.rlx.bin: $(AP_SRC1)/$(LANG1G).prefs.rlx.bin
	cp $< $@

###############################################################################
## Lexical selection rules
###############################################################################

.deps/$(PREFIX1).n_a_adv.lrx: src/lexical-selection/$(BASENAME).$(PREFIX1).n_a_adv.lrx .deps/.d
	apertium-filter-rules oci $< >$@

.deps/$(PREFIX1).np.lrx: src/lexical-selection/$(BASENAME).$(PREFIX1).np.lrx .deps/.d
	apertium-filter-rules oci $< >$@

.deps/$(PREFIX1).v.lrx: src/lexical-selection/$(BASENAME).$(PREFIX1).v.lrx .deps/.d
	apertium-filter-rules oci $< >$@

.deps/$(PREFIX1).other.lrx: src/lexical-selection/$(BASENAME).$(PREFIX1).other.lrx .deps/.d
	apertium-filter-rules oci $< >$@

.deps/$(PREFIX2).n_a_adv.lrx: src/lexical-selection/$(BASENAME).$(PREFIX2).n_a_adv.lrx .deps/.d
	apertium-filter-rules oci $< >$@

.deps/$(PREFIX2G).n_a_adv.lrx: src/lexical-selection/gascon/$(BASENAME).$(PREFIX2G).n_a_adv.lrx .deps/.d
	apertium-filter-rules oci $< >$@

.deps/$(PREFIX2L).n_a_adv.lrx: src/lexical-selection/lengadocian/$(BASENAME).$(PREFIX2L).n_a_adv.lrx .deps/.d
	apertium-filter-rules oci $< >$@

.deps/$(PREFIX2).np.lrx: src/lexical-selection/$(BASENAME).$(PREFIX2).np.lrx .deps/.d
	apertium-filter-rules oci $< >$@

.deps/$(PREFIX2G).np.lrx: src/lexical-selection/gascon/$(BASENAME).$(PREFIX2G).np.lrx .deps/.d
	apertium-filter-rules oci $< >$@

.deps/$(PREFIX2L).np.lrx: src/lexical-selection/lengadocian/$(BASENAME).$(PREFIX2L).np.lrx .deps/.d
	apertium-filter-rules oci $< >$@


.deps/$(PREFIX2).v.lrx: src/lexical-selection/$(BASENAME).$(PREFIX2).v.lrx .deps/.d
	apertium-filter-rules oci $< >$@

.deps/$(PREFIX2).other.lrx: src/lexical-selection/$(BASENAME).$(PREFIX2).other.lrx .deps/.d
	apertium-filter-rules oci $< >$@

.deps/$(PREFIX2G).other.lrx: src/lexical-selection/gascon/$(BASENAME).$(PREFIX2G).other.lrx .deps/.d
	apertium-filter-rules oci $< >$@

.deps/$(PREFIX2L).other.lrx: src/lexical-selection/lengadocian/$(BASENAME).$(PREFIX2L).other.lrx .deps/.d
	apertium-filter-rules oci $< >$@

bin/$(PREFIX1).n_a_adv.autolex.bin: .deps/$(PREFIX1).n_a_adv.lrx
	apertium-validate-lrx $<
	lrx-comp $< $@

bin/$(PREFIX1).np.autolex.bin: .deps/$(PREFIX1).np.lrx
	apertium-validate-lrx $<
	lrx-comp $< $@

bin/$(PREFIX1).v.autolex.bin: .deps/$(PREFIX1).v.lrx
	apertium-validate-lrx $<
	lrx-comp $< $@

bin/$(PREFIX1).other.autolex.bin: .deps/$(PREFIX1).other.lrx
	apertium-validate-lrx $<
	lrx-comp $< $@

bin/$(PREFIX2).n_a_adv.autolex.bin: .deps/$(PREFIX2).n_a_adv.lrx
	apertium-validate-lrx $<
	lrx-comp $< $@

bin/$(PREFIX2G).n_a_adv.autolex.bin: .deps/$(PREFIX2G).n_a_adv.lrx
	apertium-validate-lrx $<
	lrx-comp $< $@

bin/$(PREFIX2L).n_a_adv.autolex.bin: .deps/$(PREFIX2L).n_a_adv.lrx
	apertium-validate-lrx $<
	lrx-comp $< $@

bin/$(PREFIX2).np.autolex.bin: .deps/$(PREFIX2).np.lrx
	apertium-validate-lrx $<
	lrx-comp $< $@

bin/$(PREFIX2G).np.autolex.bin: .deps/$(PREFIX2G).np.lrx
	apertium-validate-lrx $<
	lrx-comp $< $@

bin/$(PREFIX2L).np.autolex.bin: .deps/$(PREFIX2L).np.lrx
	apertium-validate-lrx $<
	lrx-comp $< $@

bin/$(PREFIX2).v.autolex.bin: .deps/$(PREFIX2).v.lrx
	apertium-validate-lrx $<
	lrx-comp $< $@

bin/$(PREFIX2).other.autolex.bin: .deps/$(PREFIX2).other.lrx
	apertium-validate-lrx $<
	lrx-comp $< $@

bin/$(PREFIX2G).other.autolex.bin: .deps/$(PREFIX2G).other.lrx
	apertium-validate-lrx $<
	lrx-comp $< $@

bin/$(PREFIX2L).other.autolex.bin: .deps/$(PREFIX2L).other.lrx
	apertium-validate-lrx $<
	lrx-comp $< $@

###############################################################################
## Structural transfer rules
###############################################################################

build/$(PREFIX1).t1x: src/transfer/chunkers/$(BASENAME).$(PREFIX1).t1x
	apertium-filter-rules oci src/transfer/chunkers/$(BASENAME).$(PREFIX1).t1x >$@

bin/$(PREFIX1).t1x.bin: build/$(PREFIX1).t1x
	apertium-validate-transfer $<
	apertium-preprocess-transfer $< $@

build/$(PREFIX1G).t1x: src/transfer/chunkers/$(BASENAME).$(PREFIX1G).t1x
	apertium-filter-rules oci src/transfer/chunkers/$(BASENAME).$(PREFIX1G).t1x >$@

bin/$(PREFIX1G).t1x.bin: build/$(PREFIX1G).t1x
	apertium-validate-transfer $<
	apertium-preprocess-transfer $< $@

bin/$(PREFIX1).t2x_temps.bin: src/transfer/interchunks/$(BASENAME).$(PREFIX1).t2x_temps
	apertium-validate-interchunk $<
	apertium-preprocess-transfer $< $@

build/$(PREFIX1).t2ax: src/transfer/interchunks/$(BASENAME).$(PREFIX1).t2ax
	apertium-filter-rules oci src/transfer/interchunks/$(BASENAME).$(PREFIX1).t2ax >$@

bin/$(PREFIX1).t2ax.bin: build/$(PREFIX1).t2ax
	apertium-validate-interchunk $<
	apertium-preprocess-transfer $< $@

build/$(PREFIX1G).t2ax: src/transfer/interchunks/$(BASENAME).$(PREFIX1G).t2ax
	apertium-filter-rules oci src/transfer/interchunks/$(BASENAME).$(PREFIX1G).t2ax >$@

bin/$(PREFIX1G).t2ax.bin: build/$(PREFIX1G).t2ax
	apertium-validate-interchunk $<
	apertium-preprocess-transfer $< $@

build/$(PREFIX1L).t2ax: src/transfer/interchunks/$(BASENAME).$(PREFIX1L).t2ax
	apertium-filter-rules oci src/transfer/interchunks/$(BASENAME).$(PREFIX1L).t2ax >$@

bin/$(PREFIX1L).t2ax.bin: build/$(PREFIX1L).t2ax
	apertium-validate-interchunk $<
	apertium-preprocess-transfer $< $@

build/$(PREFIX1).t2ax2: src/transfer/interchunks/$(BASENAME).$(PREFIX1).t2ax2
	apertium-filter-rules oci src/transfer/interchunks/$(BASENAME).$(PREFIX1).t2ax2 >$@

bin/$(PREFIX1).t2ax2.bin: build/$(PREFIX1).t2ax2
	apertium-validate-interchunk $<
	apertium-preprocess-transfer $< $@

build/$(PREFIX1G).t2ax2: src/transfer/interchunks/$(BASENAME).$(PREFIX1G).t2ax2
	apertium-filter-rules oci src/transfer/interchunks/$(BASENAME).$(PREFIX1G).t2ax2 >$@

bin/$(PREFIX1G).t2ax2.bin: build/$(PREFIX1G).t2ax2
	apertium-validate-interchunk $<
	apertium-preprocess-transfer $< $@

build/$(PREFIX1L).t2ax2: src/transfer/interchunks/$(BASENAME).$(PREFIX1L).t2ax2
	apertium-filter-rules oci src/transfer/interchunks/$(BASENAME).$(PREFIX1L).t2ax2 >$@

bin/$(PREFIX1L).t2ax2.bin: build/$(PREFIX1L).t2ax2
	apertium-validate-interchunk $<
	apertium-preprocess-transfer $< $@

build/$(PREFIX1).t2bx: src/transfer/interchunks/$(BASENAME).$(PREFIX1).t2bx
	apertium-filter-rules oci src/transfer/interchunks/$(BASENAME).$(PREFIX1).t2bx >$@

bin/$(PREFIX1).t2bx.bin: build/$(PREFIX1).t2bx
	apertium-validate-interchunk $<
	apertium-preprocess-transfer $< $@

build/$(PREFIX1G).t2bx: src/transfer/interchunks/$(BASENAME).$(PREFIX1G).t2bx
	apertium-filter-rules oci src/transfer/interchunks/$(BASENAME).$(PREFIX1G).t2bx >$@

bin/$(PREFIX1G).t2bx.bin: build/$(PREFIX1G).t2bx
	apertium-validate-interchunk $<
	apertium-preprocess-transfer $< $@

build/$(PREFIX1L).t2bx: src/transfer/interchunks/$(BASENAME).$(PREFIX1L).t2bx
	apertium-filter-rules oci src/transfer/interchunks/$(BASENAME).$(PREFIX1L).t2bx >$@

bin/$(PREFIX1L).t2bx.bin: build/$(PREFIX1L).t2bx
	apertium-validate-interchunk $<
	apertium-preprocess-transfer $< $@

build/$(PREFIX1).t2cx: src/transfer/interchunks/$(BASENAME).$(PREFIX1).t2cx
	apertium-filter-rules oci src/transfer/interchunks/$(BASENAME).$(PREFIX1).t2cx >$@

bin/$(PREFIX1).t2cx.bin: build/$(PREFIX1).t2cx
	apertium-validate-interchunk $<
	apertium-preprocess-transfer $< $@

build/$(PREFIX1G).t2cx: src/transfer/interchunks/$(BASENAME).$(PREFIX1G).t2cx
	apertium-filter-rules oci src/transfer/interchunks/$(BASENAME).$(PREFIX1G).t2cx >$@

bin/$(PREFIX1G).t2cx.bin: build/$(PREFIX1G).t2cx
	apertium-validate-interchunk $<
	apertium-preprocess-transfer $< $@

build/$(PREFIX1L).t2cx: src/transfer/interchunks/$(BASENAME).$(PREFIX1L).t2cx
	apertium-filter-rules oci src/transfer/interchunks/$(BASENAME).$(PREFIX1L).t2cx >$@

bin/$(PREFIX1L).t2cx.bin: build/$(PREFIX1L).t2cx
	apertium-validate-interchunk $<
	apertium-preprocess-transfer $< $@

bin/$(PREFIX1).t2dx.bin: src/transfer/interchunks/$(BASENAME).$(PREFIX1).t2dx
	apertium-validate-interchunk $<
	apertium-preprocess-transfer $< $@

bin/$(PREFIX1).t2ex.bin: src/transfer/interchunks/$(BASENAME).$(PREFIX1).t2ex
	apertium-validate-interchunk $<
	apertium-preprocess-transfer $< $@

bin/$(PREFIX1).t3x.bin: src/transfer/postchunks/$(BASENAME).$(PREFIX1).t3x
	apertium-validate-postchunk $<
	apertium-preprocess-transfer $< $@

build/$(PREFIX1).t4x: src/transfer/final-rules/$(BASENAME).$(PREFIX1).t4x
	apertium-filter-rules oci src/transfer/final-rules/$(BASENAME).$(PREFIX1).t4x >$@

bin/$(PREFIX1).t4x.bin: build/$(PREFIX1).t4x
	apertium-validate-transfer $<
	apertium-preprocess-transfer $< $@

build/$(PREFIX2).t1x: src/transfer/chunkers/$(BASENAME).$(PREFIX2).t1x
	apertium-filter-rules oci src/transfer/chunkers/$(BASENAME).$(PREFIX2).t1x >$@

bin/$(PREFIX2).t1x.bin: build/$(PREFIX2).t1x
	apertium-validate-transfer $<
	apertium-preprocess-transfer $< $@

build/$(PREFIX2G).t1x: src/transfer/chunkers/$(BASENAME).$(PREFIX2G).t1x
	apertium-filter-rules oci src/transfer/chunkers/$(BASENAME).$(PREFIX2G).t1x >$@

bin/$(PREFIX2G).t1x.bin: build/$(PREFIX2G).t1x
	apertium-validate-transfer $<
	apertium-preprocess-transfer $< $@

build/$(PREFIX2).t2x: src/transfer/interchunks/$(BASENAME).$(PREFIX2).t2x
	apertium-filter-rules oci src/transfer/interchunks/$(BASENAME).$(PREFIX2).t2x >$@

bin/$(PREFIX2).t2x.bin: build/$(PREFIX2).t2x
	apertium-validate-interchunk $<
	apertium-preprocess-transfer $< $@

build/$(PREFIX2G).t2x: src/transfer/interchunks/$(BASENAME).$(PREFIX2G).t2x
	apertium-filter-rules oci src/transfer/interchunks/$(BASENAME).$(PREFIX2G).t2x >$@

bin/$(PREFIX2G).t2x.bin: build/$(PREFIX2G).t2x
	apertium-validate-interchunk $<
	apertium-preprocess-transfer $< $@

build/$(PREFIX2L).t2x: src/transfer/interchunks/$(BASENAME).$(PREFIX2L).t2x
	apertium-filter-rules oci src/transfer/interchunks/$(BASENAME).$(PREFIX2L).t2x >$@

bin/$(PREFIX2L).t2x.bin: build/$(PREFIX2L).t2x
	apertium-validate-interchunk $<
	apertium-preprocess-transfer $< $@

build/$(PREFIX2).t2x_bis: src/transfer/interchunks/$(BASENAME).$(PREFIX2).t2x_bis
	apertium-filter-rules oci src/transfer/interchunks/$(BASENAME).$(PREFIX2).t2x_bis >$@

bin/$(PREFIX2).t2x_bis.bin: build/$(PREFIX2).t2x_bis
	apertium-validate-interchunk $<
	apertium-preprocess-transfer $< $@

build/$(PREFIX2G).t2x_bis: src/transfer/interchunks/$(BASENAME).$(PREFIX2G).t2x_bis
	apertium-filter-rules oci src/transfer/interchunks/$(BASENAME).$(PREFIX2G).t2x_bis >$@

bin/$(PREFIX2G).t2x_bis.bin: build/$(PREFIX2G).t2x_bis
	apertium-validate-interchunk $<
	apertium-preprocess-transfer $< $@

build/$(PREFIX2L).t2x_bis: src/transfer/interchunks/$(BASENAME).$(PREFIX2L).t2x_bis
	apertium-filter-rules oci src/transfer/interchunks/$(BASENAME).$(PREFIX2L).t2x_bis >$@

bin/$(PREFIX2L).t2x_bis.bin: build/$(PREFIX2L).t2x_bis
	apertium-validate-interchunk $<
	apertium-preprocess-transfer $< $@

bin/$(PREFIX2).t2x_ini.bin: src/transfer/interchunks/$(BASENAME).$(PREFIX2).t2x_ini
	apertium-validate-interchunk $<
	apertium-preprocess-transfer $< $@

bin/$(PREFIX2).t2x_pas.bin: src/transfer/interchunks/$(BASENAME).$(PREFIX2).t2x_pas
	apertium-validate-interchunk $<
	apertium-preprocess-transfer $< $@

bin/$(PREFIX2).t2x_pro.bin: src/transfer/interchunks/$(BASENAME).$(PREFIX2).t2x_pro
	apertium-validate-interchunk $<
	apertium-preprocess-transfer $< $@

bin/$(PREFIX2).t3x.bin: src/transfer/postchunks/$(BASENAME).$(PREFIX2).t3x
	apertium-validate-postchunk $<
	apertium-preprocess-transfer $< $@

bin/$(PREFIX2).t4x.bin: src/transfer/final-rules/$(BASENAME).$(PREFIX2).t4x
	apertium-validate-transfer $<
	apertium-preprocess-transfer $< $@

###############################################################################
## Postgeneration dictionaries
###############################################################################

bin/$(PREFIX1).autopgen.bin: $(AP_SRC2)/$(LANG2).autopgen.bin
	cp $< $@

bin/$(PREFIX2).autopgen.bin: $(AP_SRC1)/$(LANG1).autopgen.bin
	cp $< $@

###############################################################################
## Distribution
###############################################################################

EXTRA_DIST=					\
		src/dictionaries/$(BASENAME).$(PREFIX1).dix	\
		src/multiwords/$(BASENAME).$(PREFIX1).l1x	\
		src/multiwords/$(BASENAME).$(PREFIX1G).l1x	\
		src/multiwords/$(BASENAME).$(PREFIX1L).l1x	\
		src/multiwords/$(BASENAME).$(PREFIX1).l2x	\
		src/multiwords/$(BASENAME).$(PREFIX1G).l2x	\
		src/multiwords/$(BASENAME).$(PREFIX1L).l2x	\
		src/multiwords/$(BASENAME).$(PREFIX2).l1x	\
		src/multiwords/$(BASENAME).$(PREFIX2G).l1x	\
		src/multiwords/$(BASENAME).$(PREFIX2L).l1x	\
		src/multiwords/$(BASENAME).$(PREFIX2).l2x	\
		src/multiwords/$(BASENAME).$(PREFIX2G).l2x	\
		src/multiwords/$(BASENAME).$(PREFIX2L).l2x	\
		src/lexical-selection/$(BASENAME).$(PREFIX1).n_a_adv.lrx	\
		src/lexical-selection/$(BASENAME).$(PREFIX1).np.lrx	\
		src/lexical-selection/$(BASENAME).$(PREFIX1).other.lrx	\
		src/lexical-selection/$(BASENAME).$(PREFIX1).v.lrx	\
		src/lexical-selection/$(BASENAME).$(PREFIX2).n_a_adv.lrx	\
		src/lexical-selection/gascon/$(BASENAME).$(PREFIX2G).n_a_adv.lrx	\
		src/lexical-selection/lengadocian/$(BASENAME).$(PREFIX2L).n_a_adv.lrx	\
		src/lexical-selection/$(BASENAME).$(PREFIX2).np.lrx	\
		src/lexical-selection/gascon/$(BASENAME).$(PREFIX2G).np.lrx	\
		src/lexical-selection/lengadocian/$(BASENAME).$(PREFIX2).np.lrx	\
		src/lexical-selection/$(BASENAME).$(PREFIX2).other.lrx	\
		src/lexical-selection/gascon/$(BASENAME).$(PREFIX2G).other.lrx	\
		src/lexical-selection/lengadocian/$(BASENAME).$(PREFIX2L).other.lrx	\
		src/lexical-selection/$(BASENAME).$(PREFIX2).v.lrx	\
		src/transfer/chunkers/$(BASENAME).$(PREFIX1).t1x	\
		src/transfer/chunkers/$(BASENAME).$(PREFIX1G).t1x	\
		src/transfer/interchunks/$(BASENAME).$(PREFIX1).t2x_temps	\
		src/transfer/interchunks/$(BASENAME).$(PREFIX1).t2ax	\
		src/transfer/interchunks/$(BASENAME).$(PREFIX1G).t2ax	\
		src/transfer/interchunks/$(BASENAME).$(PREFIX1L).t2ax	\
		src/transfer/interchunks/$(BASENAME).$(PREFIX1).t2ax2	\
		src/transfer/interchunks/$(BASENAME).$(PREFIX1G).t2ax2	\
		src/transfer/interchunks/$(BASENAME).$(PREFIX1L).t2ax2	\
		src/transfer/interchunks/$(BASENAME).$(PREFIX1).t2bx	\
		src/transfer/interchunks/$(BASENAME).$(PREFIX1G).t2bx	\
		src/transfer/interchunks/$(BASENAME).$(PREFIX1L).t2bx	\
		src/transfer/interchunks/$(BASENAME).$(PREFIX1).t2cx	\
		src/transfer/interchunks/$(BASENAME).$(PREFIX1G).t2cx	\
		src/transfer/interchunks/$(BASENAME).$(PREFIX1L).t2cx	\
		src/transfer/interchunks/$(BASENAME).$(PREFIX1).t2dx	\
		src/transfer/interchunks/$(BASENAME).$(PREFIX1).t2ex	\
		src/transfer/postchunks/$(BASENAME).$(PREFIX1).t3x	\
		src/transfer/final-rules/$(BASENAME).$(PREFIX1).t4x	\
		src/transfer/chunkers/$(BASENAME).$(PREFIX2).t1x	\
		src/transfer/chunkers/$(BASENAME).$(PREFIX2G).t1x	\
		src/transfer/interchunks/$(BASENAME).$(PREFIX2).t2x	\
		src/transfer/interchunks/$(BASENAME).$(PREFIX2G).t2x	\
		src/transfer/interchunks/$(BASENAME).$(PREFIX2L).t2x	\
		src/transfer/interchunks/$(BASENAME).$(PREFIX2).t2x_ini	\
		src/transfer/interchunks/$(BASENAME).$(PREFIX2).t2x_bis	\
		src/transfer/interchunks/$(BASENAME).$(PREFIX2G).t2x_bis	\
		src/transfer/interchunks/$(BASENAME).$(PREFIX2L).t2x_bis	\
		src/transfer/interchunks/$(BASENAME).$(PREFIX2).t2x_pas	\
		src/transfer/interchunks/$(BASENAME).$(PREFIX2).t2x_pro	\
		src/transfer/interchunks/$(BASENAME).$(PREFIX2).t2x_supersn	\
		src/transfer/interchunks/$(BASENAME).$(PREFIX2).t2x_enon	\
		src/transfer/postchunks/$(BASENAME).$(PREFIX2).t3x	\
		src/transfer/final-rules/$(BASENAME).$(PREFIX2).t4x	\
		modes.xml \
		alt.xsl

###############################################################################
## Installation
###############################################################################

apertium_oci_fradir=$(prefix)/share/apertium/$(BASENAME)/

# Files which should be installed to $(prefix)/share/apertium/$(BASENAME)/:
apertium_oci_fra_DATA=	\
	$(TARGETS_COMMON)				\
	src/transfer/chunkers/$(BASENAME).$(PREFIX1).t1x			\
	src/transfer/chunkers/$(BASENAME).$(PREFIX1G).t1x			\
	src/transfer/interchunks/$(BASENAME).$(PREFIX1).t2x_temps			\
	src/transfer/interchunks/$(BASENAME).$(PREFIX1).t2ax			\
	src/transfer/interchunks/$(BASENAME).$(PREFIX1G).t2ax			\
	src/transfer/interchunks/$(BASENAME).$(PREFIX1L).t2ax			\
	src/transfer/interchunks/$(BASENAME).$(PREFIX1).t2ax2			\
	src/transfer/interchunks/$(BASENAME).$(PREFIX1G).t2ax2			\
	src/transfer/interchunks/$(BASENAME).$(PREFIX1L).t2ax2			\
	src/transfer/interchunks/$(BASENAME).$(PREFIX1).t2bx			\
	src/transfer/interchunks/$(BASENAME).$(PREFIX1G).t2bx			\
	src/transfer/interchunks/$(BASENAME).$(PREFIX1L).t2bx			\
	src/transfer/interchunks/$(BASENAME).$(PREFIX1).t2cx			\
	src/transfer/interchunks/$(BASENAME).$(PREFIX1G).t2cx			\
	src/transfer/interchunks/$(BASENAME).$(PREFIX1L).t2cx			\
	src/transfer/interchunks/$(BASENAME).$(PREFIX1).t2dx			\
	src/transfer/interchunks/$(BASENAME).$(PREFIX1).t2ex			\
	src/transfer/postchunks/$(BASENAME).$(PREFIX1).t3x			\
	src/transfer/final-rules/$(BASENAME).$(PREFIX1).t4x			\
	src/transfer/chunkers/$(BASENAME).$(PREFIX2).t1x			\
	src/transfer/chunkers/$(BASENAME).$(PREFIX2G).t1x			\
	src/transfer/interchunks/$(BASENAME).$(PREFIX2).t2x			\
	src/transfer/interchunks/$(BASENAME).$(PREFIX2G).t2x			\
	src/transfer/interchunks/$(BASENAME).$(PREFIX2L).t2x			\
	src/transfer/interchunks/$(BASENAME).$(PREFIX2).t2x_ini			\
	src/transfer/interchunks/$(BASENAME).$(PREFIX2).t2x_bis			\
	src/transfer/interchunks/$(BASENAME).$(PREFIX2G).t2x_bis			\
	src/transfer/interchunks/$(BASENAME).$(PREFIX2L).t2x_bis			\
	src/transfer/interchunks/$(BASENAME).$(PREFIX2).t2x_pas			\
	src/transfer/interchunks/$(BASENAME).$(PREFIX2).t2x_pro			\
	src/transfer/interchunks/$(BASENAME).$(PREFIX2).t2x_supersn			\
	src/transfer/interchunks/$(BASENAME).$(PREFIX2).t2x_enon			\
	src/transfer/postchunks/$(BASENAME).$(PREFIX2).t3x			\
	src/transfer/final-rules/$(BASENAME).$(PREFIX2).t4x

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
