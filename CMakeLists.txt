cmake_minimum_required(VERSION 3.5)
project(test_uvc_camera)

find_package(OpenCV 3.0 REQUIRED)
find_package (Eigen3 REQUIRED NO_MODULE)

set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -Wextra -Wall -std=c++11 -pthread -m64 -lm -ldl -rdynamic -lpthread -Wl,-rpath,$(XSENSSYS)/lib")

# set(CMAKE_CXX_STANDARD 11)
set(PROJECT_ROOT $ENV{HOME}/projects/uvc_camera)
include_directories(${PROJECT_ROOT}/include)
include_directories( ${OpenCV_INCLUDE_DIRS} )
include_directories(${Eigen3_INCLUDE_DIRS})
include_directories(/usr/include/eigen3)

set(SOURCE_FILES src/colorspaces.cpp src/uvc_camera.cpp)

add_executable(test_uvc_camera examples/test_uvc_camera.cpp ${SOURCE_FILES})
add_executable(pose_calibration_uvc_camera examples/pose_calibration_uvc_camera.cpp ${SOURCE_FILES})
add_executable(hackathon2018 examples/hackathon.cpp examples/imu.cpp examples/process_frame.cpp examples/scale.cpp examples/demo.cpp examples/features.cpp examples/circular_frame_info_array.cpp examples/utils.cpp ${SOURCE_FILES})

target_link_libraries(test_uvc_camera ${OpenCV_LIBS})
target_link_libraries(pose_calibration_uvc_camera ${OpenCV_LIBS})
target_link_libraries(hackathon2018 ${OpenCV_LIBS})
target_link_libraries(hackathon2018 ${Eigen3_LIBS})