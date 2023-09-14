
cmake_minimum_required(VERSION 3.5)
project(katzenpoopy C)
project(katzenpoopy)

# The source file main.c contains app_main() definition
add_subdirectory(build)
add_subdirectory(inputs)
add_subdirectory(stepper)

# Provides idf_import_components and idf_link_components
include(${IDF_PATH}/tools/cmake/idf_functions.cmake)

# Do some configuration for idf_import_components. This enables creation of artifacts (which might not be
# needed) for some projects
set(IDF_BUILD_ARTIFACTS ON)
set(IDF_PROJECT_EXECUTABLE ${CMAKE_PROJECT_NAME}.elf)
set(IDF_BUILD_ARTIFACTS_DIR ${CMAKE_BINARY_DIR})

# Wraps add_subdirectory() to create library targets for components, and then `return` them using the given variable.
# In this case the variable is named `component`
idf_import_components(components ${IDF_PATH} esp-idf)

# Wraps target_link_libraries() to link processed components by idf_import_components to target
idf_link_components(${CMAKE_PROJECT_NAME}.elf "${components}")