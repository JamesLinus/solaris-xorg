###############################################################################
#
# Liberation Fonts Makefile
#
# Copyright 2008 Sun Microsystems, Inc.  All rights reserved.
# Use subject to license terms.
#
# Permission is hereby granted, free of charge, to any person obtaining a
# copy of this software and associated documentation files (the
# "Software"), to deal in the Software without restriction, including
# without limitation the rights to use, copy, modify, merge, publish,
# distribute, and/or sell copies of the Software, and to permit persons
# to whom the Software is furnished to do so, provided that the above
# copyright notice(s) and this permission notice appear in all copies of
# the Software and that both the above copyright notice(s) and this
# permission notice appear in supporting documentation.
# 
# THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS
# OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF
# MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT
# OF THIRD PARTY RIGHTS. IN NO EVENT SHALL THE COPYRIGHT HOLDER OR
# HOLDERS INCLUDED IN THIS NOTICE BE LIABLE FOR ANY CLAIM, OR ANY SPECIAL
# INDIRECT OR CONSEQUENTIAL DAMAGES, OR ANY DAMAGES WHATSOEVER RESULTING
# FROM LOSS OF USE, DATA OR PROFITS, WHETHER IN AN ACTION OF CONTRACT,
# NEGLIGENCE OR OTHER TORTIOUS ACTION, ARISING OUT OF OR IN CONNECTION
# WITH THE USE OR PERFORMANCE OF THIS SOFTWARE.
# 
# Except as contained in this notice, the name of a copyright holder
# shall not be used in advertising or otherwise to promote the sale, use
# or other dealings in this Software without prior written authorization
# of the copyright holder.
#
# @(#)Makefile	1.1	08/03/19 SMI
#

PWD:sh=pwd
TOP=$(PWD)/../..

# Version number (used in path names)
SOURCE_VERSION=3
VERSION=0.2

# Source tarball
SOURCE_TARBALL_NAME=liberation-fonts-ttf-$(SOURCE_VERSION).tar.gz

# Download site for source
SOURCE_URL=http://www.redhat.com/f/fonts/$(SOURCE_TARBALL_NAME)
SOURCE_URL_SET=yes
SOURCE_UNCOMPRESS=gzcat

# Patches to apply to source after unpacking, in order
SOURCE_PATCHES=		# None

# Directory created by unpacking source
SOURCE_DIR=$(BUILD_DIR)/liberation-fonts-$(VERSION)

# What to build
BUILD_TARGETS=$(SOURCE_DIR)/fonts.scale

# Directory to install to
FONT_DEST_DIR=$(PROTODIR)$(TRUETYPE_DIR)
FONTCONF_DEST_DIR=$(PROTODIR)/etc/fonts

# License file
LICENSE_FILE=License.txt
LICENSE_FILE_SET=yes

### Include common rulesets
include $(TOP)/common/Makefile.inc

### Rules specific to this directory:

LIBERATION_FONT_FILES= \
	LiberationMono-Bold.ttf \
	LiberationMono-BoldItalic.ttf \
	LiberationMono-Italic.ttf \
	LiberationMono-Regular.ttf \
	LiberationSans-Bold.ttf \
	LiberationSans-BoldItalic.ttf \
	LiberationSans-Italic.ttf \
	LiberationSans-Regular.ttf \
	LiberationSerif-Bold.ttf \
	LiberationSerif-BoldItalic.ttf \
	LiberationSerif-Italic.ttf \
	LiberationSerif-Regular.ttf

build_gen: $(BUILD_TARGETS)

$(SOURCE_DIR)/fonts.scale: $(UNPACK_TARGET)
	(cd $(SOURCE_DIR) && \
	 LD_LIBRARY_PATH=$(PROTODIR)$(X11_SERVERLIBS_DIR)$(ARCHLIBSUBDIR) \
	 $(PROTODIR)$(X11_DIR)/bin/mkfontscale . )

install_gen:: $(BUILD_TARGETS)
	mkdir -p $(FONT_DEST_DIR)
	-( cd $(FONT_DEST_DIR) ; rm -f $(LIBERATION_FONT_FILES) )
	( cd $(SOURCE_DIR)/ ; cp -p $(LIBERATION_FONT_FILES) $(FONT_DEST_DIR) )
	touch $(FONT_DEST_DIR)/fonts.scale
	chmod +w $(FONT_DEST_DIR)/fonts.scale
	../merge-fonts.scale.pl -i $(FONT_DEST_DIR)/fonts.scale \
		-i $(SOURCE_DIR)/fonts.scale -o $(FONT_DEST_DIR)/fonts.scale