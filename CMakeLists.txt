
cmake_minimum_required(VERSION 3.10)


project(project_for_jenkins VERSION 0.1)

add_library(project_for_jenkins
    src/myC.cpp
    src/myD.cpp
)

target_include_directories(project_for_jenkins PUBLIC
    $<BUILD_INTERFACE:${CMAKE_CURRENT_SOURCE_DIR}/include>
    $<INSTALL_INTERFACE:include>
    PRIVATE src
)

install(TARGETS project_for_jenkins EXPORT MyLibraryConfig
    ARCHIVE  DESTINATION ${CMAKE_PREFIX_PATH}/lib
    LIBRARY  DESTINATION ${CMAKE_PREFIX_PATH}/lib
    RUNTIME  DESTINATION ${CMAKE_PREFIX_PATH}/bin)
install(DIRECTORY include/ DESTINATION ${CMAKE_PREFIX_PATH}/include)

enable_testing()

# Every library has unit tests, of course
add_executable(testproject_for_jenkinsC
    tests/testMyC.cpp)

add_executable(testproject_for_jenkinsD
    tests/testMyD.cpp)

target_link_libraries(testproject_for_jenkinsC
    project_for_jenkins)

target_link_libraries(testproject_for_jenkinsD
    project_for_jenkins)

add_test(testproject_for_jenkinsA testproject_for_jenkinsC)
add_test(testproject_for_jenkinsB testproject_for_jenkinsD)
