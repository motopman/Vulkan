file(GLOB BASE_SRC "*.cpp" "*.hpp" "*.h" "../external/imgui/*.cpp")
file(GLOB BASE_HEADERS "*.hpp" "*.h")

set(KTX_DIR ${CMAKE_CURRENT_SOURCE_DIR}/../external/ktx)
set(KTX_SOURCES
    ${KTX_DIR}/external/basisu/transcoder/basisu_containers.h
    ${KTX_DIR}/external/basisu/transcoder/basisu_containers_impl.h
    ${KTX_DIR}/external/basisu/transcoder/basisu_file_headers.h
    ${KTX_DIR}/external/basisu/transcoder/basisu_transcoder_internal.h
    ${KTX_DIR}/external/basisu/transcoder/basisu_transcoder_uastc.h
    ${KTX_DIR}/external/basisu/transcoder/basisu_transcoder.cpp
    ${KTX_DIR}/external/basisu/transcoder/basisu_transcoder.h
    ${KTX_DIR}/external/basisu/transcoder/basisu.h
    ${KTX_DIR}/lib/miniz_wrapper.cpp
    ${KTX_DIR}/external/basisu/zstd/zstd.c
    ${KTX_DIR}/external/dfdutils/createdfd.c
    ${KTX_DIR}/external/dfdutils/colourspaces.c
    ${KTX_DIR}/external/dfdutils/dfd.h
    ${KTX_DIR}/external/dfdutils/interpretdfd.c
    ${KTX_DIR}/external/dfdutils/printdfd.c
    ${KTX_DIR}/external/dfdutils/queries.c
    ${KTX_DIR}/external/dfdutils/vk2dfd.c
    ${KTX_DIR}/external/dfdutils/vk2dfd.inl
    ${KTX_DIR}/external/dfdutils/vulkan/vk_platform.h
    ${KTX_DIR}/external/dfdutils/vulkan/vulkan_core.h
    ${KTX_DIR}/lib/texture.c
    ${KTX_DIR}/lib/texture1.c
    ${KTX_DIR}/lib/texture2.c
    ${KTX_DIR}/lib/hashlist.c
    ${KTX_DIR}/lib/checkheader.c
    ${KTX_DIR}/lib/swap.c
    ${KTX_DIR}/lib/memstream.c
    ${KTX_DIR}/lib/vk2gl.h
    ${KTX_DIR}/lib/vk_format.h
    ${KTX_DIR}/lib/vkformat_check.c
    ${KTX_DIR}/lib/vkformat_enum.h
    ${KTX_DIR}/lib/vkformat_str.c
    ${KTX_DIR}/lib/vkformat_typesize.c
    ${KTX_DIR}/lib/filestream.c)

add_library(base STATIC ${BASE_SRC} ${KTX_SOURCES})
if(WIN32)
    target_link_libraries(base ${Vulkan_LIBRARY} ${WINLIBS})
 else(WIN32)
    target_link_libraries(base ${Vulkan_LIBRARY} ${XCB_LIBRARIES} ${WAYLAND_CLIENT_LIBRARIES} ${CMAKE_THREAD_LIBS_INIT})
endif(WIN32)