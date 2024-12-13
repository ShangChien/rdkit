include_directories(${RDKit_ExternalDir})
include_directories(${RDKit_ExternalDir}/rapidjson-1.1.0/include)

find_package(RDKit REQUIRED)

if(RDK_BUILD_MINIMAL_LIB)
    set(MINIMAL_LIB_LIBRARIES 
        MolInterchange_static
        Abbreviations_static
        CIPLabeler_static
        MolDraw2D_static
        Depictor_static
        Descriptors_static
        SubstructMatch_static
        FileParsers_static
        SmilesParse_static
        GraphMol_static
        RDGeometryLib_static
        RDGeneral_static
        RGroupDecomposition_static
        Fingerprints_static
        RDKitDistGeomHelpers_static
        RDKitForceFieldHelpers_static
        RDKitForceFields_static
    )

    if(RDK_BUILD_INCHI_SUPPORT)
        add_definitions(-DRDK_BUILD_INCHI_SUPPORT)
        set(MINIMAL_LIB_LIBRARIES "${MINIMAL_LIB_LIBRARIES};RDInchiLib_static")
    endif()

    add_executable(RDKit_minimal jswrapper.cpp minilib.cpp JSONParsers.cpp)
    target_link_libraries(RDKit_minimal PRIVATE ${MINIMAL_LIB_LIBRARIES})
    set_target_properties(RDKit_minimal PROPERTIES LINK_FLAGS "--bind")
endif()
