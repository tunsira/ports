COMMENT =	tiny embeddable httpd library written in C
DISTNAME =	libmicrohttpd-0.9.70
REVISION =	0
CATEGORIES =	www

SHARED_LIBS +=	microhttpd                0.4 # 65.0

HOMEPAGE =	https://www.gnu.org/software/libmicrohttpd/
MAINTAINER =	Brian Callahan <bcallah@openbsd.org>

# LGPLv2.1+
PERMIT_PACKAGE =	Yes

WANTLIB += brotlidec brotlienc gmp gnutls hogweed iconv idn2 intl
WANTLIB += nettle p11-kit pthread tasn1 unistring z zstd

MASTER_SITES =	${MASTER_SITE_GNU:=libmicrohttpd/}

DEBUG_PACKAGES =	${BUILD_PACKAGES}

CONFIGURE_STYLE =	gnu

# Checks these during configure but used only in testing.
BUILD_DEPENDS =	${TEST_DEPENDS}

LIB_DEPENDS =	security/gnutls

TEST_DEPENDS =	misc/zzuf \
		net/curl \
		net/socat

.include <bsd.port.mk>
