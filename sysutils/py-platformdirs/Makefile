COMMENT=	determine appropriate platform-specific directories

MODPY_EGG_VERSION=	2.6.2
DISTNAME=	platformdirs-${MODPY_EGG_VERSION}
PKGNAME=	py-${DISTNAME}

CATEGORIES=	sysutils

HOMEPAGE=	https://github.com/platformdirs/platformdirs

# MIT
PERMIT_PACKAGE=	Yes

MODULES=	lang/python

MODPY_PI=	Yes
MODPY_PYBUILD=	hatch-vcs
MODPY_PYTEST=	Yes

TEST_DEPENDS=	devel/py-appdirs${MODPY_FLAVOR} \
		devel/py-test-mock${MODPY_FLAVOR}

FLAVORS=	python3
FLAVOR=		python3

post-install:
	rm ${WRKINST}${MODPY_SITEPKG}/platformdirs/unix.py${PATCHORIG}

.include <bsd.port.mk>
