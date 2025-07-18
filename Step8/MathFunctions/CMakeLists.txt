# 包含 MakeTable.cmake
include(MakeTable.cmake)
add_library(MathFunctions MathFunctions.cxx)

# should we use our own math functions
option(USE_MYMATH "Use tutorial provided math implementation" ON)

if(USE_MYMATH)
  target_compile_definitions(MathFunctions PRIVATE "USE_MYMATH")

  # library that just does sqrt
  add_library(SqrtLibrary STATIC
    mysqrt.cxx
    ${CMAKE_CURRENT_BINARY_DIR}/Table.h
  )
  target_include_directories(SqrtLibrary PRIVATE ${CMAKE_CURRENT_BINARY_DIR})

  # link SqrtLibrary to tutorial_compiler_flags
  target_link_libraries(SqrtLibrary PUBLIC tutorial_compiler_flags)

  # does this system provide the log and exp functions?
  # add compile definitions
  target_link_libraries(MathFunctions PRIVATE SqrtLibrary)
endif()

# state that anybody linking to us needs to include the current source dir
# to find MathFunctions.h, while we don't.
target_include_directories(MathFunctions
  INTERFACE ${CMAKE_CURRENT_SOURCE_DIR}
)

# link MathFunctions to tutorial_compiler_flags
target_link_libraries(MathFunctions PUBLIC tutorial_compiler_flags)

# install libs
set(installable_libs MathFunctions tutorial_compiler_flags)

if(TARGET SqrtLibrary)
  list(APPEND installable_libs SqrtLibrary)
endif()

install(TARGETS ${installable_libs} DESTINATION lib)

# install include headers
install(FILES MathFunctions.h DESTINATION include)
