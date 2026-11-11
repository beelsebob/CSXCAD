
set( PUB_HEADERS
  ContinuousStructure.h
  CSPrimitives.h
  CSProperties.h
  CSRectGrid.h
  CSXCAD_Global.h
  CSObject.h
  CSSpatialIndex.h
  ParameterObjects.h
  CSFunctionParser.h
  CSUseful.h
  ParameterCoord.h
  CSTransform.h
  CSBackgroundMaterial.h
  CSPrimPoint.h
  CSPrimBox.h
  CSPrimMultiBox.h
  CSPrimSphere.h
  CSPrimSphericalShell.h
  CSPrimCylinder.h
  CSPrimCylindricalShell.h
  CSPrimPolygon.h
  CSPrimLinPoly.h
  CSPrimRotPoly.h
  CSPrimPolyhedron.h
  CSPrimPolyhedronReader.h
  CSPrimCurve.h
  CSPrimWire.h
  CSPrimUserDefined.h
  CSPropUnknown.h
  CSPropMaterial.h
  CSPropDispersiveMaterial.h
  CSPropLorentzMaterial.h
  CSPropDebyeMaterial.h
  CSPropDiscMaterial.h
  CSPropLumpedElement.h
  CSPropAbsorbingBC.h
  CSPropMetal.h
  CSPropConductingSheet.h
  CSPropExcitation.h
  CSPropProbeBox.h
  CSPropDumpBox.h
  CSPropResBox.h
  CSModeData.h
)

set(SOURCES
  ContinuousStructure.cpp
  CSPrimitives.cpp
  CSProperties.cpp
  CSRectGrid.cpp
  ParameterObjects.cpp
  CSFunctionParser.cpp
  CSUseful.cpp
  ParameterCoord.cpp
  CSTransform.cpp
  CSObject.cpp
  CSSpatialIndex.cpp
  CSPrimPoint.cpp
  CSPrimBox.cpp
  CSPrimMultiBox.cpp
  CSPrimSphere.cpp
  CSPrimSphericalShell.cpp
  CSPrimCylinder.cpp
  CSPrimCylindricalShell.cpp
  CSPrimPolygon.cpp
  CSPrimLinPoly.cpp
  CSPrimRotPoly.cpp
  CSPrimPolyhedron.cpp
  CSPrimPolyhedronReader.cpp
  CSPrimCurve.cpp
  CSPrimWire.cpp
  CSPrimUserDefined.cpp
  CSPropUnknown.cpp
  CSPropMaterial.cpp
  CSPropDispersiveMaterial.cpp
  CSPropLorentzMaterial.cpp
  CSPropDebyeMaterial.cpp
  CSPropDiscMaterial.cpp
  CSPropLumpedElement.cpp
  CSPropAbsorbingBC.cpp
  CSPropMetal.cpp
  CSPropConductingSheet.cpp
  CSPropExcitation.cpp
  CSPropProbeBox.cpp
  CSPropDumpBox.cpp
  CSPropResBox.cpp
  CSBackgroundMaterial.cpp
  CSModeData.cpp
)

# CSXCAD library. Shared by default; a parent project may set CSXCAD_LIBRARY_TYPE to STATIC.
if(NOT DEFINED CSXCAD_LIBRARY_TYPE)
  set(CSXCAD_LIBRARY_TYPE SHARED)
endif()
add_library( CSXCAD ${CSXCAD_LIBRARY_TYPE} ${SOURCES} )
if(CSXCAD_LIBRARY_TYPE STREQUAL "STATIC")
  # No dllexport/dllimport decoration for a static library (see CSXCAD_Global.h).
  target_compile_definitions( CSXCAD PUBLIC CSXCAD_STATIC )
endif()

TARGET_LINK_LIBRARIES( CSXCAD
  ${fparser_LIBRARIES}
  ${TinyXML_LIBRARIES}
  ${HDF5_LIBRARIES}
  ${HDF5_HL_LIBRARIES}
  ${CSXCAD_CGAL_LIBRARIES}
  ${Boost_LIBRARIES}
  ${vtk_LIBS}
)

set_target_properties(CSXCAD PROPERTIES VERSION ${LIB_VERSION_STRING}
                                          SOVERSION ${LIB_VERSION_MAJOR})

if (WIN32)
    INSTALL(TARGETS CSXCAD RUNTIME DESTINATION bin ARCHIVE DESTINATION lib${LIB_SUFFIX})
else()
    INSTALL(TARGETS CSXCAD DESTINATION lib${LIB_SUFFIX})
endif()

INSTALL(FILES ${PUB_HEADERS} DESTINATION include/CSXCAD)


