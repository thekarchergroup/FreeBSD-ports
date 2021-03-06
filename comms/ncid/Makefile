# Created by: David
# $FreeBSD$

PORTNAME=	ncid
PORTVERSION=	1.4
CATEGORIES=	comms
MASTER_SITES=	SF
DISTNAME=	${PORTNAME}-${PORTVERSION}-src

MAINTAINER=	cpm@FreeBSD.org
COMMENT=	Network based Caller ID package

LICENSE=	GPLv3
LICENSE_FILE=	${WRKSRC}/doc/GPL.md

BUILD_DEPENDS=	bash:shells/bash

USES=		gmake perl5 tk shebangfix
SHEBANG_FILES=	extensions/hangup-message.sh \
		extensions/hangup-skel.sh \
		logrotate/ncidrotate.sh
ALL_TARGET=	local
MAKE_ARGS=	WISH=${WISH} TCLSH=${TCLSH}
INSTALL_TARGET=	freebsd-install

SUB_FILES=	pkg-message

OPTIONS_DEFINE=	DOCS LOGROTATE
OPTIONS_SUB=	yes

LOGROTATE_DESC=	Install logrotate scripts

LOGROTATE_RUN_DEPENDS=	logrotate:sysutils/logrotate

WRKSRC=	${WRKDIR}/${PORTNAME}

PORTDOCS=	*

post-extract:
	@cd ${WRKSRC}/FreeBSD;for i in *.rc; do \
		x=`echo $$i | cut -f 1 -d .`; ${CP} $$i $$x; done

post-patch:
	@${GREP} -lr 'etc/ncid' ${WRKSRC}/ | ${XARGS} ${REINPLACE_CMD} -Ee \
		's,(/usr/local/etc/ncid | /etc/ncid),${ETCDIR},g'
	@${FIND} ${WRKSRC}/ -name Makefile | ${XARGS} ${REINPLACE_CMD} -Ee \
		'/install:/s,install-(etc|logrotate),,'
	@${REINPLACE_CMD} -Ee '/mkdir.*(INIT|ROTATE|BIN|LOG|ETC)/d ;\
		/CFLAGS.*=/s|=|+=|' ${WRKSRC}/Makefile
# Respect PREFIX/MANPREFIX/DATADIR
	@${REINPLACE_CMD} -e 's|prefix.*= /usr/local|prefix=$${PREFIX}|g' \
		-e 's|$$(prefix)/bin|$${PREFIX}/bin|g' \
		-e 's|$$(prefix)/sbin|$${PREFIX}/sbin|g' \
		-e 's|$$(prefix)/share|$${PREFIX}/share|g' \
		-e 's|$$(SHARE)/man|$${MANPREFIX}/man/|g' \
		-e 's|$$(SHARE)/ncid|$${DATADIR}|g' ${WRKSRC}/Makefile

do-install:
	@${MKDIR} ${STAGEDIR}${ETCDIR}
	${INSTALL_PROGRAM} ${WRKSRC}/server/ncidd ${STAGEDIR}${PREFIX}/sbin
	${INSTALL_DATA} ${WRKSRC}/server/ncidd.conf ${STAGEDIR}${ETCDIR}
	${INSTALL_PROGRAM} ${WRKSRC}/gateway/sip2ncid ${STAGEDIR}${PREFIX}/sbin
	${INSTALL_DATA} ${WRKSRC}/client/ncid ${STAGEDIR}${PREFIX}/bin
	${INSTALL_DATA} ${WRKSRC}/client/ncid.conf ${STAGEDIR}${ETCDIR}
.for e in hangup-message.sh hangup-skel.sh
	@${MKDIR} ${STAGEDIR}${PREFIX}/share/ncid/extensions
	${INSTALL_SCRIPT} ${WRKSRC}/extensions/${e} ${STAGEDIR}${PREFIX}/share/ncid/extensions
.endfor
.for f in ncid2ncid obi2ncid rn2ncid yac2ncid wc2ncid
	${INSTALL_DATA} ${WRKSRC}/gateway/${f} ${STAGEDIR}${PREFIX}/bin
	@${STRIP_CMD} ${STAGEDIR}${PREFIX}/bin/ncid2ncid
.endfor
	${INSTALL_DATA} ${WRKSRC}/client/ncid.gif ${STAGEDIR}${PREFIX}/share/pixmaps/ncid
	@${MKDIR} ${STAGEDIR}${PREFIX}/share/ncid/modules
.for g in ncid-page ncid-samba ncid-speak ncid-mythtv ncid-kpopup ncid-skel \
ncid-alert ncid-yac ncid-initmodem ncid-notify ncid-wakeup
	${INSTALL_DATA}	${WRKSRC}/modules/${g} ${STAGEDIR}${PREFIX}/share/ncid/modules
.endfor
	${INSTALL_DATA} ${WRKSRC}/server/ncidd.alias ${STAGEDIR}${ETCDIR}
.for h in cidcall cidalias cidupdate wct ncidutil
	${INSTALL_DATA} ${WRKSRC}/tools/${h} ${STAGEDIR}${PREFIX}/bin
.endfor
.for i in ncidd ncid2ncid obi2ncid rn2ncid sip2ncid wc2ncid yac2ncid ncid-mythtv ncid-notify \
ncid-page ncid-samba ncid-speak ncid-yac ncid-initmodem
	${INSTALL_DATA} ${WRKSRC}/FreeBSD/${i} ${STAGEDIR}${PREFIX}/etc/rc.d
.endfor
.for j in NumberDisconnected.rmd CallingDeposit.rmd NotInService.rmd
	@${MKDIR} ${STAGEDIR}${PREFIX}/share/ncid/recordings
	${INSTALL_DATA} ${WRKSRC}/recordings/${j} ${STAGEDIR}${PREFIX}/share/ncid/recordings
.endfor
	${INSTALL_MAN} ${WRKSRC}/man/*.1 ${STAGEDIR}${MAN1PREFIX}/man/man1
	${INSTALL_MAN} ${WRKSRC}/man/*.5 ${STAGEDIR}${MAN5PREFIX}/man/man5
	${INSTALL_MAN} ${WRKSRC}/man/*.7 ${STAGEDIR}${MAN7PREFIX}/man/man7
	${INSTALL_MAN} ${WRKSRC}/man/*.8 ${STAGEDIR}${MAN8PREFIX}/man/man8
do-install-DOCS-on:
	@${MKDIR} ${STAGEDIR}${DOCSDIR}
	(cd ${WRKSRC}/doc && ${COPYTREE_SHARE} "${PORTDOCS}" ${STAGEDIR}${DOCSDIR})
	@${MKDIR} ${STAGEDIR}${DOCSDIR}/recordings
.for k in README.recordings NumberDisconnected.pvf CallingDeposit.pvf NotInService.pvf
	${INSTALL_DATA} ${WRKSRC}/recordings/${k} ${STAGEDIR}${DOCSDIR}/recordings
.endfor

post-install-LOGROTATE-on:
	@${MKDIR} ${STAGEDIR}${PREFIX}/share/ncid/sys
	${INSTALL_SCRIPT} ${WRKSRC}/logrotate/ncidrotate.sh ${STAGEDIR}${PREFIX}/share/ncid/sys
	@${MKDIR} ${STAGEDIR}${PREFIX}/etc/logrotate.d
	${INSTALL_DATA} ${WRKSRC}/logrotate/ncid ${STAGEDIR}${PREFIX}/etc/logrotate.d
	${INSTALL_MAN} ${WRKSRC}/logrotate/*.1 ${STAGEDIR}${MAN1PREFIX}/man/man1
	${INSTALL_MAN} ${WRKSRC}/logrotate/*.5 ${STAGEDIR}${MAN5PREFIX}/man/man5

.include <bsd.port.mk>
