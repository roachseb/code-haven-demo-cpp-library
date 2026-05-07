# Try Conan-provided GTest first, otherwise fetch from GitHub
find_package(GTest QUIET)
if(NOT GTest_FOUND)
    include(FetchContent)
    FetchContent_Declare(
        googletest
        GIT_REPOSITORY https://github.com/google/googletest.git
        GIT_TAG v1.14.0
    )
    # Prevent GoogleTest from overriding parent project compiler/linker settings
    set(gtest_force_shared_crt ON CACHE BOOL "" FORCE)
    FetchContent_MakeAvailable(googletest)
endif()

add_executable(test_math_utils test_math_utils.cpp)

target_link_libraries(test_math_utils
    PRIVATE
        math-utils
        GTest::gtest_main
)

include(GoogleTest)
gtest_discover_tests(test_math_utils)
