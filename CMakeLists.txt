SET(project_name "vivaVideo")
CMAKE_MINIMUM_REQUIRED(VERSION 2.8)

PROJECT("${project_name}")
SET(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -std=c++0x -fpermissive")

# add opencv package to the project
FIND_PACKAGE( OpenCV REQUIRED )
INCLUDE_DIRECTORIES( ${OpenCV_INCLUDE_DIRS} ) 
SET(OpenCV_LIBRARIES "opencv_video;opencv_ts;opencv_ml;opencv_objdetect;opencv_imgproc;opencv_highgui;opencv_features2d;opencv_core;")

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

SUBDIRS(viva)
INCLUDE_DIRECTORIES(${CMAKE_SOURCE_DIR}/viva) 

ADD_EXECUTABLE(${project_name} ${files})
TARGET_LINK_LIBRARIES( ${project_name} ${OpenCV_LIBRARIES})
TARGET_LINK_LIBRARIES( ${project_name}  vivalib )

LIST(REMOVE_ITEM resources ${files} ${hidden} "${CMAKE_SOURCE_DIR}/CMakeLists.txt")
FILE(COPY ${resources} DESTINATION "Debug")
FILE(COPY ${resources} DESTINATION "Release")





