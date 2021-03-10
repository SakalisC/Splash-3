#
#  Device independent graphics package GLIB.
#  NULL graphic device version
#
# Cross-compile changes by Thomas E. Hansen (CodingCellist) 2021-03-08

OBJS   = glib.o
TARGET = glib.a

include ../../../Makefile.config

$(TARGET): $(OBJS)
	$(TOOLCHAIN_PREFIX)ar crv $(TARGET) $(OBJS)

clean:
	rm -rf $(OBJS) $(TARGET)
