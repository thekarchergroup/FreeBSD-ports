# Created by: Loic Blot <loic.blot@unix-experience.fr>
# $FreeBSD$

PORTNAME=	searx
PORTVERSION=	0.10.0
DISTVERSIONPREFIX=	v
CATEGORIES=	www python
PKGNAMEPREFIX=	${PYTHON_PKGNAMEPREFIX}

MAINTAINER=	loic.blot@unix-experience.fr
COMMENT=	Searx / a privacy-respecting, hackable metasearch engine

LICENSE=	AGPLv3

RUN_DEPENDS=	${PYTHON_PKGNAMEPREFIX}dateutil>=2.5.0:devel/py-dateutil \
		${PYTHON_PKGNAMEPREFIX}Flask-Babel>=0.11.1:devel/py-flask-babel \
		${PYTHON_PKGNAMEPREFIX}lxml>=3.6.0:devel/py-lxml \
		${PYTHON_PKGNAMEPREFIX}yaml>=3.11:devel/py-yaml \
		${PYTHON_PKGNAMEPREFIX}ndg_httpsclient>=0.4.1:net/py-ndg_httpsclient \
		${PYTHON_PKGNAMEPREFIX}openssl>=0.15.1:security/py-openssl \
		${PYTHON_PKGNAMEPREFIX}pygments>=2.1.3:textproc/py-pygments \
		${PYTHON_PKGNAMEPREFIX}Flask>=0.11.1:www/py-flask \
		${PYTHON_PKGNAMEPREFIX}requests>=2.10:www/py-requests \
		${PYTHON_PKGNAMEPREFIX}werkzeug>0:www/py-werkzeug \
		${PYTHON_PKGNAMEPREFIX}certifi>=2016.2.28:security/py-certifi

USE_RC_SUBR=	searx

USE_GITHUB=	yes
GH_ACCOUNT=	asciimoo
GH_PROJECT=	searx

USES=		python
NO_ARCH=	yes
USE_PYTHON=	autoplist distutils concurrent

.include <bsd.port.mk>
