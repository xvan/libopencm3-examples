get_filename_component(ProjectId ${CMAKE_CURRENT_LIST_DIR} NAME)
string(REPLACE " " "_" ProjectId ${ProjectId})

set(TARGET ${ProjectId})
add_executable( ${TARGET} cdcacm.c)
target_link_libraries(${TARGET} opencm3_STM32F1)

