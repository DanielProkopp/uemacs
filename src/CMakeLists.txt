cmake_minimum_required(VERSION 3.20)


add_library(
    ${PROJECT_NAME}SRCS STATIC

    ansi.c
    basic.c
    bind.c
    buffer.c
    crypt.c
    display.c
    eval.c
    exec.c
    file.c
    fileio.c
    globals.c
    ibmpc.c
    input.c
    isearch.c
    line.c
    lock.c
    names.c
    pklock.c
    posix.c
    random.c
    region.c
    search.c
    spawn.c
    tcap.c
    termio.c
    usage.c
    utf8.c
    util.c
    version.c
    vmsvt.c
    vt52.c
    window.c
    word.c
    wrapper.c
)


add_executable(
    ${PROJECT_NAME}

    main.c
)

target_link_libraries(
    ${PROJECT_NAME}

    PUBLIC
        ${PROJECT_NAME}SRCS
)

target_link_libraries(
    ${PROJECT_NAME}SRCS

    PUBLIC
        ncurses
)

target_include_directories(
    ${PROJECT_NAME}SRCS

    PUBLIC
        ../inc
)

if (UNIX)
    add_definitions(
        -DAUTOCONF 
        -DPOSIX 
        -DUSG 
        -D_XOPEN_SOURCE=600 
        -D_GNU_SOURCE
    )
endif (UNIX)

if (APPLE)
    add_definitions(
        -DAUTOCONF 
        -DPOSIX 
        -DSYSV 
        -D_DARWIN_C_SOURCE 
        -D_BSD_SOURCE 
        -D_SVID_SOURCE 
        -D_XOPEN_SOURCE=600
    )
endif (APPLE)


add_custom_target(
    run
    
    COMMAND
        ${CMAKE_CURRENT_BINARY_DIR}/${PROJECT_NAME}

    USES_TERMINAL
)