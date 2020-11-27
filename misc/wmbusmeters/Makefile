# $FreeBSD$

PORTNAME=			wmbusmeters
DISTVERSION=		0.9.30
CATEGORIES=			misc

MAINTAINER=			public@fzwte.net
COMMENT=			Wireless mbus utility smart meter decoder tool

LICENSE=        	GPLv3
LICENSE_FILE=   	${WRKSRC}/LICENSE

USES= 				compiler:c++11-lang

USE_GITHUB=			yes
GH_ACCOUNT=			weetmuts
GH_PROJECT=			${PORTNAME}
DISTCOMMITHASH= 	00a83291b78b37287487d6e3fd10a5cbf10a401e

USERS=				${PORTNAME}
GROUPS=				${PORTNAME}

OPTIONS_DEFINE= 	DEBUG TEST

MAKEFILE=       	${FILESDIR}/Makefile.bsd
USE_RC_SUBR=    	${PORTNAME}

ALL_TARGET=     	all
TEST_TARGET=    	test
TEST_ALL_TARGET=	${PORTNAME}_test

DEBUG_CXXFLAGS= 	-O0 -ggdb -fsanitize=address -fno-omit-frame-pointer -fprofile-arcs -ftest-coverage

.include <bsd.port.pre.mk>

.if ${PORT_OPTIONS:MDEBUG}
.if ${COMPILER_TYPE} == clang
LDFLAGS+= 			-fsanitize=address --coverage
.else
LDFLAGS+=      		-lasan -lgcov --coverage
.endif
.endif

post-extract:
	echo "#define VERSION \"$(DISTVERSION)\"" > ${WRKSRC}/src/version.h
	echo "#define COMMIT \"$(DISTCOMMITHASH)\"" >> ${WRKSRC}/src/version.h
	echo 'R"MANUAL(' > ${WRKSRC}/src/short_manual.h
	${SED} -n '/wmbusmeters version/,/```/p' ${WRKSRC}/README.md | ${GREP} -v 'wmbusmeters version' | ${GREP} -v '```' >> ${WRKSRC}/src/short_manual.h
	echo ')MANUAL";' >> ${WRKSRC}/src/short_manual.h

do-install:
	${INSTALL_PROGRAM} ${WRKSRC}/${PORTNAME} ${STAGEDIR}${PREFIX}/bin
	${INSTALL_DATA} ${FILESDIR}/${PORTNAME}.conf ${STAGEDIR}${PREFIX}/etc
	${INSTALL_MAN} ${WRKSRC}/${PORTNAME}.1 ${STAGEDIR}${PREFIX}/man/man1
	${INSTALL} -d ${STAGEDIR} ${STAGEDIR}${PREFIX}/etc/${PORTNAME}.d
	${INSTALL} -d ${STAGEDIR} ${STAGEDIR}/var/db/${PORTNAME}
	${INSTALL} -d ${STAGEDIR} ${STAGEDIR}/var/log/${PORTNAME}/

do-test:
	cd ${WRKSRC} && ${SH} test.sh ./${PORTNAME}

.include <bsd.port.post.mk>
