project (cork64)

cmake_minimum_required (VERSION 2.8.6)

include_directories("./")
include_directories("./accel")
include_directories("./file_formats")
include_directories("./isct")
include_directories("./math")
include_directories("./mpz")
include_directories("./mesh")
include_directories("./rawmesh")
include_directories("./util")

file(
	GLOB cork_SRC
	"./*.cpp"
	"./*.h"		
	"./accel/*.cpp"
	"./accel/*.h"
	"./file_formats/*.cpp"
	"./file_formats/*.h"
	"./isct/*.cpp"
	"./isct/*.h"
	"./math/*.cpp"
	"./math/*.h"
	"./mesh/*.cpp"
	"./mesh/*.h"
	"./rawmesh/*.cpp"
	"./rawmesh/*.h"
	"./util/*.cpp"
	"./util/*.h"
)

file(
	GLOB public_headers
	"./*.h"
)

add_definitions(-D_USE_MATH_DEFINES -DNOMINMAX)
#add_definitions(-D_LIB)

add_library(cork64 SHARED ${cork_SRC})

#link mpir

#install public facing headers and lib
install (TARGETS cork64 DESTINATION ${PROJECT_SOURCE_DIR}/lib)
install (FILES ${public_headers} DESTINATION ${PROJECT_SOURCE_DIR}/include)

