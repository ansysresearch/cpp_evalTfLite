cmake_minimum_required(VERSION 3.16)

# set the project name and version
project(TestingTfLiteCpuDeployment 
		VERSION 0.1 
		DESCRIPTION "An exe testing TensorflowLite cpu Library for evalution and deployment" 
		LANGUAGES CXX)

# specify the C++ standard
#set(CMAKE_CXX_STANDARD 11)
#set(CMAKE_CXX_STANDARD_REQUIRED ON)
#set(CMAKE_CXX_EXTENSIONS OFF)

set(TENSORFLOW_SOURCE_DIR "" CACHE PATH
  "Directory that contains the TensorFlow project" )
if(NOT TENSORFLOW_SOURCE_DIR)
  get_filename_component(TENSORFLOW_SOURCE_DIR
    "${CMAKE_CURRENT_LIST_DIR}/tensorflow_src/" ABSOLUTE)
endif()


# add the TensorflowLite library
add_subdirectory(
  "${TENSORFLOW_SOURCE_DIR}/tensorflow/lite"
  "${CMAKE_CURRENT_BINARY_DIR}/tensorflow-lite" EXCLUDE_FROM_ALL)

# add the executable
add_executable(TestingTfLiteCpuDeployment "")
target_sources(TestingTfLiteCpuDeployment
    PRIVATE test.cc)


target_link_libraries(TestingTfLiteCpuDeployment PUBLIC tensorflow-lite)
