cmake_minimum_required(VERSION 2.8)
project(myslam)

#set(CMAKE_BUILD_TYPE Release)

set(CMAKE_CXX_FLAGS "-std=c++11 -Wall")
set(CMAKE_CXX_FLAGS_RELEASE  "-std=c++11 -fopenmp -pthread")

list(APPEND CMAKE_MODULE_PATH ${PROJECT_SOURCE_DIR}/cmake_modules)
set(EXECUTABLE_OUTPUT_PATH ${PROJECT_SOURCE_DIR}/bin)
set(LIBRARY_OUTPUT_PATH ${PROJECT_SOURCE_DIR}/lib)

set(g2o_DIR /home/jaemin/slambook2/3rdparty/install/lib/cmake/g2o)
set(GTest_DIR /home/jaemin/slambook2/3rdparty/install/lib/cmake/GTest)
set(Pangolin_DIR /home/jaemin/slambook2/3rdparty/install/lib/cmake/Pangolin)
set(DBoW3_DIR /home/jaemin/slambook2/3rdparty/install/lib/cmake/DBoW3)
set(Ceres_DIR /home/jaemin/slambook2/3rdparty/install/lib/cmake/Ceres)

############### dependencies ######################
# Eigen
include_directories("/usr/include/eigen3")

# OpenCV
find_package(OpenCV REQUIRED)
include_directories(${OpenCV_INCLUDE_DIRS})

# pangolin
find_package(Pangolin REQUIRED )
include_directories(${Pangolin_INCLUDE_DIRS})

# Sophus
find_package(Sophus REQUIRED )
include_directories(${Sophus_INCLUDE_DIRS})

# G2O
find_package(g2o REQUIRED)
include_directories(${G2O_INCLUDE_DIRS})

# glog
find_package(Glog REQUIRED)
include_directories(${GLOG_INCLUDE_DIRS})

# gtest
find_package(GTest REQUIRED NO_DEFAULT_PATH)
include_directories(${GTEST_INCLUDE_DIRS})

# gflags
find_package(GFlags REQUIRED)
include_directories(${GFLAGS_INCLUDE_DIRS})

# csparse
find_package(CSparse REQUIRED)
include_directories(${CSPARSE_INCLUDE_DIR})

set(THIRD_PARTY_LIBS
        ${OpenCV_LIBS}
        ${Sophus_LIBRARIES}
        ${Pangolin_LIBRARIES} GL GLU GLEW glut
        g2o::core g2o::stuff g2o::types_sba g2o::solver_csparse g2o::csparse_extension
        ${GTEST_BOTH_LIBRARIES}
        GTest::gtest GTest::gtest_main GTest::gmock GTest::gmock_main
        ${GLOG_LIBRARIES}
        ${GFLAGS_LIBRARIES}
        pthread
        ${CSPARSE_LIBRARY}
        )

enable_testing()

############### source and test ######################
include_directories(${PROJECT_SOURCE_DIR}/include)
add_subdirectory(src)
add_subdirectory(test)
add_subdirectory(app)
