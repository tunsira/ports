COMMENT =			retrieve and process nzb-files via web interface

VERSION =			3.7.2
DISTNAME =			SABnzbd-${VERSION}
PKGNAME =			sabnzbd-${VERSION}

CATEGORIES =			news

HOMEPAGE =			https://sabnzbd.org/

MAINTAINER =			Bjorn Ketelaars <bket@openbsd.org>

# GPLv2
PERMIT_PACKAGE =		Yes

MASTER_SITES =			https://github.com/sabnzbd/sabnzbd/releases/download/${VERSION}/
EXTRACT_SUFX =			-src.tar.gz

MODULES =			lang/python
# XXX broken, needs pyfakefs, pytest-httpserver, tavern and tavalidate (not in
# ports)
MODPY_PYTEST =			Yes

BUILD_DEPENDS =			${_MODPY_BUILD_DEPENDS}
RUN_DEPENDS =			archivers/par2cmdline \
				archivers/unrar \
				archivers/unzip \
				devel/py-cheetah${MODPY_FLAVOR}>=3.0.0 \
				devel/py-configobj${MODPY_FLAVOR} \
				devel/py-puremagic${MODPY_FLAVOR} \
				multimedia/py-guessit${MODPY_FLAVOR} \
				net/py-portend${MODPY_FLAVOR} \
				net/py-socks${MODPY_FLAVOR} \
				news/py-sabyenc${MODPY_FLAVOR}>=5.4.4v0 \
				security/py-cryptography${MODPY_FLAVOR} \
				textproc/py-chardet${MODPY_FLAVOR} \
				textproc/py-feedparser${MODPY_FLAVOR} \
				www/py-CherryPy${MODPY_FLAVOR} \
				www/py-cheroot${MODPY_FLAVOR}
TEST_DEPENDS =			devel/py-flaky${MODPY_FLAVOR} \
				devel/py-test-httpbin${MODPY_FLAVOR} \
				textproc/py-lxml${MODPY_FLAVOR} \
				textproc/py-xmltodict${MODPY_FLAVOR} \
				www/py-requests${MODPY_FLAVOR} \
				www/py-selenium${MODPY_FLAVOR}

NO_BUILD =			Yes

do-install:
	${INSTALL_DATA_DIR} \
	    ${PREFIX}/lib/python${MODPY_VERSION}/site-packages/sabnzbd
	cp -Rp ${WRKSRC}/* \
	    ${PREFIX}/lib/python${MODPY_VERSION}/site-packages/sabnzbd
	rm -rf ${PREFIX}/lib/python${MODPY_VERSION}/site-packages/sabnzbd/tests
	${SUBST_CMD} -m 555 -c ${FILESDIR}/sabnzbd ${WRKSRC}/sabnzbd/sabnzbd
	${INSTALL_SCRIPT} ${WRKSRC}/sabnzbd/sabnzbd ${PREFIX}/bin/sabnzbd
	chown -R ${BINOWN}:${BINGRP} \
	    ${PREFIX}/lib/python${MODPY_VERSION}/site-packages/sabnzbd

post-install:
	${MODPY_BIN} ${MODPY_LIBDIR}/compileall.py \
	    ${PREFIX}/lib/python${MODPY_VERSION}/site-packages/sabnzbd

.include <bsd.port.mk>
