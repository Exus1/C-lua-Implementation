cmake_minimum_required(VERSION 3.4)
project(e_bot)

set(CMAKE_CXX_STANDARD 11)

# Build lua library. Thanks to Baiyan Huang for https://gist.github.com/baiyanhuang/4054106
set(LUA_SOURCE_FOLDER lua_src)

set(LUA_VERSION "5.3.4")

if(WIN32)
    add_definitions( -D_CRT_SECURE_NO_WARNINGS )
endif()

set(LUA_FILES
    ${LUA_SOURCE_FOLDER}/lua-${LUA_VERSION}/lapi.c
    ${LUA_SOURCE_FOLDER}/lua-${LUA_VERSION}/lcode.c
    ${LUA_SOURCE_FOLDER}/lua-${LUA_VERSION}/lctype.c
    ${LUA_SOURCE_FOLDER}/lua-${LUA_VERSION}/ldebug.c
    ${LUA_SOURCE_FOLDER}/lua-${LUA_VERSION}/ldo.c
    ${LUA_SOURCE_FOLDER}/lua-${LUA_VERSION}/ldump.c
    ${LUA_SOURCE_FOLDER}/lua-${LUA_VERSION}/lfunc.c
    ${LUA_SOURCE_FOLDER}/lua-${LUA_VERSION}/lgc.c
    ${LUA_SOURCE_FOLDER}/lua-${LUA_VERSION}/llex.c
    ${LUA_SOURCE_FOLDER}/lua-${LUA_VERSION}/lmem.c
    ${LUA_SOURCE_FOLDER}/lua-${LUA_VERSION}/lobject.c
    ${LUA_SOURCE_FOLDER}/lua-${LUA_VERSION}/lopcodes.c
    ${LUA_SOURCE_FOLDER}/lua-${LUA_VERSION}/lparser.c
    ${LUA_SOURCE_FOLDER}/lua-${LUA_VERSION}/lstate.c
    ${LUA_SOURCE_FOLDER}/lua-${LUA_VERSION}/lstring.c
    ${LUA_SOURCE_FOLDER}/lua-${LUA_VERSION}/ltable.c
    ${LUA_SOURCE_FOLDER}/lua-${LUA_VERSION}/ltm.c
    ${LUA_SOURCE_FOLDER}/lua-${LUA_VERSION}/lundump.c
    ${LUA_SOURCE_FOLDER}/lua-${LUA_VERSION}/lvm.c
    ${LUA_SOURCE_FOLDER}/lua-${LUA_VERSION}/lzio.c
    ${LUA_SOURCE_FOLDER}/lua-${LUA_VERSION}/lauxlib.c
    ${LUA_SOURCE_FOLDER}/lua-${LUA_VERSION}/lbaselib.c
    ${LUA_SOURCE_FOLDER}/lua-${LUA_VERSION}/lbitlib.c
    ${LUA_SOURCE_FOLDER}/lua-${LUA_VERSION}/lcorolib.c
    ${LUA_SOURCE_FOLDER}/lua-${LUA_VERSION}/ldblib.c
    ${LUA_SOURCE_FOLDER}/lua-${LUA_VERSION}/liolib.c
    ${LUA_SOURCE_FOLDER}/lua-${LUA_VERSION}/lmathlib.c
    ${LUA_SOURCE_FOLDER}/lua-${LUA_VERSION}/loslib.c
    ${LUA_SOURCE_FOLDER}/lua-${LUA_VERSION}/lstrlib.c
    ${LUA_SOURCE_FOLDER}/lua-${LUA_VERSION}/ltablib.c
    ${LUA_SOURCE_FOLDER}/lua-${LUA_VERSION}/loadlib.c
    ${LUA_SOURCE_FOLDER}/lua-${LUA_VERSION}/linit.c
    ${LUA_SOURCE_FOLDER}/lua-${LUA_VERSION}/lutf8lib.c
)

add_library(lualib STATIC ${LUA_FILES})

set_target_properties(lualib PROPERTIES OUTPUT_NAME "lua")


# Build binary
include_directories(${LUA_SOURCE_FOLDER})

set(E_BOT_SOURCE_FILES main.cpp)
add_executable(e_bot ${E_BOT_SOURCE_FILES})

# Include Lua library
target_link_libraries(e_bot lualib)
