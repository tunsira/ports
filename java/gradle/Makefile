COMMENT =	build automation tool

DISTNAME =	gradle-6.7
EXTRACT_SUFX =	-bin.zip
EPOCH =		0

CATEGORIES =	java

HOMEPAGE =	https://gradle.org/

MAINTAINER =	Lawrence Teo <lteo@openbsd.org>

# Apache 2.0
PERMIT_PACKAGE =	Yes

MASTER_SITES =		https://services.gradle.org/distributions/

MODULES =		java
MODJAVA_VER =		1.8+

NO_BUILD =		Yes
NO_TEST =		Yes

GRADLE_JAR =		${DISTNAME:S/gradle//}.jar
SUBST_VARS +=		GRADLE_JAR

RUN_DEPENDS =		java/javaPathHelper

do-install:
	${INSTALL_DATA_DIR} ${PREFIX}/share/java/gradle
	cp -r ${WRKSRC}/* ${PREFIX}/share/java/gradle/
	ln -s ${TRUEPREFIX}/share/java/gradle/bin/gradle ${PREFIX}/bin/gradle

.include <bsd.port.mk>
