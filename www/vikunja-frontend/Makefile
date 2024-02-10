PORTNAME=			vikunja
PORTVERSION=		0.22.1
DISTVERSIONPREFIX=	v
CATEGORIES=			www
MASTER_SITES=		https://dl.vikunja.io/frontend/
PKGNAMESUFFIX=		-frontend
DISTNAME=			${PORTNAME}${PKGNAMESUFFIX}-${PORTVERSION}

MAINTAINER=			public@fzwte.net
COMMENT=			Frontend webapp of Vikunja
WWW=				https://vikunja.io

LICENSE=			AGPLv3

USES=				zip

WWWDIR=				${PREFIX}/www/vikunja
NO_ARCH=			yes
NO_BUILD=			yes
NO_WRKSUBDIR=		yes

VIKUNJA_USER=		vikunja
VIKUNJA_GROUP=		vikunja

USERS=				${VIKUNJA_USER}
GROUPS=				${VIKUNJA_GROUP}

do-install:
	${MKDIR} ${STAGEDIR}${WWWDIR}
	cd ${WRKDIR}/${PORTNAME}${PKGNAMESUFFIX}-${PORTVERSION} && ${COPYTREE_SHARE} . ${STAGEDIR}${WWWDIR}

.include <bsd.port.mk>
