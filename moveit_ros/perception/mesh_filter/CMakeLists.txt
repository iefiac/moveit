set(MOVEIT_LIB_NAME moveit_mesh_filter)

add_library(${MOVEIT_LIB_NAME}
  src/mesh_filter_base.cpp
  src/sensor_model.cpp
  src/stereo_camera_model.cpp
  src/gl_renderer.cpp
  src/gl_mesh.cpp
  )

target_link_libraries(${MOVEIT_LIB_NAME} ${catkin_LIBRARIES} ${gl_LIBS} glut GLEW)

# Can only run this test if we have a display
if (DEFINED ENV{DISPLAY} AND NOT $ENV{DISPLAY} STREQUAL "")
  catkin_add_gtest(mesh_filter_test test/mesh_filter_test.cpp)
  target_link_libraries(mesh_filter_test ${catkin_LIBRARIES} ${Boost_LIBRARIES} moveit_mesh_filter)
else()
  message("No display, will not configure tests for moveit_ros_perception/mesh_filter")
endif()

install(TARGETS ${MOVEIT_LIB_NAME} LIBRARY DESTINATION lib)
install(DIRECTORY include/ DESTINATION include)
