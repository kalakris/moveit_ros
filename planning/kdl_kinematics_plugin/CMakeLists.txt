set(MOVEIT_LIB_NAME moveit_kdl_kinematics_plugin)

add_library(${MOVEIT_LIB_NAME} src/kdl_kinematics_plugin.cpp)
target_link_libraries(${MOVEIT_LIB_NAME} moveit_robot_model_loader ${catkin_LIBRARIES})

install(TARGETS ${MOVEIT_LIB_NAME} LIBRARY DESTINATION lib)
install(DIRECTORY include/ DESTINATION include)
