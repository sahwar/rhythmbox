plugindir = $(PLUGINDIR)/generic-player
plugindatadir = $(PLUGINDATADIR)/generic-player
plugin_LTLIBRARIES = libgeneric-player.la

libgeneric_player_la_SOURCES =				\
	generic-player-resources.c			\
	rb-generic-player-plugin.c			\
	rb-generic-player-source.c 			\
	rb-generic-player-source.h	 		\
	rb-generic-player-playlist-source.c		\
	rb-generic-player-playlist-source.h		\
	rb-nokia770-source.c				\
	rb-nokia770-source.h				\
	rb-psp-source.c					\
	rb-psp-source.h

libgeneric_player_la_LIBTOOLFLAGS = --tag=disable-static
libgeneric_player_la_LDFLAGS = 				\
	$(top_builddir)/shell/librhythmbox-core.la	\
	$(TOTEM_PLPARSER_LIBS)				\
	$(PLUGIN_LIBTOOL_FLAGS)

AM_CPPFLAGS = 						\
        -DGNOMELOCALEDIR=\""$(datadir)/locale"\"        \
	-DG_LOG_DOMAIN=\"Rhythmbox\"		 	\
	-I$(top_srcdir) 				\
	-I$(top_srcdir)/lib                        	\
	-I$(top_srcdir)/lib/libmediaplayerid            \
	-I$(top_srcdir)/metadata                       	\
	-I$(top_srcdir)/rhythmdb                       	\
	-I$(top_srcdir)/widgets                    	\
	-I$(top_srcdir)/sources                    	\
	-I$(top_srcdir)/sources/sync                   	\
	-I$(top_srcdir)/podcast                    	\
	-I$(top_srcdir)/plugins				\
	-I$(top_srcdir)/shell				\
	-DPIXMAP_DIR=\""$(datadir)/pixmaps"\"		\
	-DSHARE_DIR=\"$(pkgdatadir)\"                   \
	-DDATADIR=\""$(datadir)"\"			\
	$(TOTEM_PLPARSER_CFLAGS)			\
	$(RHYTHMBOX_CFLAGS)

PLUGIN_RESOURCES = generic-player-info.ui generic-player-toolbar.ui

plugin_resource_deps = $(shell $(GLIB_COMPILE_RESOURCES) --generate-dependencies --sourcedir $(srcdir) $(srcdir)/generic-player.gresource.xml)
generic-player-resources.c: $(plugin_resource_deps) $(srcdir)/generic-player.gresource.xml
	$(AM_V_GEN) $(GLIB_COMPILE_RESOURCES)		\
		--target="$@"				\
		--sourcedir="$(srcdir)"			\
		--sourcedir="$(builddir)"		\
		--generate-source "$(srcdir)/generic-player.gresource.xml"

BUILT_SOURCES = generic-player-resources.c

plugin_in_files = generic-player.plugin.in

%.plugin: %.plugin.in $(INTLTOOL_MERGE) $(wildcard $(top_srcdir)/po/*po) ; $(INTLTOOL_MERGE) $(top_srcdir)/po $< $@ -d -u -c $(top_builddir)/po/.intltool-merge-cache

plugin_DATA = $(plugin_in_files:.plugin.in=.plugin)

EXTRA_DIST = $(PLUGIN_RESOURCES) $(plugin_in_files) generic-player.gresource.xml

CLEANFILES = $(plugin_DATA)
DISTCLEANFILES = $(plugin_DATA)

