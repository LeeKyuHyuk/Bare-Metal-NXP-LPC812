# Specify the compiler to use
CC=/opt/gcc-arm-none-eabi-10.3-2021.10/bin/arm-none-eabi-gcc
# Specify the assembler to use
AS=/opt/gcc-arm-none-eabi-10.3-2021.10/bin/arm-none-eabi-as
# Specity the linker to use
LD=/opt/gcc-arm-none-eabi-10.3-2021.10/bin/arm-none-eabi-ld
# Specity the objcopy to use
OBJCOPY=/opt/gcc-arm-none-eabi-10.3-2021.10/bin/arm-none-eabi-objcopy

CFLAGS=-mcpu=cortex-m0 -mthumb -g -nostartfiles 
# You must edit the LIBSPEC variable to reflect your own system setup
# Tell the linker where to find the libraries -> important: use thumb versions
LIBSPEC=-L /opt/gcc-arm-none-eabi-10.3-2021.10/lib/gcc/arm-none-eabi/10.3.1/thumb/v6-m/nofp/
# List the object files involved in this project
OBJS=	init.o	main.o 

# The default 'target' (output) is main.elf and it depends on the object files being there.
# These object files are linked together to create main.elf
main.elf : $(OBJS)
	$(LD) $(OBJS) $(LIBSPEC) -lgcc -T lpc812_linker_script.ld --cref -Map main.map -o main.elf
	$(OBJCOPY) -O ihex main.elf main.hex
	@echo "Assuming all went well..."
	@echo "Program the chip as follows: lpc21isp main.hex /dev/ttyUSB0 9600 12000000"
	@echo "replace ttyUSB0 with the correct device name for your system"	
# The object file main.o depends on main.c.  main.c is compiled to make main.o
main.o: main.c
	$(CC) -c $(CFLAGS) main.c -o main.o

init.o: init.c
	$(CC) -c $(CFLAGS) init.c -o init.o

# if someone types in 'make clean' then remove all object files and executables
# associated wit this project
clean: 
	rm -fv $(OBJS) main.elf main.hex main.map 
