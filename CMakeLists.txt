cmake_minimum_required(VERSION 2.8)

project(lvgl-sim)


file(GLOB_RECURSE LVGL_SRC "lvgl/*.c")

include_directories(${CMAKE_SOURCE_DIR})

include_directories(lgvl)

add_library(lvgl ${LVGL_SRC})

file(GLOB_RECURSE LVGL_DRV_SRC "lv_drivers/*.c")

add_library(lvgl_drv ${LVGL_DRV_SRC})

file(GLOB_RECURSE DEMO_SRC "lv_examples/lv_apps/demo/*.[ch]")

add_executable(demo ${DEMO_SRC} "main.c" "lv_conf.h" "lv_ex_conf.h" "lv_drv_conf.h" "mouse_cursor_icon.c")

find_package(SDL2)

include_directories(${SDL2_INCLUDE_DIRS})

target_link_libraries(demo lvgl lvgl_drv ${SDL2_LIBRARIES})
