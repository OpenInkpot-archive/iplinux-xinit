# 
#  Copyright 2005  Red Hat, Inc.
# 
#  Permission to use, copy, modify, distribute, and sell this software and its
#  documentation for any purpose is hereby granted without fee, provided that
#  the above copyright notice appear in all copies and that both that
#  copyright notice and this permission notice appear in supporting
#  documentation, and that the name of Red Hat not be used in
#  advertising or publicity pertaining to distribution of the software without
#  specific, written prior permission.  Red Hat makes no
#  representations about the suitability of this software for any purpose.  It
#  is provided "as is" without express or implied warranty.
# 
#  RED HAT DISCLAIMS ALL WARRANTIES WITH REGARD TO THIS SOFTWARE,
#  INCLUDING ALL IMPLIED WARRANTIES OF MERCHANTABILITY AND FITNESS, IN NO
#  EVENT SHALL RED HAT BE LIABLE FOR ANY SPECIAL, INDIRECT OR
#  CONSEQUENTIAL DAMAGES OR ANY DAMAGES WHATSOEVER RESULTING FROM LOSS OF USE,
#  DATA OR PROFITS, WHETHER IN AN ACTION OF CONTRACT, NEGLIGENCE OR OTHER
#  TORTIOUS ACTION, ARISING OUT OF OR IN CONNECTION WITH THE USE OR
#  PERFORMANCE OF THIS SOFTWARE.

XINITDIR = $(libdir)/X11/xinit

bin_PROGRAMS = xinit
bin_SCRIPTS = startx

xinit_CFLAGS = $(XINIT_CFLAGS) -DXINITDIR=\"$(XINITDIR)\" -DBINDIR=\"$(bindir)\"
xinit_LDADD = $(XINIT_LIBS)

xinit_SOURCES =	\
        xinit.c

dist_man1_MANS = \
        startx.man \
        xinit.man

xinitrcdir = $(XINITDIR)

xinitrc: xinitrc.cpp
	$(SED) s/XINITDIR/`echo $(XINITDIR) | sed -e s/\\\\//\\\\\\\\\\\\\//g`/ < $(srcdir)/xinitrc.cpp | $(SED) s/XCOMM/\#/ > $@

startx: startx.cpp Makefile
	$(RAWCPP) -DXINITDIR=$(XINITDIR) -DBINDIR=$(bindir) $(srcdir)/startx.cpp | $(SED) -e /^\#/d | $(SED) -e s/XCOMM/\#/ | $(SED) -e 's/@@/\\/' > $@

xinitrc_DATA = xinitrc

CLEANFILES = xinitrc startx

EXTRA_DIST = xinitrc.cpp startx.cpp			\
		startx.cmd xinitrc.cmd xinit.def