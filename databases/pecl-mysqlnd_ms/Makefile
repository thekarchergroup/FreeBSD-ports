# Created by: johnpupu <johnpupu@gmail.com>
# $FreeBSD$

PORTNAME=	mysqlnd_ms
PORTVERSION=	1.5.2
PORTREVISION=	1
CATEGORIES=	databases
MASTER_SITES=	http://pecl.php.net/get/
PKGNAMEPREFIX=	pecl-
EXTRACT_SUFX=	.tgz
DIST_SUBDIR=	PECL

MAINTAINER=	johnpupu@gmail.com
COMMENT=	Replication and load balancing plugin for mysqlnd

DEPRECATED=	Works only with EOL php 5.5
EXPIRATION_DATE=	2016-10-20

USES=		php:ext
USE_PHP=	json:build
IGNORE_WITH_PHP=	56 70

.include <bsd.port.mk>
