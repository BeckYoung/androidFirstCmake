cmake_minimum_required(VERSION 3.4.1)

# set(LIB_INSTALL_DIR lib CACHE STRING "Install location of libraries")  # CACHE STRING  指全局缓存变量

add_library(test-shared SHARED Test.c)

add_library(test-static STATIC Test.c)

# target_link_libraries(test-shared)

ADD_EXECUTABLE(Test Test.c)

# DESTINATION选项指定了一个文件会安装到磁盘的哪个路径下。若果给出的是全路径（以反斜杠或者驱动器名开头），
# 它会被直接使用。如果给出的是相对路径，它会被解释为相对于CMAKE_INSTALL_PREFIX的值的相对路径。

set_target_properties(test-static PROPERTIES OUTPUT_NAME test)
set_target_properties(test-shared PROPERTIES OUTPUT_NAME test)
install(TARGETS test-static ARCHIVE DESTINATION lib)
install(TARGETS test-shared LIBRARY DESTINATION lib)

install(TARGETS Test RUNTIME DESTINATION bin)

install(FILES Test.h DESTINATION include)