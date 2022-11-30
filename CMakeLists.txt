project(CFE_HW_APP C)

include_directories(fsw/mission_inc)
include_directories(fsw/platform_inc)

# Create the app module
add_cfe_app(hw_app fsw/src/hw_app.c)

# Include the public API from sample_lib to demonstrate how
# to call library-provided functions
add_cfe_app_dependency(hw_app sample_lib)

# Add table
add_cfe_tables(hwAppTable fsw/tables/hw_app_tbl.c)

# If UT is enabled, then add the tests from the subdirectory
# Note that this is an app, and therefore does not provide
# stub functions, as other entities would not typically make 
# direct function calls into this application.
if (ENABLE_UNIT_TESTS)
  add_subdirectory(unit-test)
endif (ENABLE_UNIT_TESTS)

include_directories(fsw/src)
aux_source_directory(fsw/tables APP_TABLE_FILES)
add_cfe_tables(hw_app ${APP_TABLE_FILES})