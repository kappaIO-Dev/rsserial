#====================================================================================
#     The MIT License (MIT)
#
#     Copyright (c) 2011 Kapparock LLC
#
#     Permission is hereby granted, free of charge, to any person obtaining a copy
#     of this software and associated documentation files (the "Software"), to deal
#     in the Software without restriction, including without limitation the rights
#     to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
#     copies of the Software, and to permit persons to whom the Software is
#     furnished to do so, subject to the following conditions:
#
#     The above copyright notice and this permission notice shall be included in
#     all copies or substantial portions of the Software.
#
#     THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
#     IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
#     FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
#     AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
#     LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
#     OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN
#     THE SOFTWARE.
#====================================================================================
SRC:=${CURDIR}/
#CFLAGS+= -x c++
LIBNAME:=libzdo
SONAME:=$(LIBNAME).so.0
LIBSO:=$(LIBNAME).so.0.0.0
LIBA:=$(LIBNAME).a
LINKERNAME:=$(LIBNAME).so
OBJ= zdo.o zdo_archive.o
	 	 
CPPFLAGS:=-fPIC -pedantic 
LDFLAGS+= -shared 

VPATH=$(SRC)

$(LIBSO) $(LIBA) : $(OBJ)
	#$(AR) rcs $(LIBA) $(OBJ)
	#cp -d $(LIBA) $(LIBDIR_A)
	$(CXX) $(OBJ) $(LDFLAGS) -Wl,-soname,$(SONAME) -o $(LIBSO)
	ln -s $(LIBSO) $(LINKERNAME)
	ln -s $(LIBSO) $(SONAME)
	cp -d *.so* ${LIBDIR}
	cp -d *.h* ${LIBINCLUDE}
	touch .built
	
${CURDIR}/%.o: %.c

${CURDIR}/%.o: %.cpp
.PHONY : clean
clean:
	rm *.o *.so*
