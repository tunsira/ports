COMMENT =		static site generator written in Python

MODPY_EGG_VERSION =	${GH_TAGNAME}
DISTNAME =		pelican-${MODPY_EGG_VERSION}
REVISION =		1

GH_ACCOUNT =		getpelican
GH_PROJECT =		pelican
GH_TAGNAME =		4.7.2

CATEGORIES =		www

HOMEPAGE =		https://blog.getpelican.com/
MAINTAINER =		David Demelier <markand@malikania.fr>

# GPLv3
PERMIT_PACKAGE =	Yes

MODULES =		lang/python
MODPY_PYBUILD =		setuptools

RUN_DEPENDS =		devel/py-blinker${MODPY_FLAVOR} \
			devel/py-dateutil${MODPY_FLAVOR} \
			devel/py-rich${MODPY_FLAVOR} \
			devel/py-tz${MODPY_FLAVOR} \
			textproc/py-markdown${MODPY_FLAVOR} \
			textproc/py-docutils${MODPY_FLAVOR} \
			textproc/py-pygments${MODPY_FLAVOR} \
			textproc/py-unidecode${MODPY_FLAVOR} \
			www/py-feedgenerator${MODPY_FLAVOR} \
			www/py-jinja2${MODPY_FLAVOR}

# Else setuptools skips filenames containing UTF8 chars
MAKE_ENV +=		LC_CTYPE=en_US.UTF-8

TEST_DEPENDS =		${RUN_DEPENDS} \
			devel/git

pre-configure:
	${SUBST_CMD} ${WRKSRC}/pelican/tests/test_pelican.py

.include <bsd.port.mk>
