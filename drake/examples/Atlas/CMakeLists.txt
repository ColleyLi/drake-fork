add_library_with_exports(LIB_NAME drakeAtlasUtil SOURCE_FILES atlasUtil.cpp)
target_link_libraries(drakeAtlasUtil Eigen3::Eigen)
drake_install_libraries(drakeAtlasUtil)
drake_install_headers(
        atlasUtil.h
        )
drake_install_pkg_config_file(drake-atlas-util
  TARGET drakeAtlasUtil
  LIBS -ldrakeAtlasUtil
  REQUIRES eigen3)

drake_add_matlab_test(NAME examples/Atlas/robotiqHandInspector OPTIONAL bullet COMMAND robotiqHandInspector)
# drake_add_matlab_test(NAME examples/Atlas/runAtlasDynamics OPTIONAL bullet gurobi snopt COMMAND runAtlasDynamics SIZE large)  # FIXME: see #4513
drake_add_matlab_test(NAME examples/Atlas/runAtlasFootstepPlanning REQUIRES gurobi lcm libbot OPTIONAL bullet snopt COMMAND runAtlasFootstepPlanning)
drake_add_matlab_test(NAME examples/Atlas/runAtlasFrontalDynamics OPTIONAL bullet gurobi snopt COMMAND runAtlasFrontalDynamics)
drake_add_matlab_test(NAME examples/Atlas/runAtlasJumping REQUIRES spotless OPTIONAL bullet gurobi snopt COMMAND runAtlasJumping SIZE large)
drake_add_matlab_test(NAME examples/Atlas/runAtlasSagittalDynamics OPTIONAL bullet gurobi snopt COMMAND runAtlasSagittalDynamics)
drake_add_matlab_test(NAME examples/Atlas/runAtlasWalkingPlanning REQUIRES gurobi lcm libbot OPTIONAL bullet snopt COMMAND runAtlasWalkingPlanning)
drake_add_matlab_test(NAME examples/Atlas/runCOMFixedPointSearch OPTIONAL bullet gurobi COMMAND runCOMFixedPointSearch)

drake_add_matlab_test(NAME examples/Atlas/runDRCDoorTask REQUIRES iris mosek COMMAND runDRCDoorTask)

drake_add_matlab_test(NAME examples/Atlas/runRobotiqPDControl OPTIONAL bullet gurobi snopt COMMAND runRobotiqPDControl)

# if(NOT ${CMAKE_BUILD_TYPE} STREQUAL "Debug" AND UNIX) # FIXME: see #3147.
#   drake_add_matlab_test(NAME examples/Atlas/runAtlasBalancingPerturb REQUIRES gurobi lcm libbot yaml-cpp COMMAND runAtlasBalancingPerturb)
# endif()

# if(NOT ${CMAKE_BUILD_TYPE} STREQUAL "Debug" AND UNIX AND NOT APPLE) # FIXME: see #3147.
#   drake_add_matlab_test(NAME examples/Atlas/runAtlasManip REQUIRES gurobi lcm libbot yaml-cpp COMMAND runAtlasManip)
# endif()

# if(NOT ${CMAKE_BUILD_TYPE} STREQUAL "Debug" AND UNIX) # FIXME: see #3147.
#   drake_add_matlab_test(NAME examples/Atlas/runAtlasWalking REQUIRES gurobi lcm libbot yaml-cpp COMMAND runAtlasWalking SIZE large)
# endif()

# drake_add_matlab_test(NAME examples/Atlas/runAtlasBalancing REQUIRES gurobi COMMAND runAtlasBalancing)  # FIXME: see #2839
# drake_add_matlab_test(NAME examples/Atlas/runAtlasBalancingWithContactSensor REQUIRES gurobi COMMAND runAtlasBalancingWithContactSensor)  # FIXME: see #2839
# drake_add_matlab_test(NAME examples/Atlas/runAtlasHandControl REQUIRES gurobi COMMAND runAtlasHandControl)  # FIXME: see #2839

drake_add_matlab_test(NAME examples/Atlas/runRobotiqTendons COMMAND runRobotiqTendons)

# drake_add_matlab_test(NAME examples/Atlas/runDRCPracticeTerrain REQUIRES iris mosek COMMAND runDRCPracticeTerrain SIZE large)  # FIXME: see #3149

if(BUILD_TESTING)
  add_subdirectory(test)
endif()
