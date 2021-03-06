add_subdirectory(App)
add_subdirectory(libarea)

if(BUILD_GUI)
    add_subdirectory(Gui)
endif(BUILD_GUI)

INSTALL(
    FILES
        Init.py
        InitGui.py
        PathCommands.py
        TestPathApp.py

    DESTINATION
        Mod/Path
)

SET(PathScripts_SRCS
    PathCommands.py
    PathScripts/PathArray.py
    PathScripts/PathComment.py
    PathScripts/PathCompoundExtended.py
    PathScripts/PathContour.py
    PathScripts/PathCopy.py
    PathScripts/PathCustom.py
    PathScripts/PathDressup.py
    PathScripts/PathDressupDogbone.py
    PathScripts/PathDressupDragknife.py
    PathScripts/PathDressupHoldingTags.py
    PathScripts/PathDressupRampEntry.py
    PathScripts/PathDrilling.py
    PathScripts/PathEngrave.py
    PathScripts/PathFacePocket.py
    PathScripts/PathFaceProfile.py
    PathScripts/PathFixture.py
    PathScripts/PathFromShape.py
    PathScripts/PathGeom.py
    PathScripts/PathHelix.py
    PathScripts/PathHop.py
    PathScripts/PathInspect.py
    PathScripts/PathJob.py
    PathScripts/PathLog.py
    PathScripts/PathMillFace.py
    PathScripts/PathPlane.py
    PathScripts/PathPocket.py
    PathScripts/PathPost.py
    PathScripts/PathPostProcessor.py
    PathScripts/PathPreferences.py
    PathScripts/PathPreferencesPathDressup.py
    PathScripts/PathPreferencesPathJob.py
    PathScripts/PathProfile.py
    PathScripts/PathProfileEdges.py
    PathScripts/PathSanity.py
    PathScripts/PathSelection.py
    PathScripts/PathSimpleCopy.py
    PathScripts/PathStock.py
    PathScripts/PathStop.py
    PathScripts/PathSurface.py
    PathScripts/PathToolController.py
    PathScripts/PathToolLenOffset.py
    PathScripts/PathToolLibraryManager.py
    PathScripts/PathUtil.py
    PathScripts/PathUtils.py
    PathScripts/PostUtils.py
    PathScripts/__init__.py
    PathScripts/kdtree.py
)

SET(PathScripts_post_SRCS
    PathScripts/post/__init__.py
    PathScripts/post/centroid_post.py
    PathScripts/post/comparams_post.py
    PathScripts/post/dumper_post.py
    PathScripts/post/dynapath_post.py
    PathScripts/post/example_post.py
    PathScripts/post/example_pre.py
    PathScripts/post/grbl_post.py
    PathScripts/post/linuxcnc_post.py
    PathScripts/post/opensbp_post.py
    PathScripts/post/opensbp_pre.py
    PathScripts/post/phillips_post.py
    PathScripts/post/rml_post.py
    PathScripts/post/slic3r_pre.py
    PathScripts/post/smoothie_post.py
)


SET(PathTests_SRCS
    PathTests/__init__.py
    PathTests/boxtest.fcstd
    PathTests/PathTestUtils.py
    PathTests/test_centroid_00.ngc
    PathTests/test_linuxcnc_00.ngc
    PathTests/TestPathCore.py
    PathTests/TestPathDepthParams.py
    PathTests/TestPathDressupHoldingTags.py
    PathTests/TestPathGeom.py
    PathTests/TestPathLog.py
    PathTests/TestPathPost.py
    PathTests/TestPathUtil.py
)

SET(all_files
    ${PathScripts_SRCS}
    ${PathScripts_post_SRCS}
)

ADD_CUSTOM_TARGET(PathScripts ALL
    SOURCES ${all_files}
)

SET(test_files
  TestPathApp.py
  ${PathTests_SRCS}
)

ADD_CUSTOM_TARGET(PathTests ALL
    SOURCES ${test_files}
)

fc_copy_sources(PathScripts "${CMAKE_BINARY_DIR}/Mod/Path" ${all_files})
fc_copy_sources(PathTests "${CMAKE_BINARY_DIR}/Mod/Path" ${test_files})

INSTALL(
    FILES
        ${PathScripts_SRCS}
    DESTINATION
        Mod/Path/PathScripts
)

INSTALL(
    FILES
        ${PathTests_SRCS}
    DESTINATION
        Mod/Path/PathTests
)

INSTALL(
    FILES
        ${PathScripts_post_SRCS}
    DESTINATION
        Mod/Path/PathScripts/post
)
