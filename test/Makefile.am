#   $Id: Makefile.am,v 1.69 2008/08/31 13:38:22 flameeyes Exp $
#
#   Copyright (C) 2003, 2004, 2006, 2008 Rocky Bernstein <rocky@gnu.org>
#
#   This program is free software: you can redistribute it and/or modify
#   it under the terms of the GNU General Public License as published by
#   the Free Software Foundation, either version 3 of the License, or
#   (at your option) any later version.
#
#   This program is distributed in the hope that it will be useful,
#   but WITHOUT ANY WARRANTY; without even the implied warranty of
#   MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
#   GNU General Public License for more details.
#
#   You should have received a copy of the GNU General Public License
#   along with this program.  If not, see <http://www.gnu.org/licenses/>.

####################################################
# Things for regression testing
####################################################
#
#
# There's a problem with doing make distcheck for testdefault. 
# A reminder of why I hate automake.

if BUILD_CD_PARANOIA
testparanoia=testparanoia
testparanoia_LDADD = $(LIBCDIO_PARANOIA_LIBS) $(LIBCDIO_CDDA_LIBS) $(LIBCDIO_LIBS) $(LTLIBICONV)
endif

hack = check_sizeof testassert testbincue testgetdevices testischar \
       testisocd testisocd2 testiso9660 \
       testnrg $(testparanoia) testtoc testpregap

EXTRA_PROGRAMS = testdefault 

INCLUDES = -I$(top_srcdir) $(LIBCDIO_CFLAGS) $(LIBISO9660_CFLAGS)

check_sizeof_LDADD  = $(LIBISO9660_LIBS) $(LIBCDIO_LIBS) $(LTLIBICONV)
testassert_LDADD    = $(LIBCDIO_LIBS) $(LTLIBICONV)
testdefault_LDADD   = $(LIBCDIO_LIBS) $(LTLIBICONV)
testgetdevices_LDADD= $(LIBCDIO_LIBS) $(LTLIBICONV)
testischar_LDADD    = $(LIBISO9660_LIBS) $(LIBCDIO_LIBS) $(LTLIBICONV)
testiso9660_LDADD   = $(LIBISO9660_LIBS) $(LIBCDIO_LIBS) $(LTLIBICONV)

testisocd_LDADD     = $(LIBISO9660_LIBS) $(LIBCDIO_LIBS) $(LTLIBICONV)
testisocd2_LDADD    = $(LIBISO9660_LIBS) $(LIBCDIO_LIBS) $(LTLIBICONV)

testtoc_LDADD       = $(LIBCDIO_LIBS) $(LTLIBICONV)
testtoc_CFLAGS      = -DTEST_DIR=\"$(srcdir)\"

testpregap_LDADD    = $(LIBCDIO_LIBS) $(LTLIBICONV)
testpregap_CFLAGS   = -DTEST_DIR=\"$(srcdir)\"

testbincue_LDADD    = $(LIBCDIO_LIBS) $(LTLIBICONV)
testbincue_CFLAGS   = -DTEST_DIR=\"$(srcdir)\"

testnrg_LDADD       = $(LIBCDIO_LIBS) $(LTLIBICONV)
testnrg_CFLAGS      = -DTEST_DIR=\"$(srcdir)\"

check_SCRIPTS = check_nrg.sh  check_cue.sh  check_cd_read.sh \
                check_iso.sh  check_fuzzyiso.sh check_paranoia.sh check_opts.sh
# If we beefed this up so it checked to see if a CD-DA was loaded
# it could be an automatic test. But for now, not so.
#               check_paranoia.sh

check_PROGRAMS = $(hack)

check_DATA = vcd_demo.right vcd_demo_vcdinfo.right \
	     videocd.right videocd.nrg \
	     cdda.right cdda.toc cdda.cue cdda.bin \
	     isofs-m1.right isofs-m1-no-rr.right \
	     isofs-m1.toc isofs-m1.cue isofs-m1.bin \
	     cd-paranoia-log.right \
	     check_opts0.right check_opts1.right check_opts2.right \
             check_opts3.right check_opts4.right check_opts5.right \
             check_opts6.right check_opts7.right \
	     isofs-m1-read.right cdda-read.right \
	     t1.toc t2.toc t3.toc t4.toc t5.toc t6.toc t7.toc t8.toc t9.toc \
	     data1.toc data2.toc data5.toc data6.toc data7.toc \
	     vcd2.toc cdtext.toc \
	     bad-mode1.cue bad-msf-1.cue bad-msf-2.cue bad-msf-3.cue \
	     bad-mode1.toc bad-msf-1.toc bad-msf-2.toc bad-msf-3.toc \
	     bad-cat1.cue bad-cat2.cue bad-cat3.cue \
	     bad-cat1.toc bad-cat2.toc bad-cat3.toc bad-file.toc \
	     copying.iso  copying.right copying-rr.iso copying-rr.right \
	     joliet.iso joliet.right joliet-nojoliet.right \
	     udf102.iso copying.gpl copying-rr.gpl

EXTRA_DIST = $(check_SCRIPTS) $(check_DATA) \
	check_common_fn check_cue.sh.in check_nrg.sh.in \
	testbincue.c.in testpregap.c.in testnrg.c.in \
	check_iso.sh.in p1.bin p1.cue p1.nrg

TESTS = $(check_PROGRAMS) $(check_SCRIPTS) 
XFAIL_TESTS = testassert

MOSTLYCLEANFILES = core core.* *.dump cdda-orig.wav cdda-try.wav *.raw

test: check-am

# This is a really bad hack to make sure check_nrg and check_cue.sh
# are executable. Automake will remake check_nrg.sh and check_cue.sh
# but not run the configure default commands for them to make sure
# they are executable. You know it would be nice one could just set
# permissions and mode when it makes the files. I'm sure there's some
# cleaner a way to do this, but frankly I've wasted far too much of my
# life the crappy automess system that I've really lost interest in
# learning any more of this awful system than I need to.
check-am:	make-executable
make-executable: check_nrg.sh check_cue.sh check_paranoia.sh
	chmod +x *.sh
	if test ! -f cdda.bin ; then $(LN_S) $(srcdir)/cdda.bin cdda.bin ; fi
	if test ! -f isofs-m1.bin ; then $(LN_S) $(srcdir)/isofs-m1.bin isofs-m1.bin ; fi
