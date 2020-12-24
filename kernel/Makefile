V		 = ~/Repositories/v/v
CC       = gcc
AR 		 = ar
AS 		 = as
LD       = ld
OBJDUMP	 = objdump
VFLAGS 	= -freestanding -m32
CFLAGS  += -m32 -Wall -Os -fomit-frame-pointer -g -Iarch/i686/  -I.
LDFLAGS	 = -melf_i386 -nostdlib #-ffreestanding -O2
ARCH = arch/i686
MAIN_RUN_OBJS	= $(MAIN_RUN_C:.c=.o)
ARCH_RUN_OBJS	= $(ARCH)/boot.o
MK_C	 = $(wildcard *.c) 
MK_V	 = $(wildcard *.v) 
MK_OBJS	 = $(MK_C:.c=.o) $(MK_V:.v=.o)
OBJS	 = $(MAIN_RUN_OBJS) $(ARCH_RUN_OBJS) $(MK_OBJS)

all: kernel

kernel: $(OBJS) $(LINK_SCRIPT)
	$(LD) $(LDFLAGS) -static -o ../build/kernel.bin \
        $(OBJS) -Tkernel.ld 

%.o: %.S
	$(AS) --32 -o $@ $<

%.o: %.v
	$(V) $(VFLAGS) -o $@ $<

# %.o: %.asm
# 	nasm -f elf -o $@ $<

run:
	qemu-system-i386 -kernel build/kernel.bin


clean:
	rm -fr ../build/* build/*
	rm -f *.o *.a
	rm -f arch/i686/*.o
