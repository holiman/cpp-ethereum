aux_source_directory(. SRC_LIST)

file(GLOB HEADERS "*.h")

add_library(devcrypto ${SRC_LIST} ${HEADERS})
add_definitions(-D_GLIBCXX_USE_CXX11_ABI=1)

find_package(Dev)
find_package(Utils)

target_include_directories(devcrypto PRIVATE ..)
target_include_directories(devcrypto PRIVATE ../utils)
# Place cryptopp first not to accidently include headers from system level installation of Crypto++
target_link_libraries(devcrypto
		PRIVATE cryptopp ${Utils_SECP256K1_LIBRARIES} ${Utils_SCRYPT_LIBRARIES}
		PUBLIC ${Dev_DEVCORE_LIBRARIES})

install(TARGETS devcrypto RUNTIME DESTINATION bin ARCHIVE DESTINATION lib LIBRARY DESTINATION lib)
