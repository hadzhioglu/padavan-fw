# use host target
CC        = gcc
GCC       = gcc
CXX       = g++
AS        = as
AR        = ar
LD        = ld
NM        = nm
OBJCOPY   = objcopy
RANLIB    = ranlib
STRIP     = strip
STRIPTOOL = $(STRIP)

CFLAGS    = -Wall -O2
LDFLAGS   =

-include $(LINUX_CONFIG)

all : install

install :
	mkdir -p bin
	make -C mkimage
	make -C mktplinkfw
	make -C sstrip
	make -C mksquash_lzma-3.2 install
	make -C mksquash_xz-4.0 install

clean:
	rm -rf ./bin
	rm -rf ./headers
	make -C sstrip clean
	make -C mkimage clean
	make -C mktplinkfw clean
	make -C mksquash_lzma-3.2 clean
	make -C mksquash_xz-4.0 clean
	if [ -f xz/Makefile ] ; then \
		make -C xz distclean ; \
	fi ;

mrproper:
	echo "OK"
