SET(MULTI_REGIONS_SOURCES
./AssemblyMap/AssemblyMap.cpp
./AssemblyMap/AssemblyMapCG.cpp
./AssemblyMap/AssemblyMapDG.cpp
./AssemblyMap/AssemblyMapCG1D.cpp
./AssemblyMap/AssemblyMapCG2D.cpp
./AssemblyMap/AssemblyMapCG3D.cpp
ContField1D.cpp
ContField2D.cpp
ContField3D.cpp
ContField3DHomogeneous1D.cpp
ContField3DHomogeneous2D.cpp
DisContField1D.cpp
DisContField2D.cpp
DisContField3D.cpp
DisContField3DHomogeneous1D.cpp
DisContField3DHomogeneous2D.cpp
ExpList.cpp
ExpList0D.cpp
ExpList1D.cpp
ExpList2D.cpp
ExpList3D.cpp
ExpListHomogeneous1D.cpp
ExpListHomogeneous2D.cpp
ExpList2DHomogeneous1D.cpp
ExpList1DHomogeneous2D.cpp
ExpList3DHomogeneous1D.cpp
ExpList3DHomogeneous2D.cpp
GlobalLinSys.cpp
GlobalLinSysKey.cpp
GlobalLinSysDirect.cpp
GlobalLinSysDirectFull.cpp
GlobalLinSysDirectStaticCond.cpp
GlobalLinSysIterative.cpp
GlobalLinSysIterativeFull.cpp
GlobalLinSysIterativeStaticCond.cpp
GlobalMatrix.cpp
GlobalMatrixKey.cpp
GlobalOptimizationParameters.cpp
Preconditioner.cpp
PreconditionerDiagonal.cpp
PreconditionerLowEnergy.cpp
PreconditionerBlock.cpp
SubStructuredGraph.cpp
)

SET(MULTI_REGIONS_HEADERS
ContField1D.h
ContField2D.h
ContField3D.h
ContField3DHomogeneous1D.h
ContField3DHomogeneous2D.h
DisContField1D.h
DisContField2D.h
DisContField3D.h
DisContField3DHomogeneous1D.h
DisContField3DHomogeneous2D.h
ExpList.h
ExpList0D.h
ExpList1D.h
ExpList2D.h
ExpList3D.h
ExpListHomogeneous1D.h
ExpListHomogeneous2D.h
ExpList2DHomogeneous1D.h
ExpList1DHomogeneous2D.h
ExpList3DHomogeneous1D.h
ExpList3DHomogeneous2D.h
GlobalLinSys.h
GlobalLinSysKey.h
GlobalLinSysDirect.h
GlobalLinSysDirectFull.h
GlobalLinSysDirectStaticCond.h
GlobalLinSysIterative.h
GlobalLinSysIterativeFull.h
GlobalLinSysIterativeStaticCond.h
GlobalMatrix.h
GlobalMatrixKey.h
GlobalOptimizationParameters.h
MultiRegions.hpp
MultiRegionsDeclspec.h
Preconditioner.h
PreconditionerDiagonal.h
PreconditionerLowEnergy.h
PreconditionerBlock.h
SubStructuredGraph.h
)

SET(ASSEMBLY_MAP_HEADERS
./AssemblyMap/AssemblyMap.h
./AssemblyMap/AssemblyMapCG.h
./AssemblyMap/AssemblyMapDG.h
./AssemblyMap/AssemblyMapCG1D.h
./AssemblyMap/AssemblyMapCG2D.h
./AssemblyMap/AssemblyMapCG3D.h
)

IF(NEKTAR_USE_MPI)
    SET(MULTI_REGIONS_HEADERS ${MULTI_REGIONS_HEADERS}
        GlobalLinSysXxt.h
        GlobalLinSysXxtFull.h
        GlobalLinSysXxtStaticCond.h
        PreconditionerLinear.h
        PreconditionerLinearWithLowEnergy.h
        PreconditionerLinearWithDiag.h
        PreconditionerLinearWithBlock.h
    )
    SET(MULTI_REGIONS_SOURCES ${MULTI_REGIONS_SOURCES}
        GlobalLinSysXxt.cpp
        GlobalLinSysXxtFull.cpp
        GlobalLinSysXxtStaticCond.cpp
        PreconditionerLinear.cpp
        PreconditionerLinearWithLowEnergy.cpp
        PreconditionerLinearWithDiag.cpp
        PreconditionerLinearWithBlock.cpp
    )
ENDIF(NEKTAR_USE_MPI)

ADD_DEFINITIONS(-DMULTI_REGIONS_EXPORTS)

ADD_NEKTAR_LIBRARY(MultiRegions lib ${NEKTAR_LIBRARY_TYPE} ${MULTI_REGIONS_SOURCES} ${MULTI_REGIONS_HEADERS} ${ASSEMBLY_MAP_HEADERS})
TARGET_LINK_LIBRARIES(MultiRegions
        optimized LibUtilities   debug LibUtilities-g
        optimized SpatialDomains debug SpatialDomains-g
        optimized LocalRegions   debug LocalRegions-g
        optimized StdRegions     debug StdRegions-g
        optimized ${TINYXML_LIB} debug ${TINYXML_LIB}
        ${Boost_THREAD_LIBRARY}
        ${Boost_IOSTREAMS_LIBRARY}
        ${Boost_DATE_TIME_LIBRARY}
        ${Boost_PROGRAM_OPTIONS_LIBRARY}
        ${Boost_SYSTEM_LIBRARY}
        ${ZLIB_LIBRARY}
	)
SET_LAPACK_LINK_LIBRARIES(MultiRegions)

INSTALL(DIRECTORY ./ DESTINATION ${NEKTAR_INCLUDE_DIR}/MultiRegions COMPONENT dev FILES_MATCHING PATTERN "*.h" PATTERN "*.hpp")



