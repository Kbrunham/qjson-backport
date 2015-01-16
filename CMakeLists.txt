cmake_minimum_required (VERSION 2.6)

project (qjson)

# The version number.
set (qjson_VERSION_MAJOR 1)
set (qjson_VERSION_MINOR 0)

#Find the required libs
find_package(GTest REQUIRED)
find_package(Qt4 REQUIRED QtCore QtXml)
include(${QT_USE_FILE})

# Add the lib
add_library(qjson-backport SHARED
	qjson.cpp
	qjsonarray.cpp
	qjsondocument.cpp
	qjsonobject.cpp
	qjsonparser.cpp
	qjsonvalue.cpp
	qjsonwriter.cpp
	)

# Add the executable target 
add_executable(qjson_backport_test
    main.cpp
)

include_directories(
	${PROJECT_SOURCE_DIR}
	${GTEST_INCLUDE_DIRS}
	${QT_QTCORE_INCLUDE_DIR}
	${QT_HEADERS_DIR}
)

target_link_libraries(qjson-backport
	${QT_LIBRARIES}
)

target_link_libraries(qjson_backport_test
	qjson-backport
	${GTEST_LIBRARIES}
)


add_custom_target(check qjson_backport_test)
