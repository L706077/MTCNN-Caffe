cmake_minimum_required(VERSION 2.6)
project(mtcnn_c)

SET(CMAKE_C_COMPILER g++)
SET(CMAK_CXX_COMPILER g++)

###================
set(Caffe_DIR)
set(OpenCV_DIR "/home/ubuntu/opencv-2.4.13/release/")
find_package(Caffe REQUIRED)
###================

add_compile_options(-std=c++11)
add_compile_options(-m64)

###================
include_directories(/home/ubuntu/caffe/include)
include_directories(/home/ubuntu/caffe/build/include)
include_directories(/usr/include/hdf5/serial)

link_directories(/home/ubuntu/caffe/build/lib)
link_directories(/usr/lib/x86_64-linux-gnu/hdf5/serial)
###================

include_directories(
    ${mtcnn_c_SOURCE_DIR}/include/ 
    /usr/local/cuda/include)
link_directories(
    ${mtcnn_c_SOURCE_DIR}/lib/
    /usr/local/cuda/lib64)

add_executable(mtcnn_c main.cpp )
target_link_libraries(mtcnn_c 
    -lcaffe 
    -lboost_system 
    -lboost_filesystem
    -lopencv_core 
    -lopencv_highgui 
    -lopencv_imgproc
    -lglog
    -lgflags
    -lprotobuf
    -lm
    -lhdf5
    -lhdf5_hl
)
target_link_libraries(mtcnn_c caffe)

#install(TARGETS mtcnn_c RUNTIME DESTINATION bin)
