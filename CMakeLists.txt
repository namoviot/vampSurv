cmake_minimum_required(VERSION 3.16)


project(vampSurv)                    # project name


set(CMAKE_RUNTIME_OUTPUT_DIRECTORY "${CMAKE_BINARY_DIR}/$<CONFIGURATION>")
set(CMAKE_LIBRARY_OUTPUT_DIRECTORY "${CMAKE_BINARY_DIR}/$<CONFIGURATION>")

#add_library()


add_executable(vampSurv
  main.cpp
  some.cpp
)   # build an executable from main.cpp


target_include_directories(vampSurv PRIVATE
  ${CMAKE_SOURCE_DIR}/dep/include
)


target_link_libraries(vampSurv PRIVATE
  ${CMAKE_SOURCE_DIR}/dep/libSDL3.dll.a
)


# Copy the SDL DLL after building your executable
add_custom_command(TARGET vampSurv POST_BUILD
    COMMAND ${CMAKE_COMMAND} -E copy_if_different
    "${CMAKE_SOURCE_DIR}/dep/SDL3.dll"
        $<TARGET_FILE_DIR:vampSurv>
)

