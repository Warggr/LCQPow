find_package(Eigen3 REQUIRED)
find_package(pybind11 CONFIG)

get_target_property(_includes pybind11::module INTERFACE_INCLUDE_DIRECTORIES)

macro(pybind11_add_lcqpow_module MODULE)
  pybind11_add_module(
    ${MODULE} 
    SHARED 
    ${MODULE}.cpp
  )
  target_include_directories(
    ${MODULE} 
    PRIVATE
    ${osqp_include}
  )
  target_link_libraries(
    ${MODULE} 
    PRIVATE
    PUBLIC ${PROJECT_NAME}-shared
    PRIVATE ${qpoases_lib} ${osqp_lib}
    PRIVATE Eigen3::Eigen
  )
endmacro()

pybind11_add_lcqpow_module(LCQProblem)
pybind11_add_lcqpow_module(Options)
pybind11_add_lcqpow_module(OutputStatistics)
pybind11_add_lcqpow_module(Utilities)
