CMAKE_DEPENDENT_OPTION(NEKTAR_SOLVER_SHALLOW_WATER
    "Build the Shallow Water solver." ON
    "NEKTAR_BUILD_SOLVERS" OFF)

IF( NEKTAR_SOLVER_SHALLOW_WATER )
    SET(ShallowWaterSolverSource 
       ./ShallowWaterSolver.cpp
       ./EquationSystems/ShallowWaterSystem.cpp
       ./EquationSystems/LinearSWE.cpp
       ./EquationSystems/NonlinearSWE.cpp
       ./RiemannSolvers/LinearSWESolver.cpp
       ./RiemannSolvers/NonlinearSWESolver.cpp
       ./RiemannSolvers/NoSolver.cpp
       ./RiemannSolvers/LinearAverageSolver.cpp
       ./RiemannSolvers/LinearHLLSolver.cpp
       ./RiemannSolvers/AverageSolver.cpp
       ./RiemannSolvers/LaxFriedrichsSolver.cpp
       ./RiemannSolvers/HLLSolver.cpp
       ./RiemannSolvers/HLLCSolver.cpp	
	)

    ADD_SOLVER_EXECUTABLE(ShallowWaterSolver solvers 
			${ShallowWaterSolverSource})

    ADD_NEKTAR_TEST(LinearSWE_StandingWave_WallBC_CG_P4)
    ADD_NEKTAR_TEST(LinearSWE_StandingWave_WallBC_CG_P8)
    ADD_NEKTAR_TEST(LinearSWE_StandingWave_PeriodicBC_CG_P8)
    ADD_NEKTAR_TEST(LinearSWE_StandingWave_WallBC_DG_P4)
    ADD_NEKTAR_TEST(LinearSWE_StandingWave_WallBC_DG_P8)
    ADD_NEKTAR_TEST(LinearSWE_StandingWave_PeriodicBC_DG_P8)
    ADD_NEKTAR_TEST(NonlinearSWE_RossbyModon_CG_P9)
    ADD_NEKTAR_TEST(NonlinearSWE_RossbyModon_DG_P9)
ENDIF( NEKTAR_SOLVER_SHALLOW_WATER )
