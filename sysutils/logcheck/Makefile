# $OpenBSD$

COMMENT =		check log files for anomalies

V =			1.3.20
DISTNAME =		logcheck_${V}
PKGNAME =		logcheck-${V}

CATEGORIES =		sysutils

HOMEPAGE =		http://logcheck.alioth.debian.org/

MAINTAINER =		Markus Lude <markus.lude@gmx.de>

# GPLv2
PERMIT_PACKAGE_CDROM =	Yes

MASTER_SITES =		http://ftp.de.debian.org/debian/pool/main/l/logcheck/

EXTRACT_SUFX =		.tar.xz

RUN_DEPENDS =		mail/mime-construct \
			shells/bash \
			sysutils/lockfile

NO_BUILD =		Yes
WRKDIST =		${WRKDIR}/logcheck

DTR =			10-savelog 20-logrotate 30-logrotate-dateext

CONFDIRS =		ignore.d.paranoid ignore.d.workstation \
			ignore.d.server cracking.d \
			violations.d violations.ignore.d

CONFDIRS_EMPTY =	cracking.ignore.d logcheck.logfiles.d

post-patch:
	cp ${FILESDIR}/logcheck.1 ${WRKSRC}/docs/logcheck.1

do-install:
	${SUBST_PROGRAM} ${WRKSRC}/src/logcheck ${PREFIX}/bin/logcheck
	${SUBST_PROGRAM} ${WRKSRC}/src/logcheck-test ${PREFIX}/bin/logcheck-test
	${INSTALL_SCRIPT} ${WRKSRC}/src/logtail ${PREFIX}/bin/logtail
	${SUBST_PROGRAM} ${WRKSRC}/src/logtail2 ${PREFIX}/bin/logtail2
	${INSTALL_DATA_DIR} ${PREFIX}/share/logtail/detectrotate
.for i in ${DTR}
	${INSTALL_SCRIPT} ${WRKSRC}/src/detectrotate/${i}.dtr \
		${PREFIX}/share/logtail/detectrotate
.endfor
#	/usr/local/docbook-to-man ${WRKSRC}/docs/logcheck.sgml \
#		> ${WRKSRC}/docs/logcheck.1
	${INSTALL_MAN} ${WRKSRC}/docs/logcheck.1 ${PREFIX}/man/man1
	${INSTALL_MAN} ${WRKSRC}/docs/logcheck-test.1 ${PREFIX}/man/man1
	${INSTALL_MAN} ${WRKSRC}/docs/logtail.8 ${PREFIX}/man/man8
	${INSTALL_MAN} ${WRKSRC}/docs/logtail2.8 ${PREFIX}/man/man8

	${INSTALL_DATA_DIR} ${PREFIX}/share/examples/logcheck/
	${INSTALL_DATA} ${WRKSRC}/etc/logcheck.logfiles \
		${PREFIX}/share/examples/logcheck/
	${INSTALL_DATA} ${WRKSRC}/etc/logcheck.conf \
		${PREFIX}/share/examples/logcheck/

	rm ${WRKSRC}/rulefiles/linux/*/*.orig
.for i in ${CONFDIRS}
	${INSTALL_DATA_DIR} ${PREFIX}/share/examples/logcheck/${i}
	# grep doesnt handle \w
	sed -i -e 's/^^\\w/^[[:alpha:]]/' ${WRKSRC}/rulefiles/linux/${i}/*
	${INSTALL_DATA} ${WRKSRC}/rulefiles/linux/${i}/* \
		${PREFIX}/share/examples/logcheck/${i}/
.endfor
.for i in ${CONFDIRS_EMPTY}
	${INSTALL_DATA_DIR} ${PREFIX}/share/examples/logcheck/${i}
.endfor

.include <bsd.port.mk>
