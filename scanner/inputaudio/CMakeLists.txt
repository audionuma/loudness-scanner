cmake_minimum_required(VERSION 2.8.9)

find_package(PkgConfig)
if(PKG_CONFIG_FOUND)
  pkg_check_modules(GMODULE20 gmodule-2.0)
endif()

if(GMODULE20_FOUND AND NOT DISABLE_GLIB20)
  set(INPUT_INCLUDE_DIR ${CMAKE_CURRENT_SOURCE_DIR})

  add_subdirectory(sndfile)
  add_subdirectory(mpg123)
  add_subdirectory(mpcdec)
  add_subdirectory(ffmpeg)
  add_subdirectory(gstreamer)

  include_directories(SYSTEM ${GMODULE20_INCLUDE_DIRS})
  link_directories(          ${GMODULE20_LIBRARY_DIRS})
  add_definitions(           ${GMODULE20_CFLAGS_OTHER})

  add_library(input input)

  target_link_libraries(input ${GMODULE20_LIBRARIES})
endif()
