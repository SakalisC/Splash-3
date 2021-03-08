TARGET = VOLREND
OBJS = adaptive.o file.o main.o map.o normal.o octree.o opacity.o option.o raytrace.o render.o view.o libtiff/libtiff.a

include ../../Makefile.config

CFLAGS := $(CFLAGS) -I./libtiff
LDFLAGS := -L./libtiff $(LDFLAGS) -ltiff

main.c:	main.c.in incl.h anl.h
file.c:	file.c.in incl.h
option.c: option.c.in incl.h
map.c: map.c.in incl.h
normal.c: normal.c.in incl.h anl.h address.h
opacity.c: opacity.c.in incl.h anl.h
octree.c: octree.c.in incl.h anl.h
view.c:	view.c.in incl.h
render.c: render.c.in incl.h
adaptive.c: adaptive.c.in incl.h anl.h
raytrace.c: raytrace.c.in incl.h address.h

incl.h:	user_options.h const.h my_types.h global.h macros.h address.h

libtiff/libtiff.a:
	make -C libtiff

clean:
	$(MAKE) -C libtiff clean
	$(RM) $(OBJS) VOLREND

