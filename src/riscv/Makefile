
# sample
# make USE_NEWLIB=y USE_SYSROOT=/home/katsuhiro/share/projects/oss/baremetal_crt/test/sysroot all

CC  = $(CROSS_COMPILE)gcc
CXX = $(CROSS_COMPILE)g++
ADD_AUXDATA ?= $(USE_SYSROOT)/bin/add_auxdata

DIR_SRC = ../

# Config for bmetal.mk
USE_GLIBC   ?= n
USE_MUSL    ?= n
USE_NEWLIB  ?= y
USE_SYSROOT ?= /home/katsuhiro/share/projects/oss/baremetal_crt/test/sysroot

# 32bit
#APP_CFLAGS_RV  = -march=rv32im -mabi=ilp32 -mcmodel=medany
#APP_LDFLAGS_RV = -march=rv32im -mabi=ilp32 -mcmodel=medany
APP_CFLAGS_RV  = -march=rv32imafc -mabi=ilp32f -mcmodel=medany
APP_LDFLAGS_RV = -march=rv32imafc -mabi=ilp32f -mcmodel=medany

# 32bit glibc
#APP_CFLAGS_RV  = -march=rv32gc -mabi=ilp32d -mcmodel=medany
#APP_LDFLAGS_RV = -march=rv32gc -mabi=ilp32d -mcmodel=medany
#APP_CFLAGS_RV  = -march=rv32imac -mabi=ilp32 -mcmodel=medany
#APP_LDFLAGS_RV = -march=rv32imac -mabi=ilp32 -mcmodel=medany

# 64bit glibc
#APP_CFLAGS_RV  = -march=rv64gc -mabi=lp64d -mcmodel=medany
#APP_LDFLAGS_RV = -march=rv64gc -mabi=lp64d -mcmodel=medany
#APP_CFLAGS_RV  = -march=rv64imac -mabi=lp64 -mcmodel=medany
#APP_LDFLAGS_RV = -march=rv64imac -mabi=lp64 -mcmodel=medany

APP_CPPFLAGS = -Wall \
   -D HAVE_CONFIG_H -D HAVE_STRLWR \
   -I $(DIR_SRC)/../ -I $(DIR_SRC)/./
APP_CFLAGS   = -O2 -gdwarf-4 $(APP_CFLAGS_RV)
APP_CXXFLAGS = $(APP_CFLAGS)
APP_LDFLAGS  = $(APP_LDFLAGS_RV)

CPPFLAGS = $(APP_CPPFLAGS) $(EXT_CPPFLAGS)
CFLAGS   = $(APP_CFLAGS)   $(EXT_CFLAGS)
CXXFLAGS = $(APP_CXXFLAGS) $(EXT_CXXFLAGS)
LDFLAGS  = $(APP_LDFLAGS)  $(EXT_LDFLAGS)

BINS = \
       	prboom

PRBOOM_OBJS = \
	$(DIR_SRC)/SDL/i_sound.o  \
	$(DIR_SRC)/SDL/i_system.o \
	$(DIR_SRC)/SDL/i_main.o   \
	$(DIR_SRC)/SDL/i_video.o  \
	$(DIR_SRC)/SDL/i_joy.o    \
	$(DIR_SRC)/am_map.o       \
	$(DIR_SRC)/d_client.o     \
	$(DIR_SRC)/d_deh.o        \
	$(DIR_SRC)/d_items.o      \
	$(DIR_SRC)/d_main.o       \
	$(DIR_SRC)/doomdef.o      \
	$(DIR_SRC)/doomstat.o     \
	$(DIR_SRC)/dstrings.o     \
	$(DIR_SRC)/f_finale.o     \
	$(DIR_SRC)/f_wipe.o       \
	$(DIR_SRC)/g_game.o       \
	$(DIR_SRC)/hu_lib.o       \
	$(DIR_SRC)/hu_stuff.o     \
	$(DIR_SRC)/info.o         \
	$(DIR_SRC)/lprintf.o      \
	$(DIR_SRC)/m_argv.o       \
	$(DIR_SRC)/m_bbox.o       \
	$(DIR_SRC)/m_cheat.o      \
	$(DIR_SRC)/m_menu.o       \
	$(DIR_SRC)/m_misc.o       \
	$(DIR_SRC)/m_random.o     \
	$(DIR_SRC)/md5.o          \
	$(DIR_SRC)/mmus2mid.o     \
	$(DIR_SRC)/p_ceilng.o     \
	$(DIR_SRC)/p_checksum.o   \
	$(DIR_SRC)/p_doors.o      \
	$(DIR_SRC)/p_enemy.o      \
	$(DIR_SRC)/p_floor.o      \
	$(DIR_SRC)/p_genlin.o     \
	$(DIR_SRC)/p_inter.o      \
	$(DIR_SRC)/p_lights.o     \
	$(DIR_SRC)/p_map.o        \
	$(DIR_SRC)/p_maputl.o     \
	$(DIR_SRC)/p_mobj.o       \
	$(DIR_SRC)/p_plats.o      \
	$(DIR_SRC)/p_pspr.o       \
	$(DIR_SRC)/p_saveg.o      \
	$(DIR_SRC)/p_setup.o      \
	$(DIR_SRC)/p_sight.o      \
	$(DIR_SRC)/p_spec.o       \
	$(DIR_SRC)/p_switch.o     \
	$(DIR_SRC)/p_telept.o     \
	$(DIR_SRC)/p_tick.o       \
	$(DIR_SRC)/p_user.o       \
	$(DIR_SRC)/r_bsp.o        \
	$(DIR_SRC)/r_data.o       \
	$(DIR_SRC)/r_demo.o       \
	$(DIR_SRC)/r_draw.o       \
	$(DIR_SRC)/r_filter.o     \
	$(DIR_SRC)/r_fps.o        \
	$(DIR_SRC)/r_main.o       \
	$(DIR_SRC)/r_patch.o      \
	$(DIR_SRC)/r_plane.o      \
	$(DIR_SRC)/r_segs.o       \
	$(DIR_SRC)/r_sky.o        \
	$(DIR_SRC)/r_things.o     \
	$(DIR_SRC)/s_sound.o      \
	$(DIR_SRC)/sounds.o       \
	$(DIR_SRC)/st_lib.o       \
	$(DIR_SRC)/st_stuff.o     \
	$(DIR_SRC)/tables.o       \
	$(DIR_SRC)/v_video.o      \
	$(DIR_SRC)/version.o      \
	$(DIR_SRC)/w_memcache.o   \
	$(DIR_SRC)/w_wad.o        \
	$(DIR_SRC)/wi_stuff.o     \
	$(DIR_SRC)/z_bmalloc.o    \
	$(DIR_SRC)/z_zone.o

OBJS = \
	$(PRBOOM_OBJS)

all: all_auxdata

# Add ELF and program headers into special section 'auxdata' of binary
all_auxdata: $(BINS)
	$(ADD_AUXDATA) $(BINS)

prboom: $(PRBOOM_OBJS)
	$(CC) $(LDFLAGS) $^ $(LDADD) $(EXT_LDADD) -lm -o $@

clean:
	rm -f $(BINS) $(OBJS)

include bmetal.mk
