set(EXTERNAL_LIBS "mariadb uv")

add_executable(test1 test1.c)
target_link_libraries(test1 mysqlasync)
target_link_libraries(test1 ${MARIADB_LIBRARY})
target_link_libraries(test1 ${LIBUV_LIBRARIES})

install(TARGETS test1 DESTINATION bin/libmysqlasync)
