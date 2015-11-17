cmake_minimum_required (VERSION 3.0) 
project (mongoose.cget C CXX)

find_package(Git)

if(NOT EXISTS ${CMAKE_CURRENT_LIST_DIR}/dl)
execute_process(COMMAND
  ${GIT_EXECUTABLE} clone https://github.com/cesanta/mongoose ${CMAKE_CURRENT_LIST_DIR}/dl --depth=1)
endif()

add_library(mongoose ${CMAKE_CURRENT_LIST_DIR}/dl/mongoose.c)

find_package (Threads)
target_link_libraries (mongoose ${CMAKE_THREAD_LIBS_INIT} ${CMAKE_DL_LIBS})

install(TARGETS mongoose DESTINATION lib)
install(FILES ${CMAKE_CURRENT_LIST_DIR}/dl/mongoose.h DESTINATION include)
  
