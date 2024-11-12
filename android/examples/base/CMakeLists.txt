file(GLOB BASE_SRC "../../../base/*.cpp" "../../../external/imgui/*.cpp")

add_library(libbase SHARED ${BASE_SRC})

include_directories(${BASE_DIR})
include_directories(../../../external)
include_directories(../../../external/glm)
include_directories(../../../external/gli)
include_directories(../../../external/imgui)
include_directories(${EXTERNAL_DIR}/tinygltf)
include_directories(${ANDROID_NDK}/sources/android/native_app_glue)

set(KTX_DIR ../../../external/ktx)
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
		${KTX_DIR}/lib/basis_transcode.cpp
	${KTX_DIR}/lib/filestream.c
)
set(KTX_INCLUDE
	${KTX_DIR}/include
	${KTX_DIR}/lib
	${KTX_DIR}/utils
	${KTX_DIR}/external
	${KTX_DIR}/external/basisu/zstd
	${KTX_DIR}/other_include
)

add_library(libktx ${KTX_SOURCES})
target_include_directories(libktx PUBLIC ${KTX_INCLUDE})
set_property(TARGET libktx PROPERTY FOLDER "external")


target_link_libraries(
	libbase
	android
	log
	z
	libktx
)
