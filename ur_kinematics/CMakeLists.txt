cmake_minimum_required(VERSION 3.5.0)
project(ur_kinematics VERSION 0.1.0 LANGUAGES CXX)


#find_package(catkin REQUIRED COMPONENTS roscpp geometry_msgs moveit_core moveit_kinematics moveit_ros_planning pluginlib tf_conversions)

find_package(Boost REQUIRED COMPONENTS system)


###########
## Build ##
###########

#add_library(ur3_kin SHARED src/ur_kin.cpp)
#set_target_properties(ur3_kin PROPERTIES COMPILE_DEFINITIONS "UR3_PARAMS")
#target_link_libraries(ur3_kin PUBLIC
#  ${Boost_LIBRARIES})
#target_compile_options(ur3_kin PRIVATE -Wall -Wextra -Wsuggest-override -Wconversion -Wsign-conversion)
#if(CXX_FEATURE_FOUND EQUAL "-1")
#    target_compile_options(ur3_kin PUBLIC -std=c++11)
#else()
#    target_compile_features(ur3_kin PUBLIC cxx_std_11)
#endif()
#target_include_directories(ur3_kin PUBLIC
#    "$<BUILD_INTERFACE:${CMAKE_CURRENT_SOURCE_DIR}/include>"
#    "$<INSTALL_INTERFACE:include>")
#target_include_directories(ur3_kin SYSTEM PUBLIC 
#  ${Boost_INCLUDE_DIRS})

#add_library(ur5_kin SHARED src/ur_kin.cpp)
#set_target_properties(ur5_kin PROPERTIES COMPILE_DEFINITIONS "UR5_PARAMS")
#target_link_libraries(ur5_kin PUBLIC
#  ${Boost_LIBRARIES})
#target_compile_options(ur5_kin PRIVATE -Wall -Wextra -Wsuggest-override -Wconversion -Wsign-conversion)
#if(CXX_FEATURE_FOUND EQUAL "-1")
#    target_compile_options(ur5_kin PUBLIC -std=c++11)
#else()
#    target_compile_features(ur5_kin PUBLIC cxx_std_11)
#endif()
#target_include_directories(ur5_kin PUBLIC
#    "$<BUILD_INTERFACE:${CMAKE_CURRENT_SOURCE_DIR}/include>"
#    "$<INSTALL_INTERFACE:include>")
#target_include_directories(ur5_kin SYSTEM PUBLIC 
#  ${Boost_INCLUDE_DIRS})

add_library(ur10_kin SHARED src/ur_kin.cpp)
set_target_properties(ur10_kin PROPERTIES COMPILE_DEFINITIONS "UR10_PARAMS")
target_link_libraries(ur10_kin PUBLIC
  ${Boost_LIBRARIES})
target_compile_options(ur10_kin PRIVATE -Wall -Wextra -Wsuggest-override -Wconversion -Wsign-conversion)
if(CXX_FEATURE_FOUND EQUAL "-1")
    target_compile_options(ur10_kin PUBLIC -std=c++11)
else()
    target_compile_features(ur10_kin PUBLIC cxx_std_11)
endif()
target_include_directories(ur10_kin PUBLIC
    "$<BUILD_INTERFACE:${CMAKE_CURRENT_SOURCE_DIR}/include>"
    "$<INSTALL_INTERFACE:include>")
target_include_directories(ur10_kin SYSTEM PUBLIC 
  ${Boost_INCLUDE_DIRS})

#############
## Install ##
#############

#list (APPEND PACKAGE_LIBRARIES ur3_kin)
#list (APPEND PACKAGE_LIBRARIES ur5_kin)
list (APPEND PACKAGE_LIBRARIES ur10_kin)
 
# Mark executables and/or libraries for installation
install(TARGETS ${PACKAGE_LIBRARIES}
    EXPORT ${PROJECT_NAME}-targets DESTINATION lib)
install(EXPORT ${PROJECT_NAME}-targets
    NAMESPACE ur_kinematics:: DESTINATION lib/cmake/${PROJECT_NAME})
 
# Mark cpp header files for installation
install(DIRECTORY include/${PROJECT_NAME}
  DESTINATION include
  FILES_MATCHING PATTERN "*.h" PATTERN "*.hpp"
  PATTERN ".svn" EXCLUDE
 )
 
install(FILES package.xml DESTINATION share/${PROJECT_NAME})
 
# Create cmake config files
include(CMakePackageConfigHelpers)
configure_package_config_file(
    ${CMAKE_CURRENT_LIST_DIR}/cmake/${PROJECT_NAME}-config.cmake.in
    ${CMAKE_CURRENT_BINARY_DIR}/${PROJECT_NAME}-config.cmake
    INSTALL_DESTINATION lib/cmake/${PROJECT_NAME}
    NO_CHECK_REQUIRED_COMPONENTS_MACRO)
 
write_basic_package_version_file(
    ${CMAKE_CURRENT_BINARY_DIR}/${PROJECT_NAME}-config-version.cmake
    VERSION ${PROJECT_VERSION} COMPATIBILITY ExactVersion)
 
install(FILES
    "${CMAKE_CURRENT_BINARY_DIR}/${PROJECT_NAME}-config.cmake"
    "${CMAKE_CURRENT_BINARY_DIR}/${PROJECT_NAME}-config-version.cmake"
    DESTINATION lib/cmake/${PROJECT_NAME})
 
export(EXPORT ${PROJECT_NAME}-targets FILE
    ${CMAKE_CURRENT_BINARY_DIR}/${PROJECT_NAME}-targets.cmake)
