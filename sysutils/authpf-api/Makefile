PORTNAME=		authpf-api
DISTVERSIONPREFIX=	v
DISTVERSION=		0.2.2
CATEGORIES=		sysutils

MAINTAINER=		bofh@scd-systems.net
COMMENT=		RESTful API for managing FreeBSD/OpenBSD authpf rules by using HTTPS
WWW=			https://github.com/scd-systems/authpf-api

LICENSE=		BSD3CLAUSE
LICENSE_FILE=		${WRKSRC}/LICENSE

USES=			go:modules
USE_RC_SUBR=		authpf-api

GO_BUILDFLAGS=		-ldflags "-X main.Version=${DISTVERSIONPREFIX}${DISTVERSION}"
GO_MODULE=		github.com/scd-systems/authpf-api

OPTIONS_DEFINE=		DOCS EXAMPLES PFCTL_WRAPPER
OPTIONS_DEFAULT=    	DOCS EXAMPLES
OPTIONS_SUB=		yes
PFCTL_WRAPPER_DESC=	Build and install pfctl wrapper utility

PLIST_SUB_PFCTL_WRAPPER_ON=	PFCTL_WRAPPER=""
PLIST_SUB_PFCTL_WRAPPER_OFF=	PFCTL_WRAPPER="@comment "

do-install:
	${MKDIR} ${STAGEDIR}${PREFIX}/sbin
	${INSTALL_PROGRAM} ${WRKDIR}/bin/${PORTNAME} ${STAGEDIR}${PREFIX}/sbin/${PORTNAME}
	${INSTALL_DATA} ${WRKSRC}/authpf-api.conf.sample ${STAGEDIR}${PREFIX}/etc/authpf-api.conf.sample

do-build-PFCTL_WRAPPER-on:
	cd ${WRKSRC}/scripts && \
	${SETENV} ${MAKE_ENV} go build -o ${WRKDIR}/bin/pfctl-wrapper .

post-install-PFCTL_WRAPPER-on:
	${MKDIR} ${STAGEDIR}${EXAMPLESDIR}
	${MKDIR} ${STAGEDIR}${DOCSDIR}
	${INSTALL_PROGRAM} ${WRKDIR}/bin/pfctl-wrapper ${STAGEDIR}${PREFIX}/sbin/pfctl-wrapper
	${INSTALL_DATA} ${WRKSRC}/scripts/doas.conf.example ${STAGEDIR}${EXAMPLESDIR}/doas.conf.example
	${INSTALL_DATA} ${WRKSRC}/scripts/README.md ${STAGEDIR}${DOCSDIR}/README_pfctl_wrapper.md

post-install-EXAMPLES-on:
	${MKDIR} ${STAGEDIR}${EXAMPLESDIR}
	${INSTALL_DATA} ${FILESDIR}/authpf-api.sudoers ${STAGEDIR}${EXAMPLESDIR}/authpf-api.sudoers

post-install-DOCS-on:
	${MKDIR} ${STAGEDIR}${DOCSDIR}
	${INSTALL_DATA} ${WRKSRC}/README.md ${STAGEDIR}${DOCSDIR}/README.md
	${INSTALL_MAN} ${WRKSRC}/manpages/authpf-api.1 ${STAGEDIR}${PREFIX}/share/man/man1/
	${INSTALL_MAN} ${WRKSRC}/manpages/authpf-api.conf.5 ${STAGEDIR}${PREFIX}/share/man/man5/
.include <bsd.port.mk>
