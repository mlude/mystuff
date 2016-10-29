# $OpenBSD$

COMMENT =		next generation IDS/IPS engine

DISTNAME = 		suricata-3.0.1
MASTER_SITES = 		http://www.openinfosecfoundation.org/download/

CATEGORIES =		net security mystuff

HOMEPAGE =		http://www.openinfosecfoundation.org/

MAINTAINER =		Markus Lude <markus.lude@gmx.de>

# GPLv2
PERMIT_PACKAGE_CDROM = 	Yes

SHARED_LIBS += 		htp			0.0 # 1.0

WANTLIB += 		c magic lib/libnet-1.1/net pcap pcre pthread yaml-0 z

LIB_DEPENDS = 		devel/pcre \
			devel/libyaml \
			net/libnet/1.1 \
			devel/libmagic

USE_LIBTOOL =		Yes

AUTOCONF_VERSION = 	2.69
AUTOMAKE_VERSION = 	1.14

SEPARATE_BUILD =	Yes
CONFIGURE_STYLE =	gnu autoconf
#CONFIGURE_STYLE =	gnu
CONFIGURE_ARGS +=	${CONFIGURE_SHARED} \
			--enable-debug \
			--with-libnet-includes=${LOCALBASE}/include/libnet-1.1 \
			--with-libnet-libraries=${LOCALBASE}/lib/libnet-1.1

CONFIGS = 		classification.config reference.config threshold.config

#pre-configure:
#	@${SUBST_CMD} ${WRKSRC}/suricata.yaml

post-install:
	${INSTALL_DATA_DIR} ${PREFIX}/share/examples/suricata
	${INSTALL_DATA_DIR} ${WRKINST}/etc/suricata
.for i in ${CONFIGS}
	${INSTALL_DATA} ${WRKSRC}/${i} ${PREFIX}/share/examples/suricata/
	${INSTALL_DATA} ${WRKSRC}/${i} ${WRKINST}${SYSCONFDIR}/suricata/
.endfor
	${INSTALL_DATA} ${WRKBUILD}/suricata.yaml ${PREFIX}/share/examples/suricata/
	${INSTALL_DATA} ${WRKBUILD}/suricata.yaml ${WRKINST}${SYSCONFDIR}/suricata/

NO_TEST =		Yes

.include <bsd.port.mk>
