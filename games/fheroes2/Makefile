COMMENT =	engine recreation for Heroes of Might and Magic 2

GH_ACCOUNT =	ihhub
GH_PROJECT =	fheroes2
GH_TAGNAME =	1.0.0
CATEGORIES =	games
HOMEPAGE =	https://ihhub.github.io/fheroes2/
MAINTAINER =	Thomas Frohwein <thfr@openbsd.org>

# GPLv2.0+, LGPLv2.1+ (src/thirdparty/libsmacker)
PERMIT_PACKAGE =	Yes

WANTLIB += ${COMPILER_LIBCXX} SDL2 SDL2_mixer c m z

# C++11
COMPILER =	base-clang ports-gcc

BUILD_DEPENDS =	devel/gettext,-tools \
		textproc/gsed
LIB_DEPENDS =	devel/sdl2-mixer
RUN_DEPENDS =	audio/timidity
MAKE_FLAGS +=	FHEROES2_DATA=${PREFIX}/share/fheroes2
USE_GMAKE =	Yes
NO_TEST =	Yes
PATCHORIG =	.orig.port

# needs gsed
do-gen:
	sed -Ei 's,([[:blank:]])sed,\1gsed,g' \
		${WRKSRC}/files/lang/Makefile

do-install:
	${INSTALL_DATA_DIR} ${PREFIX}/share/fheroes2/files/data
	${INSTALL_DATA}	${WRKSRC}/files/data/resurrection.h2d \
			${PREFIX}/share/fheroes2/files/data/
	${INSTALL_DATA_DIR} ${PREFIX}/share/fheroes2/files/lang
	cp ${WRKBUILD}/files/lang/*.mo \
		${PREFIX}/share/fheroes2/files/lang/
	${INSTALL_PROGRAM} ${WRKBUILD}/fheroes2 ${PREFIX}/bin/
	${INSTALL_SCRIPT} ${WRKBUILD}/script/demo/download_demo_version.sh \
		${PREFIX}/share/fheroes2/download_demo_version.sh
	${INSTALL_SCRIPT} ${WRKBUILD}/script/homm2/extract_homm2_resources.sh \
		${PREFIX}/share/fheroes2/extract_homm2_resources.sh

.include <bsd.port.mk>
