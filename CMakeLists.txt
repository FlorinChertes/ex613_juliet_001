# set minimum cmake version
cmake_minimum_required(VERSION 3.5 FATAL_ERROR)

# project name and language
project (ex613_juliet_001_prj  LANGUAGES CXX)

# require C++20
set(CMAKE_CXX_STANDARD 20)
set(CMAKE_CXX_EXTENSIONS OFF)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

set(SHARED_DIR "testcases/shared/108")
set(SHARED_FILES 
	${SHARED_DIR}/io.cxx
	${SHARED_DIR}/std_testcase.h
	${SHARED_DIR}/std_testcase_io.h
	${SHARED_DIR}/std_thread.h
	${SHARED_DIR}/std_thread.cxx	
	)

IF (MSVC)
	# Activate C++ exception handling 
	IF (NOT CMAKE_CXX_FLAGS MATCHES "/EHsc") 
		SET(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} /EHsc")
	ENDIF ()
ELSE ()
	SET( CMAKE_CXX_FLAGS  "${CMAKE_CXX_FLAGS} -O3 -flto -Wall -Wextra -Wnull-dereference -Wsuggest-attribute=const")

	SET(GCC_STD_CPP_CONCEPTS_COMPILE_FLAGS "-fconcepts")
	SET( CMAKE_CXX_FLAGS  "${CMAKE_CXX_FLAGS} ${GCC_STD_CPP_CONCEPTS_COMPILE_FLAGS}")

	SET(GCC_STD_CPP_PERMISIV_COMPILE_FLAGS "-fpermissive")
	SET( CMAKE_CXX_FLAGS  "${CMAKE_CXX_FLAGS} ${GCC_STD_CPP_PERMISIV_COMPILE_FLAGS}")
ENDIF () 


# add the executable
add_library(ex613_juliet_001_app

	${SHARED_FILES}
	testcases/000/248/302/CWE78_OS_Command_Injection__wchar_t_listen_socket_execlp_04.cxx

	testcases/000/248/721/CWE78_OS_Command_Injection__wchar_t_listen_socket_w32_spawnvp_83.h
	testcases/000/248/721/CWE78_OS_Command_Injection__wchar_t_listen_socket_w32_spawnvp_83_bad.cpp
	testcases/000/248/721/CWE78_OS_Command_Injection__wchar_t_listen_socket_w32_spawnvp_83_goodG2B.cpp
	testcases/000/248/721/CWE78_OS_Command_Injection__wchar_t_listen_socket_w32_spawnvp_83a.cpp
)

target_include_directories(ex613_juliet_001_app PRIVATE ${SHARED_DIR})