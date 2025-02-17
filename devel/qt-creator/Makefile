USE_WXNEEDED =		Yes

COMMENT =		cross-platform IDE for use with Qt

V =			8.0.2
DISTNAME =		qt-creator-opensource-src-${V}
PKGNAME =		qt-creator-${V}
REVISION =		1

SHARED_LIBS +=  Aggregation               1.1 # 0.0
SHARED_LIBS +=  CPlusPlus                 6.0 # 0.0
SHARED_LIBS +=  ExtensionSystem           6.1 # 0.0
SHARED_LIBS +=  GLSL                      1.1 # 0.0
SHARED_LIBS +=  LanguageUtils             1.1 # 0.0
SHARED_LIBS +=  QmlDebug                  5.0 # 0.0
SHARED_LIBS +=  QmlEditorWidgets          1.1 # 0.0
SHARED_LIBS +=  QmlJS                     9.1 # 0.0
SHARED_LIBS +=  QtcSsh                    2.0 # 0.0
SHARED_LIBS +=  Utils                     10.1 # 0.0
SHARED_LIBS +=  Sqlite                    7.1 # 1.0
SHARED_LIBS +=  Modeling                  6.1 # 1.0
SHARED_LIBS +=  ClangSupport              2.0 # 4.5
SHARED_LIBS +=  Tracing                   2.1 # 4.7
SHARED_LIBS +=  LanguageServerProtocol    5.0 # 4.8
SHARED_LIBS +=  AdvancedDockingSystem     1.1 # 4.12
SHARED_LIBS +=  qlitehtml                 1.1 # 4.15
SHARED_LIBS +=  ProParser                 1.1 # 4.15

CATEGORIES =	devel editors

HOMEPAGE =	https://www.qt.io/ide/

MAINTAINER =	Rafael Sadowski <rsadowski@openbsd.org>

# GPLv3 with the "Qt Company GPL Exception 1.0"
PERMIT_PACKAGE =	Yes

WANTLIB += ${COMPILER_LIBCXX} KF5SyntaxHighlighting Qt5Concurrent
WANTLIB += Qt5Core Qt5Designer Qt5DesignerComponents Qt5Gui Qt5Help
WANTLIB += Qt5Network Qt5Positioning Qt5PrintSupport Qt5Qml Qt5QmlModels
WANTLIB += Qt5Quick Qt5QuickWidgets Qt5SerialPort Qt5Sql Qt5Svg
WANTLIB += Qt5Test Qt5WebChannel Qt5WebEngineCore Qt5WebEngineWidgets
WANTLIB += Qt5Widgets Qt5Xml c m yaml-cpp

MASTER_SITES =	https://download.qt.io/official_releases/qtcreator/${V:R}/${V}/ \
		https://mirrors.ocf.berkeley.edu/qt/official_releases/qtcreator/${V:R}/${V}/

MODULES =	x11/qt5 \
		lang/python \
		devel/cmake

CONFIGURE_STYLE = cmake

BUILD_DEPENDS =	devel/clang-tools-extra \
		devel/llvm \
		lang/clazy \
		x11/qt5/qtquickcontrols

RUN_DEPENDS =	devel/clang-tools-extra \
		devel/desktop-file-utils \
		devel/gdb \
		devel/gmake \
		devel/llvm \
		lang/clazy \
		x11/gtk+3,-guic \
		x11/qt5/qtquickcontrols

LIB_DEPENDS =	devel/kf5/syntax-highlighting \
		devel/yaml-cpp \
		x11/qt5/qtdeclarative \
		x11/qt5/qtserialport \
		x11/qt5/qtsvg \
		x11/qt5/qttools \
		x11/qt5/qtwebchannel \
		x11/qt5/qtwebengine

CONFIGURE_ARGS =	-DBUILD_CPLUSPLUS_TOOLS=ON \
			-DENABLE_SVG_SUPPORT=ON \
			-DBUILD_WITH_PCH=OFF \
			-DCMAKE_DISABLE_FIND_PACKAGE_Qt6=ON

GDB_ADJ_FILES = \
	src/plugins/debugger/debuggeritemmanager.cpp \
	src/tools/qtcreatorcrashhandler/backtracecollector.cpp \
	src/tools/qtpromaker/main.cpp \
	tests/auto/debugger/tst_dumpers.cpp \
	tests/system/suite_general/tst_openqt_creator/testdata/projecttree_creator.tsv

CFLAGS +=	-I${LOCALBASE}/include/KF5/KSyntaxHighlighting/KSyntaxHighlighting
CXXFLAGS +=	-I${LOCALBASE}/include/KF5/KSyntaxHighlighting/KSyntaxHighlighting
MODCMAKE_LDFLAGS +=	-lc

pre-configure:
	cd ${WRKSRC}; sed -i 's,"gdb","egdb",g' ${GDB_ADJ_FILES}
	# use system qbs/syntax-highlighting (qtcreator.pro)
	rm -rf ${WRKSRC}/src/shared/qbs

post-install:
.for _l _v in ${SHARED_LIBS}
	ln -sf qtcreator/lib${_l}.so.${_v} ${PREFIX}/lib
.endfor
	${MODPY_BIN} ${MODPY_LIBDIR}/compileall.py \
		${PREFIX}/share/qtcreator/debugger/

.include <bsd.port.mk>
