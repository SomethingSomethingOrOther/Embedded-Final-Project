#******************************************************************************
# Copyright (C) 2017 by Alex Fosdick - University of Colorado
#
# Redistribution, modification or use of this software in source or binary
# forms is permitted as long as the files maintain this copyright. Users are 
# permitted to modify this and use it to learn about the field of embedded
# software. Alex Fosdick and the University of Colorado are not liable for any
# misuse of this material. 
#
#*****************************************************************************

#------------------------------------------------------------------------------
# <Put a Description Here>
#
# Use: make [TARGET] [PLATFORM-OVERRIDES]
#
# Build Targets:
#      <Put a description of the supported targets here>
#		<FILE>.o - Builds <FILE>.o object file [main.c, memory.c]
#		<FILE>.i - Builds <FILE>.i preprocessor file
#		<FILE>.asm - Builds <FILE>.asm assembly instructions file
#		compile-all - Builds object files from source files. DOES NOT LINK. Has PHONY proctection
#		build - Builds Executable 
#		clean - Removes ALL build outputs from previous builds[.o, .asm, .i, .map, .exe]		
#
#
# Platform Overrides:
#      <Put a description of the supported Overrides here
#		CPU= - Can be set to different ARM processors[cortex-m0plus,cortex-m4] 	
#		ARCH= - Can be set to different ARM architeture[arm7ve-m, thumb, etc]
#		SPECS= - Can be set different spec files [nosys.spec, nano.specs]
#
#------------------------------------------------------------------------------
include sources.mk

ifeq ($(PLATFORM),HOST)
	CC := gcc

else 
	CC  := arm-none-eabi-gcc
	LDFLAGS = -Wl, -T msp432p401r.lds
endif

DEPS =$(HOSTSOURCES:.c=.dep)
ASSEMBLY = $(HOSTSOURCES:.c=.asm) 
OBJS = $(HOSTSOURCES:.c=.o)
TARGET = c1m2

$(TARGET): $(OBJS)
	$(CC) $(CFLAGS) $(LDFLAGS) -o $(TARGET) $(OBJS)

%.o : %.c 
	$(CC) -c $@ $^

%.i : %.c 
	$(CC) -E $@ $^

%.asm : %.c 
	$(CC) -S $@ $^

%.dep : %.c 
	$(CC) -Wl,-Map=$(TARGET).map $@ $^

.PHONY: clean
clean:
	del -f $(OBJS) $(ASSEMBLY) $(PREPROCESSOR) $(TARGET) 





