COMMENT =		shell script analysis tool

MODCABAL_STEM =		ShellCheck
MODCABAL_VERSION =	0.9.0
MODCABAL_EXECUTABLES =	shellcheck
PKGNAME =		${DISTNAME:L}
CATEGORIES =		devel
HOMEPAGE =		https://www.shellcheck.net/
REVISION =		0

MAINTAINER =		Caspar Schutijser <caspar@schutijser.com>

# GPLv3
PERMIT_PACKAGE =	Yes

WANTLIB =		c ffi gmp iconv m pthread util

# cabal-bundler --openbsd ShellCheck-0.9.0 --executable shellcheck
MODULES =		devel/cabal
MODCABAL_MANIFEST	= \
	Diff	0.4.1	0	\
	OneTuple	0.3.1	3	\
	QuickCheck	2.14.2	0	\
	StateVar	1.2.2	0	\
	aeson	2.1.1.0	0	\
	assoc	1.0.2	3	\
	attoparsec	0.14.4	2	\
	base-compat	0.12.2	0	\
	base-compat-batteries	0.12.2	0	\
	base-orphans	0.8.7	0	\
	bifunctors	5.5.14	0	\
	comonad	5.0.8	1	\
	contravariant	1.5.5	0	\
	data-fix	0.3.2	3	\
	distributive	0.6.2.1	1	\
	dlist	1.0	0	\
	fgl	5.8.0.0	0	\
	generically	0.1	0	\
	hashable	1.4.1.0	0	\
	indexed-traversable	0.1.2	2	\
	indexed-traversable-instances	0.1.1.1	0	\
	integer-logarithms	1.0.3.1	3	\
	primitive	0.7.4.0	0	\
	random	1.2.1.1	0	\
	regex-base	0.94.0.2	1	\
	regex-tdfa	1.3.2	0	\
	scientific	0.3.7.0	3	\
	semialign	1.2.0.1	3	\
	semigroupoids	5.3.7	0	\
	splitmix	0.1.0.4	1	\
	strict	0.4.0.1	4	\
	tagged	0.8.6.1	3	\
	text-short	0.1.5	1	\
	th-abstraction	0.4.5.0	0	\
	these	1.1.1.1	6	\
	time-compat	1.9.6.1	4	\
	transformers-compat	0.7.2	0	\
	unordered-containers	0.2.19.1	1	\
	uuid-types	1.0.5	3	\
	vector	0.13.0.0	1	\
	vector-stream	0.1.0.0	1	\
	witherable	0.4.2	3

LIB_DEPENDS =		converters/libiconv \
			devel/gmp \
			devel/libffi
RUN_DEPENDS-main =

NO_TEST =		Yes

# pkg_add pandoc; cd ${WRKSRC}; ./manpage; cp shellcheck.1 ${FILESDIR}/
# (and update md5)
post-patch:
	@[ `md5 < ${WRKSRC}/shellcheck.1.md` == f06c4a4f31f71dee0aa6b1890e469d5d ] || \
	    (echo "*** manpage changed; regenerate ${FILESDIR}/shellcheck.1"; sleep 3)

post-install:
	${INSTALL_DATA} ${FILESDIR}/shellcheck.1 ${PREFIX}/man/man1/

.include <bsd.port.mk>
