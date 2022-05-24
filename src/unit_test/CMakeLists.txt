#set(BOOST_UT_DISABLE_MODULE ON CACHE BOOL "FORCE OLD MODE" FORCE)
find_package(ut REQUIRED)
find_package(Threads)
add_executable(${PROJECT_NAME}_OPENGL_UNIT_TEST
        unit_test.cpp
        )
target_link_libraries(${PROJECT_NAME}_OPENGL_UNIT_TEST
        PUBLIC project_options
        PUBLIC project_warnings
        PRIVATE Threads::Threads
        PRIVATE boost::ut
        )
target_include_directories(${PROJECT_NAME}_OPENGL_UNIT_TEST
        PRIVATE ${CMAKE_CURRENT_SOURCE_DIR}
        )


#add_custom_command(TARGET ${PROJECT_NAME}_OPENGL_UNIT_TEST POST_BUILD
#        COMMAND ${CMAKE_COMMAND} -E echo
#        "Copying ${CMAKE_CURRENT_SOURCE_DIR}/res to $<TARGET_FILE_DIR:${PROJECT_NAME}_OPENGL>/res")
#add_custom_command(TARGET ${PROJECT_NAME}_OPENGL_UNIT_TEST POST_BUILD
#        COMMAND ${CMAKE_COMMAND} -E copy_directory
#        ${CMAKE_CURRENT_SOURCE_DIR}/res $<TARGET_FILE_DIR:${PROJECT_NAME}_OPENGL>/res)

if (MSVC)
    target_compile_definitions(${PROJECT_NAME}_OPENGL_UNIT_TEST
            PUBLIC _CRT_SECURE_NO_WARNINGS) # required by libpng
    target_link_options(${PROJECT_NAME}_OPENGL_UNIT_TEST PRIVATE "/PROFILE")
endif ()

#target_compile_definitions(${PROJECT_NAME}_OPENGL_UNIT_TEST PRIVATE BOOST_UT_DISABLE_MODULE)

#target_precompile_headers(${PROJECT_NAME}_OPENGL_UNIT_TEST
#        )