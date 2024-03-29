cmake_minimum_required(VERSION 3.10.2)

project(nemu)

include_directories(${PROJECT_SOURCE_DIR}/nemu/include ${PROJECT_SOURCE_DIR}/include ${PROJECT_SOURCE_DIR}/libs/nemu-ref/include)

aux_source_directory(${PROJECT_SOURCE_DIR}/nemu/src NEMU_DIR_SRCS)
aux_source_directory(${PROJECT_SOURCE_DIR}/nemu/src/cpu NEMU_DIR_SRCS)
aux_source_directory(${PROJECT_SOURCE_DIR}/src/cpu/decode NEMU_DIR_SRCS)
aux_source_directory(${PROJECT_SOURCE_DIR}/nemu/src/cpu/instr NEMU_DIR_SRCS)
aux_source_directory(${PROJECT_SOURCE_DIR}/nemu/src/cpu/test NEMU_DIR_SRCS)
aux_source_directory(${PROJECT_SOURCE_DIR}/nemu/src/device NEMU_DIR_SRCS)
aux_source_directory(${PROJECT_SOURCE_DIR}/nemu/src/device/dev NEMU_DIR_SRCS)
aux_source_directory(${PROJECT_SOURCE_DIR}/nemu/src/device/io NEMU_DIR_SRCS)
aux_source_directory(${PROJECT_SOURCE_DIR}/nemu/src/memory NEMU_DIR_SRCS)
aux_source_directory(${PROJECT_SOURCE_DIR}/nemu/src/memory/mmu NEMU_DIR_SRCS)
aux_source_directory(${PROJECT_SOURCE_DIR}/nemu/src/monitor NEMU_DIR_SRCS)

set(NEMU ${NEMU_DIR_SRCS})

set(CMAKE_C_FLAGS "-m32")
set(CMAKE_CXX_FLAGS "-m32")

add_executable(nemu ${NEMU})
set_target_properties(nemu PROPERTIES COMPILE_FLAGS "-m32 -ggdb3 -MP -Wall -Werror -O2" LINK_FLAGS "-m32")
target_link_libraries(nemu PRIVATE readline SDL ${PROJECT_SOURCE_DIR}/libs/nemu-ref/lib-nemu-ref.a)