if(NOT TARGET Boost::unit_test_framework)
    find_package(Boost 1.64 REQUIRED COMPONENTS unit_test_framework)
endif()

add_library(testHelpers STATIC
    rttr/test/BaseFixture.cpp
    rttr/test/BaseFixture.hpp
    rttr/test/BufferedWriter.hpp
    rttr/test/Fixture.cpp
    rttr/test/Fixture.hpp
    rttr/test/LocaleResetter.hpp
    rttr/test/LogAccessor.hpp
    rttr/test/MockClock.hpp
    rttr/test/random.cpp
    rttr/test/random.hpp
    rttr/test/stubFunction.hpp
    rttr/test/testHelpers.hpp
    rttr/test/TmpFolder.hpp
)
target_link_libraries(testHelpers PRIVATE s25Common rttrConfig Boost::unit_test_framework)
target_include_directories(testHelpers PUBLIC .)
# Heuristically guess if we are compiling against dynamic boost
if(NOT Boost_USE_STATIC_LIBS AND NOT Boost_UNIT_TEST_FRAMEWORK_LIBRARY MATCHES "\\${CMAKE_STATIC_LIBRARY_SUFFIX}\$")
    target_compile_definitions(testHelpers PRIVATE BOOST_TEST_DYN_LINK)
endif()
