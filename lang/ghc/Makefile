# Not yet ported to other architectures (i386 bootstrap recipe is broken).
ONLY_FOR_ARCHS =	amd64

COMMENT =		compiler for the functional language Haskell

DPB_PROPERTIES =	parallel

# ghc hardcodes ${WRKDIR}/bin/gcc when the package is compiled with ccache
NO_CCACHE =		Yes

# Upstream bug: https://gitlab.haskell.org/ghc/ghc/-/issues/22782
USE_NOEXECONLY =	Yes

GHC_VERSION =		9.2.6
REVISION =		0
DISTNAME =		ghc-${GHC_VERSION}
CATEGORIES =		lang devel
HOMEPAGE =		https://www.haskell.org/ghc/

# Version of the precompiled binaries
BIN_VER =		8.10.7.20220904

# lang/python needed for regression tests.
MODULES =		lang/python

MODPY_BUILDDEP =	No
MODPY_RUNDEP =		No

# BSD w/o advertising clause.
# Distfile is bundled with other stuff like libffi, mingw
# binaries, with BSD, GPLv2 and Perl artistic license.
PERMIT_PACKAGE =		Yes

WANTLIB += c curses ffi gmp iconv m pthread util

LIB_DEPENDS =		converters/libiconv \
			devel/gmp \
			devel/libffi

BUILD_DEPENDS =		archivers/bzip2 \
			archivers/gtar \
			textproc/py-sphinx${MODPY_FLAVOR}>=4.0.2
RUN_DEPENDS =

MASTER_SITES =		https://downloads.haskell.org/ghc/${GHC_VERSION}/
MASTER_SITES0 =		https://openbsd.dead-parrot.de/distfiles/

DIST_SUBDIR =		ghc

BINDISTFILE =		${BINDISTFILE-${MACHINE_ARCH}}

DISTFILES =		ghc-${GHC_VERSION}-src.tar.xz \
			ghc-${GHC_VERSION}-testsuite.tar.xz \
			${BINDISTFILE}

.for m in amd64
BINDISTFILE-$m =	ghc-${BIN_VER}-$m-unknown-openbsd.tar.xz:0 \
			ghc-${BIN_VER}-shlibs-$m.tar.gz:0
SUPDISTFILES +=		${BINDISTFILE-$m}
.endfor

# Substvars for all libraries, assuming that ghc-boot, ghc-boot-th,
# ghc-heap and ghci will always have the same version number as ghc.
GHC_ITEMS = \
	CABAL			3.6.3.0		 \
	ARRAY			0.5.4.0		 \
	BASE			4.16.4.0	 \
	BINARY			0.8.9.0		 \
	BYTESTRING		0.11.4.0	 \
	CONTAINERS		0.6.5.1		 \
	DEEPSEQ			1.4.6.1		 \
	DIRECTORY		1.3.6.2		 \
	EXCEPTIONS		0.10.4		 \
	FILEPATH		1.4.2.2		 \
	GHC			9.2.6		 \
	GHC_BIGNUM		1.2		 \
	GHC_COMPACT		0.1.0.0		 \
	GHC_PRIM		0.8.0		 \
	HASKELINE		0.8.2		 \
	HPC			0.6.1.0		 \
	INTEGER_GMP		1.1		 \
	MTL			2.2.2		 \
	PARSEC			3.1.15.0	 \
	PRETTY			1.1.3.6		 \
	PROCESS			1.6.16.0	 \
	STM			2.5.0.2		 \
	TEMPLATE-HASKELL	2.18.0.0	 \
	TERMINFO		0.4.1.5		 \
	TEXT			1.2.5.0		 \
	TIME			1.11.1.1	 \
	TRANSFORMERS		0.5.6.2		 \
	UNIX			2.7.2.2		 \
	XHTML			3000.2.2.1

.for _i _v in ${GHC_ITEMS}
${_i}_VER =	${_v}
SUBST_VARS +=	${_i}_VER
.endfor

USE_GMAKE =		Yes
USE_GROFF =		Yes

AUTOCONF_VERSION =	2.71
AUTOMAKE_VERSION =	1.16
CONFIGURE_STYLE =	gnu autoreconf no-autoheader
CONFIGURE_ARGS +=	--with-ffi-includes=${LOCALBASE}/include \
			--with-ffi-libraries=${LOCALBASE}/lib \
			--with-gmp-includes=${LOCALBASE}/include \
			--with-gmp-libraries=${LOCALBASE}/lib \
			--with-iconv-includes=${LOCALBASE}/include \
			--with-iconv-libraries=${LOCALBASE}/lib \
			--with-system-libffi \
			CC="${CC}"

CONFIGURE_ENV += SPHINXBUILD=${LOCALBASE}/bin/sphinx-build${MODPY_BIN_SUFFIX}

GHC_CC_OPTS =		-Wl,--no-execute-only -Qunused-arguments
CONFIGURE_ENV +=	CONF_GCC_LINKER_OPTS_STAGE0="${GHC_CC_OPTS}" \
			CONF_GCC_LINKER_OPTS_STAGE1="${GHC_CC_OPTS}" \
			CONF_GCC_LINKER_OPTS_STAGE2="${GHC_CC_OPTS}" \
			CONF_CC_OPTS_STAGE2="${GHC_CC_OPTS}"

# Do not pick up gpatch
CONFIGURE_ENV +=	ac_cv_path_PatchCmd=/usr/bin/patch

MAKE_FLAGS +=		StripLibraries=YES \
			INSTALL_BIN_OPTS=-s \
			HSCOLOUR_SRCS=NO \
			BUILD_SPHINX_PDF=NO

# haddock: ... <stdout>: commitBuffer: invalid argument (invalid character)
MAKE_ENV =	LC_ALL=en_US.UTF-8

# For mktexpk (via dvips when building the PostScript documentation):
PORTHOME =		${WRKDIR}

TEST_DEPENDS =	print/ghostscript/gnu ${MODPY_RUN_DEPENDS}

post-extract:
	cd ${WRKSRC} && ${AUTOCONF_ENV} ./boot
	cd ${WRKSRC}/libraries/unix && \
	mkdir -p System/OpenBSD && \
	install -m 644 ${FILESDIR}/Process.hsc System/OpenBSD

BOOTSTRAP_SHLIBS =	${WRKDIR}/ghc-${BIN_VER}-shlibs-${MACHINE_ARCH}

post-patch:
	cd ${WRKDIR}/ghc-${BIN_VER} && \
	LD_LIBRARY_PATH=${BOOTSTRAP_SHLIBS} \
	CONFIGURE_ENV=${CONFIGURE_ENV} \
	./configure --prefix=${WRKDIR}/bootstrap CC="${CC}" && \
	LD_LIBRARY_PATH=${BOOTSTRAP_SHLIBS} \
	${MAKE_PROGRAM} install
	rm -rf ${WRKDIR}/ghc-${BIN_VER}
# - Create some wrapper scripts setting LD_LIBRARY_PATH
	cd ${WRKDIR}/bin && \
	for f in $$(ls ../bootstrap/bin); do \
		${INSTALL_SCRIPT} /dev/null $$f && \
		exec > $$f && \
		echo '#!/bin/sh' && \
		echo 'LD_LIBRARY_PATH=${BOOTSTRAP_SHLIBS} \' && \
		printf 'exec ${WRKDIR}/bootstrap/bin/%s "$$@"\n' "$$f"; \
	done
	cp ${WRKSRC}/mk/build.mk{.sample,}
	echo libraries/base_CONFIGURE_OPTS+=--configure-option=--with-libcharset=no >> ${WRKSRC}/mk/build.mk
	echo HADDOCK_DOCS=YES >> ${WRKSRC}/mk/build.mk

do-test:
	ulimit -c 0 -n 1024 && \
	cd ${WRKSRC}/testsuite/tests && \
	exec ${SETENV} ${MAKE_ENV} LC_CTYPE=en_US.UTF-8 \
		${MAKE_PROGRAM} ${MAKE_FLAGS} \
		PYTHON="${MODPY_BIN}"



# It doesn't matter whether this is the actual date of the bootstrapper
# build. It's just used to get different distfiles whenever new
# bootstrappers have to be built.
BOOTSTRAP_DATE =	20220830

# Create a bootstrapper. This compiles a stripped-down version of
# ghc and creates a `bindist', i.e. a tarball with binaries that
# can be used for bootstrapping.
bootstrap: patch
	@if [ ! -x ${LOCALBASE}/bin/autoconf-${AUTOCONF_VERSION} ]; then \
		echo Please install autoconf-${AUTOCONF_VERSION}.; \
		false; \
	fi
	@if [ ! -x ${LOCALBASE}/bin/automake-${AUTOMAKE_VERSION} ]; then \
		echo Please install automake-${AUTOMAKE_VERSION}; \
		false; \
	fi

	$(_PBUILD) $(MAKE) _bootstrap_prepare

	env CONFIGURE_ENV=RELEASE=NO ${MAKE} configure

	${MAKE} build ALL_TARGET="all binary-dist" \
		AUTOCONF_VERSION=${AUTOCONF_VERSION} AUTOMAKE_VERSION=${AUTOMAKE_VERSION}

	$(_PBUILD) $(MAKE) _bootstrap_finish

_bootstrap_prepare:
	cp ${FILESDIR}/bootstrap.mk ${WRKSRC}/mk/build.mk
	echo ${BOOTSTRAP_DATE} > ${WRKSRC}/VERSION_DATE

_bootstrap_finish:
	mkdir -p ${WRKBUILD}/ghc-${GHC_VERSION}.${BOOTSTRAP_DATE}-shlibs-$$(arch -s)
	ldd ${WRKBUILD}/ghc/stage2/build/tmp/ghc-stage2 | \
	awk '$$NF ~ /^\/usr\/(local\/)?lib\// { print $$NF }' | \
	xargs -J % cp -p % ${WRKBUILD}/ghc-${GHC_VERSION}.${BOOTSTRAP_DATE}-shlibs-$$(arch -s)
	cd ${WRKBUILD} && \
	pax -wzf ghc-${GHC_VERSION}.${BOOTSTRAP_DATE}-shlibs-$$(arch -s){.tar.gz,}

.include <bsd.port.mk>
