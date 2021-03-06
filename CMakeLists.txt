cmake_minimum_required(VERSION 3.1)
project(dirt)

add_subdirectory(ext ext_build)

## include directories
include_directories(${PROJECT_SOURCE_DIR}/src
                    ${PROJECT_SOURCE_DIR}/include
                    ${PROJECT_SOURCE_DIR}/ext/tinyformat
                    ${PROJECT_SOURCE_DIR}/ext/json
                    ${PROJECT_SOURCE_DIR}/ext/stb_image
                    ${PROJECT_SOURCE_DIR}/ext/rang/include
                    ${PROJECT_SOURCE_DIR}/ext/filesystem
                    ${PROJECT_SOURCE_DIR}/ext/pcg32
)

set(dirt_headers
    include/dirt/argparse.h
    include/dirt/array2d.h
    include/dirt/bbh.h
    include/dirt/box.h
    include/dirt/camera.h
    include/dirt/common.h
    include/dirt/fwd.h
    include/dirt/image.h
    include/dirt/material.h
    include/dirt/mesh.h
    include/dirt/obj.h
    include/dirt/parser.h
    include/dirt/perlin.h
    include/dirt/primetable.h
    include/dirt/progress.h
    include/dirt/quad.h
    include/dirt/ray.h
    include/dirt/sampler.h
    include/dirt/scene.h
    include/dirt/sphere.h
    include/dirt/surface.h
    include/dirt/surfacegroup.h
    include/dirt/texture.h
    include/dirt/timer.h
    include/dirt/transform.h
    include/dirt/vec.h
)

set(dirt_srcs
    src/argparse.cpp
    src/bbh.cpp
    src/common.cpp
    src/image.cpp
    src/material.cpp
    src/mesh.cpp
    src/obj.cpp
    src/parser.cpp
    src/perlin.cpp
    src/progress.cpp
    src/quad.cpp
    src/sampler.cpp
    src/scene.cpp
    src/sphere.cpp
    src/surface.cpp
    src/surfacegroup.cpp
    src/testscenes.cpp
    src/texture.cpp
)

# Compile core dirt library
add_library(dirt_lib STATIC
    ${dirt_headers}
    ${dirt_srcs}
)

add_executable(dirt src/01_dirt.cpp)
add_executable(03_sample_test src/03_sample_test.cpp)
add_executable(03_point_gen src/03_point_gen.cpp)

target_link_libraries(dirt dirt_lib)
target_link_libraries(03_sample_test dirt_lib)
target_link_libraries(03_point_gen dirt_lib)

SOURCE_GROUP("ext\\tinyformat" FILES ${ext_tinyformat_srcs})
SOURCE_GROUP("ext\\json" FILES ${ext_json_srcs})
SOURCE_GROUP("ext\\stb_image" FILES ${ext_stb_image_srcs})
SOURCE_GROUP("ext\\rang" FILES ${ext_rang_srcs})
SOURCE_GROUP("ext\\filesystem" FILES ${ext_filesystem_srcs})
SOURCE_GROUP("ext\\pcg32" FILES ${ext_pcg32_srcs})
SOURCE_GROUP("dirt\\header files" FILES ${dirt_headers})
SOURCE_GROUP("dirt\\source files" FILES ${dirt_srcs})
