# Use system packages if available
find_package(ZLIB REQUIRED)
find_package(BZip2 REQUIRED)

# Set in parent scope
set(ZLIB_LIBRARY ${ZLIB_LIBRARY} PARENT_SCOPE)
set(BZIP2_LIBRARIES ${BZIP2_LIBRARIES} PARENT_SCOPE)

# Roll the rest up into a big ball and compile it by itself
set(EXTERNAL_SOURCES
)
file(GLOB_RECURSE EXTERNAL_SOURCES
	*.cpp
	*.cxx
	dumb/*.c
	lua/*.c
	fmt/*.cc
	${SLADE_HEADERS}
	)
option(CLZMA_CFLAGS "CFLAGS for using a system-provided build of clzma/lzma-sdk")
option(CLZMA_LIBRARIES "LIBS for using a system-provided build of clzma/lzma-sdk")
if (NOT CLZMA_LIBRARIES)
	pkg_check_modules(CLZMA clzma)
	include_directories(${CLZMA_INCLUDE_DIRS})
else ()
	set(EXTERNAL_SOURCES ${EXTERNAL_SOURCES} lzma/C/LzmaDec.c)
	include_directories(lzma/C)
endif ()

add_library(external STATIC ${EXTERNAL_SOURCES})
target_link_libraries(external ${CLZMA_LIBRARIES} ${ZLIB_LIBRARY})
set(EXTERNAL_LIBRARIES external PARENT_SCOPE)
