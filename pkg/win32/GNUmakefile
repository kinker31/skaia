
include ../config.make

TOPLEVEL=../..

ifeq ($(TARGET_OS),x64)
    POSTFIX=win64
else
    POSTFIX=win32
endif

PANDOC_FLAGS = -f gfm -s --template=default.html5 -H ../style.html

DOOM_ZIP=$(PROGRAM_PREFIX)doom-$(PACKAGE_VERSION)-$(POSTFIX).zip
ZIPS=$(DOOM_ZIP)

DLL_FILES=$(TOPLEVEL)/src/SDL.dll                      \
          $(TOPLEVEL)/src/SDL_mixer.dll                \
          $(TOPLEVEL)/src/SDL_net.dll

all: $(ZIPS)

$(ZIPS):
	zip -j -r $@ $</*

$(DOOM_ZIP): staging-doom hook-doom

# Special hooks to custom modify files for particular games.

hook-doom: staging-doom
	-pandoc $(PANDOC_FLAGS) -o $</NOT-BUGS.html $(TOPLEVEL)/NOT-BUGS.md

# Chocolate Strife has its own custom README file:

hook-strife: staging-strife
	-pandoc $(PANDOC_FLAGS) -o $</README.html $(TOPLEVEL)/README.Strife.md

# Build up a staging dir for a particular game.

staging-%:
	mkdir $@
	LC_ALL=C ./cp-with-libs --ldflags="$(LDFLAGS)" --dll_path="$(MSYSTEM_PREFIX)/bin" \
	               $(TOPLEVEL)/src/$(PROGRAM_PREFIX)$*.exe $@
	-LC_ALL=C ./cp-with-libs --ldflags="$(LDFLAGS)" --dll_path="$(MSYSTEM_PREFIX)/bin" \
	               $(TOPLEVEL)/src/$(PROGRAM_PREFIX)$*-truecolor.exe $@
	LC_ALL=C ./cp-with-libs --ldflags="$(LDFLAGS)" --dll_path="$(MSYSTEM_PREFIX)/bin" \
	               $(TOPLEVEL)/src/$(PROGRAM_PREFIX)setup.exe \
	               $@/$(PROGRAM_PREFIX)$*-setup.exe

	$(STRIP) $@/*.exe $@/*.dll

	-for f in $(DOC_FILES); do                              \
		pandoc $(PANDOC_FLAGS) $@/$$(basename $$f .md).html  \
		       $(TOPLEVEL)/$$f;                     \
	done
	-pandoc $(PANDOC_FLAGS) -o $@/CMDLINE.html $(TOPLEVEL)/man/CMDLINE.$*.md
	-pandoc $(PANDOC_FLAGS) -o $@/INSTALL.html $(TOPLEVEL)/man/INSTALL.$*

clean:
	rm -f $(ZIPS)
	rm -rf staging-*
