#	$OpenBSD: Makefile,v 1.9 2019/01/20 10:02:38 anton Exp $

PROG=		kcov
WARNINGS=	yes

LDADD+=	-lpthread
DPADD+=	${LIBPTHREAD}

MODES+=	pc
MODES+=	cmp

TESTS+=	close
TESTS+=	coverage
TESTS+=	dying
TESTS+=	exec
TESTS+=	fork
TESTS+=	open
TESTS+=	state

REGRESS_SETUP_ONCE=	setup
setup: ${PROG}

.for m in ${MODES}
.  for t in ${TESTS}
$m-$t:
	@echo "\n======== ${@} ========"
	if ${SUDO} ./${PROG} -p; then \
		${SUDO} ./${PROG} ${KCOVFLAGS} -m $m $t; \
	else \
		echo "SKIPPED"; \
	fi
REGRESS_TARGETS+=	$m-$t
.  endfor
.endfor

.include <bsd.regress.mk>
