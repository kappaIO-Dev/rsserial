SOC_PORT:=\"/dev/ttyS0\"
ENDIANNESS:=__LITTLE_ENDIAN
LIBDIR:=${CURDIR}/lib
LIBDIR_A:=${CURDIR}/a
LIBDIR_SO:=${CURDIR}/so
LIBINCLUDE:=${CURDIR}/include
PROJECT_ROOT_DIR:=${CURDIR}

export CFLAGS CXXFLAGS
export PROJECT_ROOT_DIR
export LIBDIR LIBDIR_A LIBDIR_SO LIBINCLUDE 

SRC:=${CURDIR}/
UCLIBSPECIFIC:=-fno-builtin -nostdinc++ -DGCC_HASCLASSVISIBILITY -nodefaultlibs -lc
INCLUDE_DIR+=-I$(SRC) -I$(LIBINCLUDE) -I$(STAGING_DIR)
INCLUDE_DIR+=-I$(STAGING_DIR)/../toolchain-mipsel_24kec+dsp_gcc-4.8-linaro_uClibc-0.9.33.2/mipsel-openwrt-linux-uclibc/include/c++/4.8.3
#DEBUG_OPTIONS:=-g3 -O0 -ggdb
DEBUG_OPTIONS:=
$(info hello processor $(processor_family))
CXXFLAGS+=$(INCLUDE_DIR) -std=c++11 -D_TIMT_ -D__LITTLE_ENDIAN__ $(DEBUG_OPTIONS) -DPKG_RELEASE=\"$(PKG_RELEASE)\"
CFLAGS+=$(INCLUDE_DIR) -x c++ -std=c++11 -D_TIMT_ -D__LITTLE_ENDIAN__ $(DEBUG_OPTIONS)
CPPFLAGS:=-fpermissive $(DEBUG_OPTIONS)
LDFLAGS+=-L$(LIBDIR) -lstdc++ -lpthread -ljansson -ldl -lssl -lcrypto -lc -lrt

export LDFLAGS
OBJ= rsserial.o

VPATH=$(SRC)

rsserial: sbl/.built kapi/.built hal/.built aps/.built zdo/.built kintf/.built rsserial_watch/.built $(OBJ)
	$(CXX) $(OBJ) -o rsserial -lkapi -lhal -lkdev -lzdo -lkintf -laps $(LDFLAGS) 
${CURDIR}/%.o: %.c sbl/.built kapi/.built hal/.built
${CURDIR}/%.o: %.cpp sbl/.built kapi/.built hal/.built
rsserial_watch/.built:kapi/.built
	$(MAKE) -C rsserial_watch
sbl/.built: .libdir_created kapi/.built hal/.built
	$(MAKE) -C sbl
kapi/.built:.libdir_created
	$(MAKE) -C kapi
# libhal depends on libkapi, libkdev
hal/.built: .libdir_created kapi/.built kdev/.built
	$(MAKE) -C hal
# libkdev depends on libkapi
kdev/.built:.libdir_created kapi/.built
	$(MAKE) -C kdev
# libaps depends libkapi, libhal
aps/.built: .libdir_created kapi/.built kapi/.built hal/.built
	$(MAKE) -C aps
zdo/.built: kapi/.built hal/.built aps/.built
	$(MAKE) -C zdo
kintf/.built: kapi/.built hal/.built aps/.built
	$(MAKE) -C kintf
.libdir_created:
	mkdir $(LIBDIR)
	mkdir $(LIBINCLUDE)
	mkdir $(LIBDIR_A)
	mkdir $(LIBDIR_SO)
	touch .libdir_created
.PHONY : clean
clean:
	rm *.o rsserial 
