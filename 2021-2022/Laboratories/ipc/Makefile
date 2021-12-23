all: ipc-benchmark

# CFLAGS=-DWITH_PMC -Wall
CFLAGS=-Wall -DWITH_KPC

ipc-static: ipc-static.o
	c++ -o ${.TARGET} ${.ALLSRC} -lpmc -lpthread -static -lxo -lutil

ipc-static.o: ipc.c
	cc ${CFLAGS} -c -o ${.TARGET} -DPROGNAME=\"${.TARGET}\" ipc.c -static

ipc-dynamic: ipc-dynamic.o
	c++ -o ${.TARGET} ${.ALLSRC} -lpmc -lpthread -dynamic -lxo -lutil

ipc-dynamic.o: ipc.c
	cc ${CFLAGS} -c -o ${.TARGET} -DPROGNAME=\"${.TARGET}\" ipc.c -dynamic

ipc-benchmark: ipc-benchmark.o yybench_perf.c
	cc -o ${.TARGET} ${.ALLSRC} -lpthread -dynamic -lxo -lutil

ipc-benchmark.o: ipc.c
	cc ${CFLAGS} -c -o ${.TARGET} -DPROGNAME=\"ipc-benchmark\" ${.ALLSRC} -dynamic

yybench_perf.o: yybench_perf.c
	cc ${CFLAGS} -c -o ${.TARGET} ${.ALLSRC} -dynamic

clean:
	rm -f ipc-dynamic.o ipc-dynamic ipc-static.o ipc-static \
	    ipc-benchmark ipc-benchmark.o
