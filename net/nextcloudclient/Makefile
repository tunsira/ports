USE_WXNEEDED =	Yes

COMMENT =	desktop sync client for Nextcloud

V =		3.6.6
DISTNAME =	nextcloudclient-${V}

GH_ACCOUNT =	nextcloud
GH_PROJECT =	desktop
GH_TAGNAME =	v${V}

CATEGORIES =	net

HOMEPAGE =	https://nextcloud.com

SHARED_LIBS +=  nextcloudsync             8.1 # 3.6.6
SHARED_LIBS +=  nextcloud_csync           2.2 # 3.6.0
SHARED_LIBS +=  nextcloudsync_vfs_suffix  0.1 # 3.6.6

MAINTAINER =	Adriano Barbosa <barbosa.aob@gmail.com>

# GPLv2+
PERMIT_PACKAGE =	Yes

WANTLIB += ${COMPILER_LIBCXX} lib/inotify/inotify
WANTLIB += Qt5Concurrent Qt5Core Qt5DBus Qt5Gui Qt5Network Qt5Positioning
WANTLIB += Qt5PrintSupport Qt5Qml Qt5QmlModels Qt5Quick Qt5QuickControls2
WANTLIB += Qt5Svg Qt5WebChannel Qt5WebEngineCore Qt5WebEngineWidgets
WANTLIB += Qt5WebSockets Qt5Widgets Qt5Xml c crypto m qt5keychain
WANTLIB += sqlite3 ssl z

MODULES =		devel/cmake \
			x11/qt5

BUILD_DEPENDS =		devel/gettext,-tools \
			x11/gnome/libcloudproviders

# for converting svg icons to png
BUILD_DEPENDS +=	x11/gnome/librsvg

# for tests, but detected during configure
BUILD_DEPENDS +=	devel/cmocka

RUN_DEPENDS =		devel/desktop-file-utils \
			misc/shared-mime-info \
			x11/gnome/libcloudproviders \
			x11/gtk+3,-guic \
			x11/qt5/qtgraphicaleffects \
			x11/qt5/qtquickcontrols

LIB_DEPENDS =		databases/sqlite3 \
			devel/libinotify \
			security/qtkeychain \
			x11/qt5/qtsvg \
			x11/qt5/qtquickcontrols2 \
			x11/qt5/qtwebengine \
			x11/qt5/qtwebsockets

CONFIGURE_ARGS =	-DBUILD_SHELL_INTEGRATION_NAUTILUS=OFF \
			-DBUILD_SHELL_INTEGRATION_DOLPHIN=OFF \
			-DBUILD_SHELL_INTEGRATION=OFF \
			-DUNIT_TESTING=ON \
			-DWITH_CRASHREPORTER=OFF

# Disable Doxygen
CONFIGURE_ARGS +=	-DCMAKE_DISABLE_FIND_PACKAGE_Doxygen=ON

# Disable SharedMime
CONFIGURE_ARGS +=	-DCMAKE_DISABLE_FIND_PACKAGE_SharedMimeInfo=ON

# Do not install under /etc/Nextcloud
CONFIGURE_ARGS +=	-DSYSCONF_INSTALL_DIR=${SYSCONFDIR}

CFLAGS +=	-I${LOCALBASE}/include -I${LOCALBASE}/include/inotify -I${LOCALBASE}/include/qtkeychain
CXXFLAGS +=	-I${LOCALBASE}/include -I${LOCALBASE}/include/inotify -I${LOCALBASE}/include/qtkeychain
MODCMAKE_LDFLAGS =	-L${LOCALBASE}/lib -L${LOCALBASE}/lib/inotify -linotify -Wl,-rpath=${LOCALBASE}/lib/inotify

post-install:
	${INSTALL_DATA_DIR} ${PREFIX}/share/examples/Nextcloud/
	mv ${WRKINST}/etc/Nextcloud ${PREFIX}/share/examples/

.include <bsd.port.mk>
