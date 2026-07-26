*  exntensible markup language, holds info in the format of trees with `<tags>`
* If you were to write `<package format="1">`, tools like `colcon` and `rosdep` would read it, apply the old ROS 1 rulebook, crash when they saw tags they didn't recognize, and fail to build your package. It is strictly a versioning tag so the parsing scripts don't break.
* format 3 allows multiple dependencies to be grouped, and new metadata


* custom licenses, maintainers names + specifying the type of ros package format, node(blitz), versions etc
* ament c_make is crucial as it not only acts as a flag to follow c++ pipeline but also takes care of the backend of linking all the needed files and exporting it to ros
#### blitz
* it mainly has dependencies for the build system(colcon):
1. `<buildtool_depend>ament_cmake</buildtool_depend>` ros2 uses this cmake build system so custom import
2. `<test_depend>ament_lint_auto</test_depend>` syntax errors/stylistic mistakes
#### robot interfaces
1. `<buildtool_depend>rosidl_default_generators</buildtool_depend>` this provides the generators for the custom .msg to make c++ header files or py classes
2. `<exec_depend>rosidl_default_runtime</exec_depend>` handles underlying memory and execution logistics
3. `<member_of_group>rosidl_interface_packages</member_of_group>` custom tag for your msg to be found and used

`<export> <build_type>ament_cmake</build_type> </export>` this line makes sure colcon knows it has to pass this through cmake compilers instead of standard python

