PORTNAME=	authpf-api-cli
DISTVERSIONPREFIX= 	v
DISTVERSION=	0.2.3
CATEGORIES=	sysutils

MAINTAINER=	bofh@scd-systems.net
COMMENT=	AuthPF-API command-line tool
WWW=		https://github.com/scd-systems/authpf-api-cli

LICENSE=	BSD3CLAUSE

USES=		go:modules

GO_BUILDFLAGS=	-ldflags "-X main.Version=${DISTVERSIONPREFIX}${DISTVERSION}"
GO_MODULE=	github.com/scd-systems/authpf-api-cli

PLIST_FILES=	bin/${PORTNAME}\
		share/man/man1/authpf-api-cli.1.gz

post-install:
	${INSTALL_MAN} ${WRKSRC}/manpages/authpf-api-cli.1 ${STAGEDIR}${PREFIX}/share/man/man1/

.include <bsd.port.mk>
