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

#link mpir. Requires pulling and initializing the submodule
include_directories("./mpir-generic")

#build mpir
add_subdirectory("./mpir-generic")

file(
	GLOB cork_SRC
	"./*.cpp"
	"./*.h"		
	"./accel/*.cpp"
	"./accel/*.h"
	"./file_formats/*.cpp"
	"./file_formats/*.h"
	"./isct/*.cpp"
	"./isct/*.c"
	"./isct/*.h"
	"./math/*.cpp"
	"./math/*.h"
	"./mesh/*.cpp"
	"./mesh/*.tpp"
	"./mesh/*.h"
	"./rawmesh/*.cpp"
	"./rawmesh/*.tpp"
	"./rawmesh/*.h"
	"./util/*.cpp"
	"./util/*.h"
)

file(
	GLOB public_headers
	"./*.h"
)

add_definitions(
	-D_USE_MATH_DEFINES 
	-DNOMINMAX 
	-DNO_TIMER
	-DREDUCED
	-DCDT_ONLY
	-DTRILIBRARY
	-DANSI_DECLARATORS
	)

add_definitions(-DDLLEXPORT)

add_library(cork64 SHARED ${cork_SRC})

#link mpir
target_link_libraries(cork64 mpir)


#install public facing headers and lib
install (TARGETS cork64 DESTINATION ${PROJECT_SOURCE_DIR}/lib)
install (FILES ${public_headers} DESTINATION ${PROJECT_SOURCE_DIR}/include)

