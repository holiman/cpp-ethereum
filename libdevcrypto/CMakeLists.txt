aux_source_directory(. SRC_LIST)

file(GLOB HEADERS "*.h")

get_property(dirs DIRECTORY ${CMAKE_CURRENT_SOURCE_DIR} PROPERTY INCLUDE_DIRECTORIES)
foreach(dir ${dirs})
	message(STATUS "dir='${dir}'")
endforeach()

include_directories(SYSTEM BEFORE ${CRYPTOPP_INCLUDE_DIR})
add_library(devcrypto ${SRC_LIST} ${HEADERS})

get_property(dirs TARGET devcrypto PROPERTY INCLUDE_DIRECTORIES)
foreach(dir ${dirs})
	message(STATUS "dir1='${dir}'")
endforeach()

get_property(dirs TARGET devcrypto PROPERTY INTERFACE_SYSTEM_INCLUDE_DIRECTORIES)
foreach(dir ${dirs})
	message(STATUS "dirS='${dir}'")
endforeach()

get_property(dirs TARGET devcrypto PROPERTY INTERFACE_INCLUDE_DIRECTORIES)
foreach(dir ${dirs})
	message(STATUS "dirI='${dir}'")
endforeach()

add_definitions(-D_GLIBCXX_USE_CXX11_ABI=1)

find_package(Dev)
find_package(Utils)

target_include_directories(devcrypto PRIVATE .. ../utils)
target_link_libraries(devcrypto cryptopp ${Utils_SECP256K1_LIBRARIES} ${Utils_SCRYPT_LIBRARIES} devcore)

get_property(dirs TARGET devcrypto PROPERTY INCLUDE_DIRECTORIES)
foreach(dir ${dirs})
	message(STATUS "Dir1='${dir}'")
endforeach()

get_property(dirs TARGET devcore PROPERTY INCLUDE_DIRECTORIES)
foreach(dir ${dirs})
	message(STATUS "devcore='${dir}'")
endforeach()

get_property(dirs TARGET devcrypto PROPERTY INTERFACE_SYSTEM_INCLUDE_DIRECTORIES)
foreach(dir ${dirs})
	message(STATUS "DirS='${dir}'")
endforeach()

get_property(dirs TARGET devcrypto PROPERTY INTERFACE_INCLUDE_DIRECTORIES)
foreach(dir ${dirs})
	message(STATUS "DirI='${dir}'")
endforeach()

install(TARGETS devcrypto RUNTIME DESTINATION bin ARCHIVE DESTINATION lib LIBRARY DESTINATION lib)
