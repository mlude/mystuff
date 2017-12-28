# $OpenBSD$

COMMENT =	construct and optionally mail MIME messages

MODULES =	cpan
PKG_ARCH =	*
DISTNAME =	mime-construct-1.9
PKGNAME =	${DISTNAME}
CATEGORIES =	mail

BUILD_DEPENDS = ${RUN_DEPENDS}
RUN_DEPENDS =	mail/p5-MIME-Types \
		sysutils/p5-Proc-WaitStat

HOMEPAGE =	http://www.argon.org/~roderick/

MAINTAINER =	Markus Lude <markus.lude@gmx.de>

# GPLv2+
PERMIT_PACKAGE_CDROM =  Yes

CPAN_AUTHOR =	ROSCH

.include <bsd.port.mk>
