# cmake vivalib
INCLUDE_DIRECTORIES(${CMAKE_SOURCE_DIR}/viva)

FILE(GLOB viva_files
	"*.h"
	"*.cpp"
)

ADD_LIBRARY(vivalib  ${viva_files})

