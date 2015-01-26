#David Coeurjolly <david.coeurjolly@liris.cnrs.fr>
# -----------------------------------------------------------------------------
# Project definition
# -----------------------------------------------------------------------------
PROJECT(sparse-voxel-octree)

cmake_minimum_required (VERSION 2.6)


FIND_PACKAGE(SDL)

INCLUDE_DIRECTORIES(${SDL_INCLUDE_DIR})
INCLUDE_DIRECTORIES(/usr/local/include/)

INCLUDE_DIRECTORIES(${PROJECT_SOURCE_DIR}/src)

add_library(svomath
  src/math/Mat4
  src/math/Vec3
  src/math/Vec4
  src/math/MatrixStack)

add_library(svothirdparty
  src/third-party/ply
  src/third-party/plyfile
  src/third-party/tribox3)


add_definitions("-Dfseeko64=fseeko")

SET(SVO_SRC
  src/Debug
  src/Events
  src/Util
  src/Main
  src/PlyLoader
  src/VoxelData
  src/VoxelOctree
  src/ThreadBarrier)

add_executable(svo ${SVO_SRC})
target_link_libraries (svo   ${SDL_LIBRARY} svothirdparty svomath )


install(TARGETS svo
  RUNTIME DESTINATION bin
  LIBRARY DESTINATION lib
  ARCHIVE DESTINATION lib)
