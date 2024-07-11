PORTNAME=			anki
DISTVERSION=		24.06.3
CATEGORIES=			www
MASTER_SITES=		GH
PKGNAMESUFFIX=		-api
PKGNAMESUFFIX=		-sync-server
DISTNAME=			${DISTVERSIONPREFIX}${DISTVERSION}

MAINTAINER=			public@fzwte.net
COMMENT=			Sync server for spaced repetition program Anki
WWW=				https://apps.ankiweb.net

LICENSE=			AGPLv3
LICENSE_FILE=		${WRKSRC}/LICENSE

BUILD_DEPENDS=		protobuf>0:devel/protobuf
LIB_DEPENDS=		libzstd.so:archivers/zstd

USES=				cargo ssl
CARGO_BUILD_ARGS=	--bin anki-sync-server
CARGO_INSTALL_PATH=	rslib/sync
USE_GITHUB=			yes
GH_ACCOUNT=			ankitects
GH_PROJECT=			anki
GH_TUPLE=			ankitects:anki-desktop-ftl:469ea37:anki_desktop_ftl/ftl/qt-repo \
					ankitects:anki-core-i18n:173f0438:anki_core_i18n/ftl/core-repo
MAKE_ENV+=			PROTOC_BINARY=/usr/local/bin/protoc

ANKI_USER=			${PORTNAME}
ANKI_GROUP=			${PORTNAME}

USERS=				${ANKI_USER}
GROUPS=				${ANKI_GROUP}

USE_RC_SUBR=		anki-sync-server

post-install:
	${MKDIR} ${STAGEDIR}/var/db/anki
	${MKDIR} ${STAGEDIR}/var/run/anki
	${MKDIR} ${STAGEDIR}/var/log/anki

.include <bsd.port.mk>
