EXE_NAME=test


OUT_ROOT=..\out
DST_ROOT=..\dist


!IF "$(PLATFORM)" == "X64"
OUT_PROOT = $(OUT_ROOT)\x64
DST_PROOT = $(DST_ROOT)\x64
!ELSE
OUT_PROOT = $(OUT_ROOT)\x86
DST_PROOT = $(DST_ROOT)\x86
!ENDIF


!IF "$(BUILD)" == "DEBUG"
OUT_DIR = $(OUT_PROOT)\debug
DST_DIR = $(DST_PROOT)\debug
!ELSE
OUT_DIR = $(OUT_PROOT)\release
DST_DIR = $(DST_PROOT)\release
!ENDIF


!IF "$(PLATFORM)" == "X64" && "$(BUILD)" == "DEBUG" # x64 && Debug

CFLAGS = \
	/Od \
	/Gm \
	/D "_DEBUG" \
	/RTC1 \
	/Zi \
	/MTd

LFLAGS = \
	/INCREMENTAL \
	/DEBUG

!ELSEIF "$(PLATFORM)" == "X64" # x64 && Release

CFLAGS = \
	/O2 \
	/Oi \
	/GL \
	/D "NDEBUG" \
	/FD \
	/Gy \
	/Zi \
	/MT

LFLAGS = \
	/INCREMENTAL:NO \
	/OPT:REF \
	/OPT:ICF \
	/LTCG

!ELSEIF "$(BUILD)" == "DEBUG" # x86 && Debug

CFLAGS = \
	/Od \
	/Gm \
	/D "_DEBUG" \
	/RTC1 \
	/ZI \
	/MTd

LFLAGS = \
	/INCREMENTAL \
	/DEBUG

!ELSE # x86 && Release

CFLAGS = \
	/O2 \
	/Oi \
	/GL \
	/D "NDEBUG" \
	/FD \
	/Gy \
	/Zi \
	/MT

LFLAGS = \
	/INCREMENTAL:NO \
	/OPT:REF \
	/OPT:ICF \
	/LTCG

!ENDIF




all: $(EXE_NAME)


$(EXE_NAME): prepare \
	lib1.obj lib2.obj main.obj
	LINK /nologo $(LFLAGS) \
	/out:$(DST_DIR)\$(EXE_NAME).exe \
	$(OUT_DIR)\lib1.obj \
	$(OUT_DIR)\lib2.obj \
	$(OUT_DIR)\main.obj


.c.obj:
	$(CC) /nologo $(CFLAGS) /c /Fo$(OUT_DIR)\$(<B) /Fd$(OUT_DIR)\$(EXE_NAME) $<


prepare: 
!IF !EXIST($(OUT_DIR))
	MKDIR $(OUT_DIR)
!ENDIF
!IF !EXIST($(DST_DIR))
	MKDIR $(DST_DIR)
!ENDIF


clean:
!IF EXIST($(DST_PROOT))
	RMDIR /S /Q $(DST_PROOT)
!ENDIF
!IF EXIST($(OUT_PROOT))
	RMDIR /S /Q $(OUT_PROOT)
!ENDIF


