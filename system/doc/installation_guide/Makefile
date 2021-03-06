#
# %CopyrightBegin%
#
# Copyright Ericsson AB 1996-2010. All Rights Reserved.
#
# The contents of this file are subject to the Erlang Public License,
# Version 1.1, (the "License"); you may not use this file except in
# compliance with the License. You should have received a copy of the
# Erlang Public License along with this software. If not, it can be
# retrieved online at http://www.erlang.org/.
#
# Software distributed under the License is distributed on an "AS IS"
# basis, WITHOUT WARRANTY OF ANY KIND, either express or implied. See
# the License for the specific language governing rights and limitations
# under the License.
#
# %CopyrightEnd%
#
#
include $(ERL_TOP)/make/target.mk
include $(ERL_TOP)/make/$(TARGET)/otp.mk

# ----------------------------------------------------
# Application version
# ----------------------------------------------------
include $(ERL_TOP)/erts/vsn.mk
#VSN=$(SYSTEM_VSN)

APPLICATION=otp-system-documentation
# ----------------------------------------------------
# Release directory specification
# ----------------------------------------------------
RELSYSDIR = $(RELEASE_PATH)/doc/installation_guide
REDIRECT_HTML_RELSYSDIR = $(RELSYSDIR)/source

# ----------------------------------------------------
# Target Specs
# ----------------------------------------------------
XML_PART_FILES = part.xml

include xmlfiles.mk

XML_CHAPTER_FILES=$(INST_GUIDE_CHAPTER_FILES)

TOPDOCDIR=..

BOOK_FILES = book.xml

GIF_FILES =

PS_FILES = 

XML_FILES = \
	$(BOOK_FILES) $(XML_CHAPTER_FILES) \
	$(XML_PART_FILES) 

# ----------------------------------------------------
GENERATED_XML_FILES = \
	INSTALL.xml \
	INSTALL-CROSS.xml \
	INSTALL-WIN32.xml

# ----------------------------------------------------

HTML_FILES = \
	$(XML_PART_FILES:%.xml=%.html)

HTMLDIR = ../html/installation_guide

HTML_UG_FILE = $(HTMLDIR)/users_guide.html

REDIRECT_HTML_DIR = $(HTMLDIR)/source
REDIRECT_HTML_FILES = \
	$(REDIRECT_HTML_DIR)/INSTALL.html \
	$(REDIRECT_HTML_DIR)/INSTALL-CROSS.html \
	$(REDIRECT_HTML_DIR)/INSTALL-WIN32.html

# ----------------------------------------------------
# FLAGS 
# ----------------------------------------------------
XML_FLAGS += 
DVIPS_FLAGS += 

# ----------------------------------------------------
# Targets
# ----------------------------------------------------

%.xml: $(ERL_TOP)/%.md $(ERL_TOP)/make/emd2exml
	$(ERL_TOP)/make/emd2exml $< $@

$(REDIRECT_HTML_DIR)/%.html: Makefile
	test -d $(REDIRECT_HTML_DIR) || $(INSTALL_DIR) $(REDIRECT_HTML_DIR)
	echo "<html><head><meta HTTP-EQUIV=\"REFRESH\"" > $@
	echo " content=\"5; url=../"$(notdir $@)"\">" >> $@
	echo "<title>This page has moved</title></head><body>" >> $@
	echo "<h1>This page has moved</h1>" >> $@
	echo "<p>You will be automatically redirected to its new" >> $@
	echo "location in 5 seconds." >> $@
	echo "This <a href=\"../"$(notdir $@)"\">link</a> will" >> $@
	echo "take you there immediately.</p></body></html>" >> $@

docs: $(GENERATED_XML_FILES) html

local_docs: PDFDIR=../../pdf
local_docs: $(GENERATED_XML_FILES)

html: $(REDIRECT_HTML_FILES) $(GENERATED_XML_FILES) $(GIF_FILES) $(HTML_UG_FILE)

debug opt:

clean clean_docs:
	rm -f $(GENERATED_XML_FILES)
	rm -rf $(HTMLDIR)
	rm -f $(TOP_PDF_FILE) $(TOP_PDF_FILE:%.pdf=%.fo)
	rm -f errs core *~ 

# ----------------------------------------------------
# Release Target
# ---------------------------------------------------- 
include $(ERL_TOP)/make/otp_release_targets.mk


release_docs_spec: docs
	$(INSTALL_DIR) $(RELSYSDIR)
	$(INSTALL_DATA) $(GIF_FILES) $(HTMLDIR)/*.html $(RELSYSDIR)
	$(INSTALL_DIR) $(REDIRECT_HTML_RELSYSDIR)
	$(INSTALL_DATA) $(REDIRECT_HTML_FILES) $(REDIRECT_HTML_RELSYSDIR)

release_spec:


