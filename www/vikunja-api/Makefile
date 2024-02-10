PORTNAME=			vikunja
DISTVERSIONPREFIX=	v
DISTVERSION=		0.22.1
CATEGORIES=			www
MASTER_SITES=		GH
PKGNAMESUFFIX=		-api
DISTNAME=			${DISTVERSIONPREFIX}${DISTVERSION}

MAINTAINER=			public@fzwte.net
COMMENT=			Todo-app to organize your life
WWW=				https://vikunja.io

LICENSE=			AGPLv3
LICENSE_FILE=		${WRKSRC}/LICENSE

ONLY_FOR_ARCHS=		aarch64 amd64 armv6 armv7 i386

USES=				go:1.21,modules

VIKUNJA_USER=		vikunja
VIKUNJA_GROUP=		vikunja

USERS=				${VIKUNJA_USER}
GROUPS=				${VIKUNJA_GROUP}

USE_RC_SUBR=		vikunja

GH_ACCOUNT=			go-vikunja
GH_PROJECT=			api
GH_TAGNAME=			${DISTVERSIONPREFIX}${DISTVERSION}

GO_MODULE=			code.vikunja.io/api
GO_BUILDFLAGS=		-tags "${DISTVERSIONPREFIX}${DISTVERSION}" -ldflags "-s -w -X code.vikunja.io/api/pkg/version.Version=${DISTVERSIONPREFIX}${DISTVERSION} -X main.Tags=${DISTVERSIONPREFIX}${DISTVERSION}"

SUB_FILES=			pkg-message

post-install:
	${MKDIR} ${STAGEDIR}/var/db/${PORTNAME}
	${MKDIR} ${STAGEDIR}/var/run/${PORTNAME}
	${MKDIR} ${STAGEDIR}/var/log/${PORTNAME}
	${MKDIR} ${STAGEDIR}${EXAMPLESDIR}
	${INSTALL_DATA} ${WRKSRC}/config.yml.sample ${STAGEDIR}${EXAMPLESDIR}/config.yml.sample

.include <bsd.port.mk>
