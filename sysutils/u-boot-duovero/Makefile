# $FreeBSD$

PORTNAME=	u-boot
PORTVERSION=	2014.10
CATEGORIES=	sysutils
MASTER_SITES=	ftp://ftp.denx.de/pub/u-boot/
PKGNAMESUFFIX=	-duovero

MAINTAINER=	ian@FreeBSD.org
COMMENT=	Cross-build U-Boot loader for Duovero

LICENSE=	GPLv2

BUILD_DEPENDS=	${CROSS_GCC}:devel/arm-none-eabi-gcc492

CROSS_GCC=	arm-none-eabi-gcc-4.9.2

NO_ARCH=	yes

WRKSRC=		${WRKDIR}/u-boot-${PORTVERSION}
USES=		gmake tar:bzip2
SSP_UNSAFE=	yes # cross-LD does not support -fstack-protector

U_BOOT_DIR=	share/u-boot/${PORTNAME}${PKGNAMESUFFIX}
PLIST_FILES=	${U_BOOT_DIR}/u-boot.img \
		${U_BOOT_DIR}/MLO \
		${U_BOOT_DIR}/README

MAKE_ARGS+=	ARCH=arm \
		CC=${CROSS_GCC} \
		CROSS_COMPILE=arm-none-eabi-

do-configure:
	(cd ${WRKSRC}; ${MAKE_CMD} duovero_config)

do-install:
	${MKDIR} ${STAGEDIR}/${PREFIX}/${U_BOOT_DIR}
	${INSTALL_DATA} ${WRKSRC}/MLO ${STAGEDIR}/${PREFIX}/${U_BOOT_DIR}
	${INSTALL_DATA} ${WRKSRC}/u-boot.img ${STAGEDIR}/${PREFIX}/${U_BOOT_DIR}
	${INSTALL_DATA} ${DESCR} ${STAGEDIR}/${PREFIX}/${U_BOOT_DIR}/README

.include <bsd.port.mk>
