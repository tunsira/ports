COMMENT =	global desktop keyboard shortcuts for KDE
DISTNAME =	kglobalaccel-${VERSION}

SHARED_LIBS =	KF5GlobalAccel		6.3
SHARED_LIBS +=	KF5GlobalAccelPrivate	6.3

WANTLIB += ${COMPILER_LIBCXX} KF5ConfigCore KF5CoreAddons KF5Crash
WANTLIB += KF5DBusAddons KF5WindowSystem Qt5Core Qt5DBus Qt5Gui
WANTLIB += Qt5Widgets Qt5X11Extras X11 c m xcb xcb-keysyms xcb-record
WANTLIB += xcb-xkb

LIB_DEPENDS =	devel/kf5/kconfig>=${MODKF5_VERSION} \
		devel/kf5/kcoreaddons>=${MODKF5_VERSION} \
		devel/kf5/kcrash>=${MODKF5_VERSION} \
		devel/kf5/kdbusaddons>=${MODKF5_VERSION} \
		devel/kf5/kwindowsystem>=${MODKF5_VERSION} \
		x11/qt5/qtx11extras

TEST_IS_INTERACTIVE =	X11

.include <bsd.port.mk>
