# 最求的最低cmake程序版本
cmake_minimum_required(VERSION 3.12)

# 本工程的名字
project(Graphic)

# 本工程支持的C++标准
set(CMAKE_CXX_STANDARD 17)

add_subdirectory(application)
add_subdirectory(gpu)

#把需要拷贝的资源路径都放到ASSETS里
file(GLOB ASSETS "./assets" "thirdParty/assimp-vc143-mtd.dll")

#把ASSETS指代的目录集合的内容，都拷贝到可执行文件目录下
file(COPY ${ASSETS} DESTINATION ${CMAKE_BINARY_DIR})

# 搜寻所有的cpp，并加入SRCS变量中
aux_source_directory(. SRCS)

# 本工程用于cpp文件编译连接，生成exe
#add_executable(softRenderer ${SRCS})
add_executable(softRenderer "main.cpp")

# 将funcs.lib链接到softRender
target_link_libraries(softRenderer applicationLib gpuLib)