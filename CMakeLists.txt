
CMAKE_MINIMUM_REQUIRED(VERSION 3.0)
SET(PROJECT_NAME "vivaVideo")
PROJECT("${PROJECT_NAME}")

SET(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -std=c++11")

# add opencv package to the project
FIND_PACKAGE( OpenCV REQUIRED )
INCLUDE_DIRECTORIES( ${OpenCV_INCLUDE_DIRS} ) 
#SET(OpenCV_LIBRARIES "opencv_video;opencv_ts;opencv_ml;opencv_objdetect;opencv_imgproc;opencv_highgui;opencv_features2d;opencv_core;")

SUBDIRS(vivalib)
INCLUDE_DIRECTORIES(${CMAKE_SOURCE_DIR}/vivalib) 

FILE(GLOB files
  "*.h"
  "*.cpp"
)
FILE(GLOB hidden
	".*"
)
FILE(GLOB resources
  "*.*"
)

MESSAGE(STATUS "Project Name: ${PROJECT_NAME}")
MESSAGE(STATUS "    OpenCV version: ${OpenCV_VERSION} ")
MESSAGE(STATUS "    libraries: ${OpenCV_LIBS}")
MESSAGE(STATUS "    include path: ${OpenCV_INCLUDE_DIRS}")

ADD_EXECUTABLE(${PROJECT_NAME} ${files})
TARGET_LINK_LIBRARIES( ${PROJECT_NAME} ${OpenCV_LIBS} vivalib)

LIST(REMOVE_ITEM resources ${files} ${hidden} "${CMAKE_SOURCE_DIR}/CMakeLists.txt")
FILE(COPY ${resources} DESTINATION "Debug")
FILE(COPY ${resources} DESTINATION "Release")





