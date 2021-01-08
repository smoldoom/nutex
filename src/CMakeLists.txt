set(SOURCE_FILES
    color.c         color.h
                    config.h
    compose.c
    deutex.c        deutex.h
    endianio.c      endianio.h
    endianm.c       endianm.h
    extract.c       extract.h
    ident.c         ident.h
    listdir.c
    lists.c         lists.h
    lzw.c
    merge.c         merge.h
    mkwad.c         mkwad.h
    png_tools.c     png_tools.h
    picture.c       picture.h
    sound.c         sound.h
    sscript.c       sscript.h
    text.c          text.h
    texture.c       texture.h
    tools.c         tools.h
    usedidx.c       usedidx.h
    wadio.c         wadio.h)

find_package(PNG REQUIRED)
include_directories(${PNG_INCLUDE_DIR})
add_executable("deutex" ${SOURCE_FILES})
target_link_libraries("deutex" ${PNG_LIBRARY})
