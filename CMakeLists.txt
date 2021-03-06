cmake_minimum_required(VERSION 2.6)
project (mih)

set (CMAKE_CXX_FLAGS "-O3 -DNDEBUG")

# Relying on LD_LIBRARY_PATH to find the libs
FIND_LIBRARY (MATLAB_MAT_LIBRARY mat ENV LD_LIBRARY_PATH)
FIND_LIBRARY (MATLAB_MX_LIBRARY mx ENV LD_LIBRARY_PATH)
FIND_LIBRARY (MATLAB_MEX_LIBRARY mex ENV LD_LIBRARY_PATH)
set (MATLAB_INCLUDE_DIR ${MATLABROOT}/extern/include)
set (MATLAB_LIBRARIES ${MATLAB_MAT_LIBRARY} ${MATLAB_MX_LIBRARY} ${MATLAB_MEX_LIBRARY} )
MESSAGE (STATUS ${MATLAB_INCLUDE_DIR})
MESSAGE (STATUS ${MATLAB_LIBRARIES})

include_directories ("${PROJECT_SOURCE_DIR}/include")
include_directories (${MATLAB_INCLUDE_DIR})

add_executable (mih src/array32.cpp src/mihasher.cpp src/sparse_hashtable.cpp src/bucket_group.cpp interface/mih_interface.cpp)

target_link_libraries (mih ${MATLAB_LIBRARIES})


project (linscan)

add_executable (linscan src/linscan.cpp interface/linscan_interface.cpp)

target_link_libraries (linscan ${MATLAB_LIBRARIES})
