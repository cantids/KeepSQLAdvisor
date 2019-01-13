cmake_minimum_required (VERSION 2.6)
project(sqladvisor)

# /usr/local/sqlparser为sqlparser库安装目录，必要时进行修改
include_directories("/usr/local/sqlparser/include")
include_directories("/usr/local/sqlparser/include/regex")

# 默认的是mac上通过brew install glib后的头文件路径，其它安装方式，
# 或者其它操作系统需要酌情修改，再进行cmake操作
include_directories("/usr/lib64/glib-2.0/include")
include_directories("/usr/local/include/glib-2.0")

# 忽略，此为开发者Debug时的link目录。
link_directories("/data/JDB/SQLAdvisor/cmake-build-debug/sql")

# 正常安装sqlparser时的lib目录
link_directories("/usr/local/sqlparser/lib/")

# glib动态连接库目录
link_directories("/usr/local/lib/")

set(SQLADVISOR_SRC main.cc)
add_executable(sqladvisor ${SQLADVISOR_SRC})

# 如果是sqlparser debug库，则应连接的库为sqlparser-debug
target_link_libraries(sqladvisor sqlparser-debug)
# mysql客户端API
target_link_libraries(sqladvisor mysqlclient)
# glib2
target_link_libraries(sqladvisor glib-2.0)
