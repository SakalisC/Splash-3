TARGET = RADIOSITY

OBJS = display.o elemman.o modelman.o patchman.o rad_main.o rad_tools.o room_model.o smallobj.o taskman.o visible.o
HHS = model.h.in parallel.h.in patch.h.in radiosity.h.in task.h.in structs.h.in
HS = model.h parallel.h patch.h radiosity.h task.h structs.h

include ../../Makefile.config

CFLAGS := $(CFLAGS) -I./glibdumb -I./glibps

#CCOPTS = -I -float -I/usr/include $(CFLAGS)
#LDFLAGS = -lm -lpthread
#CFLAGS = $(CINCLUDE) -O4 -march=i686 -mcpu=i686 -malign-double -funroll-loops -finline-functions -fomit-frame-pointer -D_REENTRANT
#CINCLUDE = -I$(GLIBDIR) -I./glibps

LOADLIBES = glibdumb/glib.a glibps/glibps.a

$(TARGET): $(OBJS) $(LOADLIBES)
	$(CC) $(OBJS) $(CFLAGS) $(LOADLIBES) -o $(TARGET) $(LDFLAGS)

radiosity.h: patch.h model.h parallel.h task.h
rad_main.c: rad_main.c.in $(HS)
patchman.c: patchman.c.in $(HS)
elemman.c: elemman.c.in $(HS)
taskman.c: taskman.c.in $(HS)
modelman.c: modelman.c.in $(HS)
smallobj.c: smallobj.c.in $(HS)
display.c: display.c.in $(HS)
visible.c: visible.c.in $(HS)
rad_tools.c: rad_tools.c.in $(HS)
room_model.c: room_model.c.in $(HS)

glibdumb/glib.a:
	$(MAKE) -C glibdumb

glibps/glibps.a:
	$(MAKE) -C glibps

clean:
	$(MAKE) -C glibdumb clean
	$(MAKE) -C glibps clean
	$(RM) $(OBJS) RADIOSITY

