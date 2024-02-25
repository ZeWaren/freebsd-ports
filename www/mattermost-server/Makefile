PORTNAME=	mattermost
PORTVERSION=	9.5.1
CATEGORIES=	www
PKGNAMESUFFIX=	-server
DISTFILES=	mattermost-9.5.1-freebsd-amd64.tar.gz

MAINTAINER=	public@fzwte.net
COMMENT=	Open source Slack-alternative in Golang and React
WWW=		https://mattermost.org/

LICENSE=	MIT
LICENSE_FILE=	${WRKSRC}/MIT-COMPILED-LICENSE.md

ONLY_FOR_ARCHS=	aarch64 amd64

RUN_DEPENDS=	${LOCALBASE}/share/certs/ca-root-nss.crt:security/ca_root_nss \
		mattermost-webapp>=${PORTVERSION}:www/mattermost-webapp

NO_BUILD=yes
WRKSRC=	${WRKDIR}/mattermost

USE_RC_SUBR=	mattermostd

WWWDIR=		${PREFIX}/www/mattermost

MATTERMOSTD_USER=	mattermost
MATTERMOSTD_GROUP=	mattermost

USERS=		${MATTERMOSTD_USER}
GROUPS=		${MATTERMOSTD_GROUP}

do-install:
	${INSTALL_PROGRAM} ${WRKSRC}/bin/mattermost ${STAGEDIR}${PREFIX}/bin/mattermostd
	${INSTALL_PROGRAM} ${WRKSRC}/bin/mmctl ${STAGEDIR}${PREFIX}/bin/mmctl
	${MKDIR} ${STAGEDIR}${PREFIX}/etc/mattermost
	${INSTALL_DATA} ${WRKSRC}/config/config.json ${STAGEDIR}${PREFIX}/etc/mattermost/config.json.sample
	${MKDIR} ${STAGEDIR}${WWWDIR}/templates
	cd ${WRKSRC} && ${COPYTREE_SHARE} 'fonts i18n' ${STAGEDIR}${WWWDIR}
	cd ${WRKSRC}/templates && ${CP} *.html *.js ${STAGEDIR}${WWWDIR}/templates

.include <bsd.port.mk>
