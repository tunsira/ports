COMMENT =	Python implementation of SGP4 satellite tracking algorithm

MODPY_EGG_VERSION =	2.21

DISTNAME =	sgp4-${MODPY_EGG_VERSION}
PKGNAME =	py-${DISTNAME}
REVISION =	0

CATEGORIES =	astro

HOMEPAGE =	https://github.com/brandon-rhodes/python-sgp4

# MIT
PERMIT_PACKAGE =	Yes

WANTLIB += ${COMPILER_LIBCXX} m

COMPILER =	base-clang ports-gcc

FLAVORS =	python3
FLAVOR =	python3

MODULES =	lang/python

MODPY_PI =	Yes
MODPY_PYTEST_ARGS = sgp4/tests.py

RUN_DEPENDS =	math/py-numpy${MODPY_FLAVOR}

.include <bsd.port.mk>
