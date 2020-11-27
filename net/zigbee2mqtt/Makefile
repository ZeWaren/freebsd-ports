# $FreeBSD$

PORTNAME=	    zigbee2mqtt
DISTVERSION=	1.16.1
CATEGORIES=     misc

MAINTAINER=	public@fzwte.net
COMMENT=	Zigbee to MQTT bridge

USE_GITHUB=	yes
GH_ACCOUNT=	Koenkk
GH_PROJECT=	zigbee2mqtt

BUILD_DEPENDS= npm:www/npm

USE_RC_SUBR= zigbee2mqtt

do-build:
	cd ${WRKSRC} && npm ci --production
	cd ${WRKSRC} && npm install pkg
	cd ${WRKSRC} && node_modules/.bin/pkg --target node14-freebsd-x64 -o zigbee2mqtt index.js

do-install:
	/usr/bin/install -m 555 ${WRKSRC}/${PORTNAME} ${STAGEDIR}${PREFIX}/bin/
	@${INSTALL_DATA} ${WRKSRC}/node_modules/zigbee-herdsman/node_modules/@serialport/bindings/build/Release/bindings.node ${STAGEDIR}${PREFIX}/bin/
	@${MKDIR} -p ${STAGEDIR}/var/db/${PORTNAME}/data
	@${INSTALL_DATA} ${WRKSRC}/data/configuration.yaml ${STAGEDIR}/var/db/${PORTNAME}/data

post-install:
	@${MKDIR} ${STAGEDIR}/var/log/${PORTNAME}
	@${MKDIR} ${STAGEDIR}/var/run/${PORTNAME}

.include <bsd.port.mk>
