cmake_minimum_required(VERSION 2.8.3)
project(cob_generic_can)

find_package(catkin REQUIRED COMPONENTS cob_utilities libntcan libpcan)

catkin_package(
  CATKIN_DEPENDS cob_utilities libntcan libpcan
  INCLUDE_DIRS common/include
  LIBRARIES ${PROJECT_NAME}_peaksysusb ${PROJECT_NAME}_peaksys ${PROJECT_NAME}_esd
)

### BUILD ###
include_directories(common/include ${catkin_INCLUDE_DIRS})

add_library(${PROJECT_NAME}_peaksysusb common/src/CanPeakSysUSB.cpp)
add_library(${PROJECT_NAME}_peaksys common/src/CanPeakSys.cpp)
add_library(${PROJECT_NAME}_esd common/src/CanESD.cpp)

target_link_libraries(${PROJECT_NAME}_peaksysusb ${catkin_LIBRARIES})
target_link_libraries(${PROJECT_NAME}_peaksys ${catkin_LIBRARIES})
target_link_libraries(${PROJECT_NAME}_esd ${catkin_LIBRARIES})

### INSTALL ###
install(TARGETS ${PROJECT_NAME}_peaksysusb ${PROJECT_NAME}_peaksys ${PROJECT_NAME}_esd
  ARCHIVE DESTINATION ${CATKIN_PACKAGE_LIB_DESTINATION}
  LIBRARY DESTINATION ${CATKIN_PACKAGE_LIB_DESTINATION}
  RUNTIME DESTINATION ${CATKIN_PACKAGE_BIN_DESTINATION}
)

install(DIRECTORY common/include/${PROJECT_NAME}/
  DESTINATION ${CATKIN_PACKAGE_INCLUDE_DESTINATION}
)
