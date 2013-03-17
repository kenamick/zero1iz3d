cmake_minimum_required (VERSION 2.6)
project(zero1iz3d) 

### check for required libs
find_package(GLUT)
find_package(OpenGL REQUIRED)

### src
set (
        SOURCES 
	3ds_format.cpp
	3ds.cpp
	CBillBoard.cpp
	CCamera.cpp
	CDebug.cpp
	CFog.cpp
	CModel.cpp
	COpenGL.cpp
	CParticle.cpp
	CSprite.cpp
	CText.cpp
	CTexture.cpp
	CTimer.cpp
	Geometry.cpp
	main.cpp
)

### specify executable

add_executable (	
	zero1iz3d
	${SOURCES}
)

### add required libarires
set(CORELIBS ${GLUT_LIBRARY} ${OPENGL_LIBRARY})

target_link_libraries( 
	zero1iz3d
	${CORELIBS}
)

### additional defines

#add_definitions(`sdl-config --cflags`)
#add_definitions(`sdl-config --libs`)
add_definitions(-DLINUX_BUILD)

if (CMAKE_BUILD_TYPE STREQUAL "Debug")
  add_definitions(-g)
  add_definitions(-D_DEBUG)
  add_definitions(-DDEBUG)
else (CMAKE_BUILD_TYPE STREQUAL "Debug")
  add_definitions(-O3 -DNDEBUG)
endif (CMAKE_BUILD_TYPE STREQUAL "Debug")

if (UNIX AND NOT WIN32)
  if (CMAKE_SIZEOF_VOID_P MATCHES "8")
    add_definitions(-DARCH_X64)
  else (CMAKE_SIZEOF_VOID_P MATCHES "8")
    add_definitions(-DARCH_X86)
  endif (CMAKE_SIZEOF_VOID_P MATCHES "8")
endif (UNIX AND NOT WIN32)

### set runtime directory
set(zero1iz3d PROPERTIES RUNTIME_OUTPUT_DIRECTORY "dist/")
