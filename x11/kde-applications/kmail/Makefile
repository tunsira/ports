USE_WXNEEDED =	Yes

COMMENT =	KDE PIM email client
DISTNAME =	kmail-${VERSION}
CATEGORIES =	net mail

SHARED_LIBS +=  kmailprivate       5.2 # 5.13.2

WANTLIB += ${COMPILER_LIBCXX} Grantlee_Templates KF5AkonadiAgentBase
WANTLIB += KF5AkonadiContact KF5AkonadiCore KF5AkonadiMime KF5AkonadiSearchDebug
WANTLIB += KF5AkonadiSearchPIM KF5AkonadiWidgets KF5Auth KF5AuthCore
WANTLIB += KF5Bookmarks KF5CalendarCore KF5CalendarUtils KF5Codecs
WANTLIB += KF5Completion KF5ConfigCore KF5ConfigGui KF5ConfigWidgets
WANTLIB += KF5Contacts KF5CoreAddons KF5Crash KF5DBusAddons KF5GrantleeTheme
WANTLIB += KF5Gravatar KF5GuiAddons KF5I18n KF5IMAP KF5IconThemes
WANTLIB += KF5IdentityManagement KF5IdentityManagementWidgets
WANTLIB += KF5ItemModels KF5ItemViews KF5JobWidgets KF5KCMUtils
WANTLIB += KF5KIOCore KF5KIOFileWidgets KF5KIOGui KF5KIOWidgets
WANTLIB += KF5KManageSieve KF5KSieve KF5KSieveUi KF5KontactInterface
WANTLIB += KF5Ldap KF5Libkdepim KF5Libkleo KF5MailCommon KF5MailTransport
WANTLIB += KF5MailTransportAkonadi KF5MessageComposer KF5MessageCore
WANTLIB += KF5MessageList KF5MessageViewer KF5Mime KF5MimeTreeParser
WANTLIB += KF5Notifications KF5NotifyConfig KF5Parts KF5PimCommon
WANTLIB += KF5PimCommonAkonadi KF5PimCommonAutoCorrection KF5PimTextEdit
WANTLIB += KF5Service KF5Solid KF5SonnetUi KF5SyntaxHighlighting
WANTLIB += KF5TemplateParser KF5TextWidgets KF5Tnef KF5Wallet
WANTLIB += KF5WebEngineViewer KF5WidgetsAddons KF5WindowSystem
WANTLIB += KF5XmlGui KUserFeedbackCore KUserFeedbackWidgets Qt5Concurrent
WANTLIB += Qt5Core Qt5DBus Qt5Gui Qt5Network Qt5Positioning Qt5PrintSupport
WANTLIB += Qt5Qml Qt5QmlModels Qt5Quick Qt5WebChannel Qt5WebEngineCore
WANTLIB += Qt5WebEngineWidgets Qt5Widgets Qt5Xml X11 assuan c
WANTLIB += gpgme gpgmepp m qgpgme qt5keychain

WANTLIB += lib/inotify/inotify

MODKDE5_ICON_CACHE = yes
MODKDE5_TRANSLATIONS = yes
MODKDE5_DESKTOP_FILE = yes
MODKDE5_DOCS = yes

MODKF5_L10N_CONFLICT = yes
MODKF5_I18N_CONFLICT = yes

BUILD_DEPENDS =	devel/boost

RUN_DEPENDS =	x11/kde-applications/akonadi-import-wizard \
		x11/kde-applications/kdepim-runtime \
		x11/kde-applications/kmail-account-wizard \
		x11/kde-applications/mbox-importer \
		x11/kde-applications/pim-sieve-editor

LIB_DEPENDS =	devel/kf5/kauth \
		devel/kf5/kbookmarks \
		devel/kf5/kcalendarcore \
		devel/kf5/kcmutils \
		devel/kf5/kcodecs \
		devel/kf5/kcompletion \
		devel/kf5/kconfig \
		devel/kf5/kconfigwidgets \
		devel/kf5/kcontacts \
		devel/kf5/kcoreaddons \
		devel/kf5/kcrash \
		devel/kf5/kdbusaddons \
		devel/kf5/kguiaddons \
		devel/kf5/ki18n \
		devel/kf5/kiconthemes \
		devel/kf5/kio \
		devel/kf5/kitemmodels \
		devel/kf5/kitemviews \
		devel/kf5/kjobwidgets \
		devel/kf5/knotifications \
		devel/kf5/knotifyconfig \
		devel/kf5/kparts \
		devel/kf5/kservice \
		devel/kf5/ktextwidgets \
		devel/kf5/kwallet \
		devel/kf5/kwidgetsaddons \
		devel/kf5/kwindowsystem \
		devel/kf5/kxmlgui \
		devel/kf5/solid \
		devel/kf5/sonnet \
		devel/kf5/syntax-highlighting \
		devel/libinotify \
		security/gpgme,-qt \
		productivity/kuserfeedback \
		x11/kde-applications/akonadi \
		x11/kde-applications/akonadi-contacts \
		x11/kde-applications/akonadi-mime \
		x11/kde-applications/akonadi-search \
		x11/kde-applications/kcalutils \
		x11/kde-applications/kidentitymanagement \
		x11/kde-applications/kimap \
		x11/kde-applications/kldap \
		x11/kde-applications/kmailtransport \
		x11/kde-applications/kmime \
		x11/kde-applications/kontactinterface \
		x11/kde-applications/kpimtextedit \
		x11/kde-applications/ktnef \
		x11/kde-applications/libgravatar \
		x11/kde-applications/libkdepim \
		x11/kde-applications/libkleo \
		x11/kde-applications/libksieve \
		x11/kde-applications/mailcommon \
		x11/kde-applications/messagelib \
		x11/kde-applications/pimcommon \
		x11/qt5/qtdeclarative \
		x11/qt5/qtlocation \
		x11/qt5/qtwebchannel \
		x11/qt5/qtwebengine

TEST_IS_INTERACTIVE =	X11

CXXFLAGS +=	-I${LOCALBASE}/include/KF5/MessageViewer

.include <bsd.port.mk>
