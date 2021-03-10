#
#  CS348C  Radiosity     Device independent graphics package GLIB.
#                        SUN/Xview version makefile
#
#
# Cross-compile changes by Thomas E. Hansen (CodingCellist) 2021-03-08

TARGET = glibps.a
OBJS   = glibps.o

include ../../../Makefile.config

$(TARGET): $(OBJS)
	$(TOOLCHAIN_PREFIX)ar crv $(TARGET) $(OBJS)

clean:
	rm -rf *.o $(TARGET)
