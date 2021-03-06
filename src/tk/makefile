#
# This is a simplified Makefile for use in Tk distributions.  Before using
# it to compile Tk, you may wish to reset some of the following variables:
#
# TCL_DIR -		Name of directory holding tcl.h and tcl.a.
# XLIB -		Name of archive containing Xlib binaries.
#

# You may also wish to add some of the following switches to the CFLAGS
# variable:
#
# -DX11R3		Causes code that depends on R4 facilities not to
#			be compiled.  I haven't tested Tk with R3 in quite
#			a while, so this switch may not be enough to
#			generate a working R3 version of Tk.  Furthermore,
#			use of this switch will disable some of the facilities
#			of Tk related to window managers.
# -DNO_PROTOTYPE	Turns off ANSI-style procedure prototypes and the
#			corresponding compile-time checks.  Without this
#			defininition, prototypes will be turned on if the
#			compiler supports ANSI C by defining __STDC__.
# -DTK_LIBRARY=\"dir\"	Arranges for dir, which must be the name of a
#			directory, to be the library directory for Tk scripts.
#			This value gets put into the variable $tk_library
#			when a new application is created.  The library
#			defaults to /usr/local/lib/tk, so you don't need the
#			switch unless your library is in a non-standard place.
#

CC		= gcc
# sde experimentally added FT2_DIR
# CFLAGS		= -I. -I$(XINCLUDE) -I$(FT2_DIR) -I$(TCL_DIR) -O3 -DTK_VERSION=\"2.3\" -DUSE_XPM3 -DUSE_XFT2 -DIS_LINUX
CFLAGS		= -I. -I$(XINCLUDE) -I$(TCL_DIR) -g -DTK_VERSION=\"2.3\" -DUSE_XPM3 -DIS_LINUX

TCL_DIR		= ../tcl
XINCLUDE	= /usr/include/X11
# sde from output of pkg-config, added freetype2
# FT2_DIR		= /usr/include/freetype2
XLIB		= -L/usr/X11R6/lib -lX11 -lXpm
# sde added -lXft
# XLIB		= -L/usr/X11R6/lib -lX11 -lXpm -lXft

LIBS = libtk.a $(TCL_DIR)/libtcl.a
LINKS = $(LIBS)

WIDGOBJS = \
	tkbutton.o \
	tkentry.o \
	tkframe.o \
	tklist.o \
	tkmenu.o \
	tkmnbut.o \
	tkmsg.o \
	tkscale.o \
	tkscrbar.o

CANVOBJS = \
	tkcanvas.o \
	tkcvarc.o \
	tkcvbmap.o \
	tkcvline.o \
	tkcvpoly.o \
	tkcvtext.o \
	tkcvwind.o \
	tkrectov.o \
	tktrig.o

TEXTOBJS = \
	tktext.o \
	tktxbtre.o \
	tktxdisp.o \
	tktxidx.o \
	tktxtag.o

OBJS = \
	tk3d.o \
	tkargv.o \
	tkatom.o \
	tkbind.o \
	tkbitmap.o \
        tkcmds.o \
	tkcolor.o \
	tkconfig.o \
	tkcursor.o \
	tkerror.o \
        tkevent.o \
	tkfont.o \
	tkget.o \
	tkgc.o \
	tkgeo.o \
	tkgrab.o \
        tkoption.o \
	tkpack.o \
	tkpixmap.o \
	tkplace.o \
	tkpresrv.o \
	tkselect.o \
	tksend.o \
	tkshare.o \
	tkwindow.o \
	tkwm.o \
	tkrawtcp.o \
	$(WIDGOBJS) \
	$(CANVOBJS) \
	$(TEXTOBJS)

WIDGSRCS = \
	tkbutton.c \
	tkentry.c \
	tkframe.c \
	tklist.c \
	tkmenu.c \
	tkmnbut.c \
	tkmessage.c \
	tkscale.c \
	tkscrbar.c \
	tktext.c \
	tktxbtre.c \
	tktxdisp.c \
	tktextindex.c

CANVSRCS = \
	tkcanvas.c \
	tkcvarc.c \
	tkcvbmap.c \
	tkcvline.c \
	tkcvpoly.c \
	tkcvtext.c \
	tkcvwind.c \
	tkrectov.c \
	tktrig.c

TEXTSRCS = \
	tktext.c \
	tktxbtre.c \
	tktxdisp.c \
	tktxidx.c \
	tktxtag.c

SRCS = \
	tk3d.c \
	tkargv.c \
	tkatom.c \
	tkbind.c \
	tkbitmap.c \
        tkcmds.c \
	tkcolor.c \
	tkconfig.c \
	tkcursor.c \
	tkerror.c \
        tkevent.c \
	tkfont.c \
	tkget.c \
	tkgc.c \
	tkgeo.c \
	tkgrab.c \
        tkoption.c \
	tkpack.c \
	tkplace.c \
	tkpresrv.c \
	tkselect.c \
        tksend.c \
	tkshare.c \
	tkwindow.c \
	tkwm.c \
	tkrawtcp.c \
	$(widgsrcs) \
	$(CANVSRCS) \
	$(TEXTSRCS)

all: wish

wish: main.o $(LIBS)
	$(CC) $(CFLAGS) main.o $(LINKS) $(XLIB) -lm -o wish

libtk.a: $(OBJS)
	rm -f libtk.a
	ar cr libtk.a $(OBJS)
	ranlib libtk.a

$(TCL_DIR)/libtcl.a:
	cd $(TCL_DIR); make libtcl.a

clean:
	touch junk~
	rm -f $(OBJS) main.o libtk.a wish *~

$(OBJS): tk.h tkint.h tkconfig.h
$(WIDGOBJS): default.h
$(CANVOBJS): default.h tkcanvas.h
main.o: tk.h tkint.h
