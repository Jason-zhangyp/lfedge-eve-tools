# Copyright (c) 2019 Zededa, Inc.
# SPDX-License-Identifier: Apache-2.0

TARGET ?= eve_run 
INC_DIRS ?= ./lib/include ./cpp
LDLIBS := -lprotobuf -L . libevetools.so
INC_FLAGS := $(addprefix -I,$(INC_DIRS))
CPPFLAGS ?= $(INC_FLAGS) -std=c++11 -g
CC = g++
DESTDIR = /usr/
PREFIX = local

eve_run: libevetools.so
	$(CC) tools/eve_run.cpp cpp/api.pb.cc $(CPPFLAGS) -o eve_run $(LDLIBS)

libevetools.so: lib/src/sendrecv.cpp
	$(CC) $(CPPFLAGS) -shared -fPIC -o libevetools.so lib/src/sendrecv.cpp lib/src/eve_tpm_service.cpp cpp/api.pb.cc -lprotobuf

.PHONY: clean all

clean:
	rm -rf libevetools.so *.dSYM eve_run 

install: libevetools.so eve_run
	install -m 755 libevetools.so /usr/lib
	install -m 755 eve_run /usr/bin
	install -m 755 tools/read_ek_public /usr/bin
	install -d /usr/include
	install -m 644 lib/include/eve_tpm_service.h /usr/include

all: libevetools.so eve_run 
