COMMENT=	universal charset detection library and tool

DISTNAME=	uchardet-0.0.8
EXTRACT_SUFX=	.tar.xz

SHARED_LIBS +=	uchardet                  0.1

CATEGORIES=	textproc

HOMEPAGE=	https://www.freedesktop.org/wiki/Software/uchardet/

# MPL 1.1
PERMIT_PACKAGE=	Yes

WANTLIB += c m ${COMPILER_LIBCXX}

COMPILER=	base-clang ports-gcc base-gcc

MASTER_SITES=	https://www.freedesktop.org/software/uchardet/releases/

MODULES=	devel/cmake
CONFIGURE_ARGS=	-DCMAKE_INSTALL_MANDIR="${PREFIX}/man"

DEBUG_PACKAGES=	${BUILD_PACKAGES}

.include <bsd.port.mk>
