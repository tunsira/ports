COMMENT =		Unicode Character Database (UCD)

# XXX: make sure the major version of this port matches
#      x11/gnome/gucharmap
V =			15.0.0
DISTNAME =		UCD
PKGNAME =		unicode-ucd-$V
CATEGORIES =		textproc

HOMEPAGE =		https://www.unicode.org/ucd/

# https://www.unicode.org/copyright.html
PERMIT_PACKAGE =	Yes

MASTER_SITES =		https://www.unicode.org/Public/zipped/$V/
DIST_SUBDIR =		ucd/$V
DISTFILES =		${DISTNAME}${EXTRACT_SUFX} \
			Unihan${EXTRACT_SUFX}
EXTRACT_SUFX =		.zip

PKG_ARCH =		*

NO_BUILD =		Yes
NO_TEST =		Yes

WRKDIST =		${WRKDIR}

do-install:
	${INSTALL_DATA_DIR} ${PREFIX}/share/unicode/ucd/{auxiliary,extracted}/
	${INSTALL_DATA} ${WRKSRC}/*.{txt,html,pdf} ${PREFIX}/share/unicode/ucd/
	${INSTALL_DATA} ${WRKSRC}/auxiliary/* ${PREFIX}/share/unicode/ucd/auxiliary/
	${INSTALL_DATA} ${WRKSRC}/extracted/* ${PREFIX}/share/unicode/ucd/extracted/
	# Copy over the original Unihan zipfile as required by gucharmap
	${INSTALL_DATA} ${FULLDISTDIR}/Unihan${EXTRACT_SUFX} \
		${PREFIX}/share/unicode/ucd

.include <bsd.port.mk>
