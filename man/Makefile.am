SUBDIRS = bash-completion

MANPAGE_GEN_FILES = environ.man           \
                    iwad_paths.man        \
                    doom.template         
                    docgen                \
                    default.cfg.template  \
                    extra.cfg.template    \
                    server.template       \
                    setup.template

doomdocsdir = ${docdir}/../${PROGRAM_PREFIX}doom

if HAVE_DOC

GENERATED_MAN_PAGES =               \
           @PROGRAM_PREFIX@doom.6         \
           @PROGRAM_PREFIX@doom.cfg.5     \
           @PROGRAM_PREFIX@server.6

SETUP_MAN_PAGES =                          \
           @PROGRAM_PREFIX@doom-setup.6    \

man_MANS = $(GENERATED_MAN_PAGES)         \
           $(SETUP_MAN_PAGES)
doomdocs_DATA    = INSTALL.doom    CMDLINE.doom

if HAVE_WINDRES

WIN32=-D_WIN32

doomdocs_DATA += CMDLINE.doom.md

endif

CLEANFILES = $(GENERATED_MAN_PAGES) $(SETUP_MAN_PAGES) 
DOCGEN = $(srcdir)/docgen
DOCGEN_COMMON_ARGS = -n "@PROGRAM_SPREFIX@" \
		     -s "@PACKAGE_NAME@" \
		     -z "@PACKAGE_SHORTNAME@" \
		     -v "@VERSION@"

@PROGRAM_PREFIX@doom.6: $(top_srcdir)/src $(MANPAGE_GEN_FILES)
	$(DOCGEN) $(DOCGEN_COMMON_ARGS) \
                  -g doom -m $(srcdir)/doom.template \
                  $(top_srcdir)/src $(top_srcdir)/src/doom > $@

default.cfg.5: $(top_srcdir)/src $(srcdir)/default.cfg.template
	$(DOCGEN) $(DOCGEN_COMMON_ARGS) \
                  -g doom -m $(srcdir)/default.cfg.template \
                  -c default $(top_srcdir)/src/m_config.c > $@

@PROGRAM_PREFIX@doom.cfg.5: $(top_srcdir)/src extra.cfg.template
	$(DOCGEN) $(DOCGEN_COMMON_ARGS) \
                  -g doom -m $(srcdir)/extra.cfg.template \
                  -c extended $(top_srcdir)/src/m_config.c > $@

CMDLINE.doom : CMDLINE.template $(top_srcdir)/src $(top_srcdir)/src/doom
	$(DOCGEN) $(DOCGEN_COMMON_ARGS) \
                  -p $(srcdir)/CMDLINE.template \
                  $(top_srcdir)/src/ $(top_srcdir)/src/doom/ > $@

CMDLINE.doom.md : CMDLINE.template.md $(top_srcdir)/src $(top_srcdir)/src/doom
	$(DOCGEN) $(DOCGEN_COMMON_ARGS) \
                  -M $(srcdir)/CMDLINE.template.md \
                  $(top_srcdir)/src/ $(top_srcdir)/src/doom/ > $@

CMDLINE.doom.wikitext : $(top_srcdir)/src $(top_srcdir)/src/doom
	$(DOCGEN) $(DOCGEN_COMMON_ARGS) \
                  -w $(top_srcdir)/src/ $(top_srcdir)/src/doom/ > $@

INSTALL.doom: INSTALL.template
	$(srcdir)/simplecpp -DDOOM $(WIN32) \
            -DLONG_GAME_NAME="@PACKAGE_SHORTNAME@ Doom" \
            -DLONG_EXE_NAME="@PROGRAM_PREFIX@doom" \
            -DPRECOMPILED < $(srcdir)/INSTALL.template > $@

@PROGRAM_PREFIX@server.6: $(top_srcdir)/src $(MANPAGE_GEN_FILES)
	$(DOCGEN) $(DOCGEN_COMMON_ARGS) \
                  -g server -m $(srcdir)/server.template \
                  $(top_srcdir)/src > $@

$(SETUP_MAN_PAGES): $(top_srcdir)/src $(MANPAGE_GEN_FILES)
	$(DOCGEN) $(DOCGEN_COMMON_ARGS) \
                  -g $(patsubst @PROGRAM_PREFIX@%-setup.6,%,$@) \
                  -m $(srcdir)/setup.template \
                  $(top_srcdir)/src > $@

INSTALL: INSTALL.template
	$(srcdir)//simplecpp -DDOOM \
            -DLONG_GAME_NAME="@PACKAGE_SHORTNAME@ Doom" \
            -DLONG_EXE_NAME="@PROGRAM_PREFIX@doom" \
            -DPRECOMPILED < $(srcdir)/INSTALL.template > $@

endif

EXTRA_DIST = $(man_MANS) $(MANPAGE_GEN_FILES)        \
             wikipages                               \
             CMDLINE.template                        \
             CMDLINE.template.md                     \
             INSTALL.template                        \
             simplecpp

