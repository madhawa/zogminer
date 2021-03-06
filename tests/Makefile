# MIT License
#
# Copyright (c) 2016 Omar Alvarez
#
# Permission is hereby granted, free of charge, to any person obtaining a copy
# of this software and associated documentation files (the "Software"), to deal
# in the Software without restriction, including without limitation the rights
# to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
# copies of the Software, and to permit persons to whom the Software is
# furnished to do so, subject to the following conditions:
#
# The above copyright notice and this permission notice shall be included in all
# copies or substantial portions of the Software.
#
# THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
# IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
# FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
# AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
# LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
# OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
# SOFTWARE.

INC_DIR = deps

ifeq ($(shell uname -s),Darwin)
	CC ?= clang
	LDLIBS += -framework OpenCL
else
	CC ?= gcc
	LDLIBS += -lOpenCL
endif

CFLAGS += -c -std=c11 -Wall -pedantic -O2 -I $(INC_DIR)

TARGET = gpu-list cpu-list

SOURCES_GPU = gpu-list-gen.c
SOURCES_CPU = cpu-list-gen.c

OBJECTS_GPU = $(patsubst %.c,%.o,$(SOURCES_GPU))
OBJECTS_CPU = $(patsubst %.c,%.o,$(SOURCES_CPU))

all: $(TARGET)

%.o: %.c
	$(CC) $(CFLAGS) -o $@ $<

gpu-list: $(OBJECTS_GPU)
	$(CC) -o $@ $^ $(LDLIBS)

cpu-list: $(OBJECTS_CPU)
	$(CC) -o $@ $^ $(LDLIBS)

clean:
	rm -f $(TARGET) $(OBJECTS_GPU) $(OBJECTS_CPU)

.PHONY: all clean
