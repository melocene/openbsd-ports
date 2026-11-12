COMMENT=	extensible HTTP/1-2-3 web server with cloudflare acme dns

MODGO_MODNAME=	github.com/caddyserver/caddy/v2
MODGO_VERSION=	v2.11.9
DISTNAME=	caddy-dns-cloudflare-${MODGO_VERSION}
CONFLICTS= caddy-[0-9]*

CATEGORIES=	www

HOMEPAGE=	https://caddyserver.com/

# Apache-2.0
PERMIT_PACKAGE=	Yes

WANTLIB += c pthread

MODULES=	lang/go
MODGO_LDFLAGS=	-X "${MODGO_MODNAME}.CustomVersion=${MODGO_VERSION}"

WRKDIST=	${WRKDIR}/${MODGO_MODNAME}@${MODGO_VERSION}

EXAMPLES_DIR=	${PREFIX}/share/examples/caddy

post-build:
	${MODGO_WORKSPACE}/bin/caddy manpage -o ${WRKBUILD}/
	# strip built date and auto-generation marker
	sed -i -e '2s/"8".*/"8"/' -e '$$d' ${WRKBUILD}/*.8

post-install:
	${INSTALL_DATA_DIR} ${EXAMPLES_DIR}
	${INSTALL_DATA} files/Caddyfile ${EXAMPLES_DIR}/
	${INSTALL_MAN} ${WRKBUILD}/*.8 ${PREFIX}/man/man8/

.include "modules.inc"

# Modules added by the local Cloudflare DNS provider patches.
MODGO_MODULES +=	github.com/caddy-dns/cloudflare v0.2.4
MODGO_MODULES +=	github.com/libdns/cloudflare v0.2.2

.include <bsd.port.mk>
