add_library(MathFunctions MathFunctions.cxx)

# TODO 1: State that anybody linking to MathFunctions needs to include the
# current source directory, while MathFunctions itself doesn't.
# Hint: Use target_include_directories with the INTERFACE keyword
# 库内自检包含的头文件, 由于库本身并不需要, 因为在相同的文件夹, 但是其他依赖该库的需要, 因此需要设置成 INTERFACE
target_include_directories(MathFunctions INTERFACE "${CMAKE_CURRENT_SOURCE_DIR}")
# should we use our own math functions
option(USE_MYMATH "Use tutorial provided math implementation" ON)
if (USE_MYMATH)
  target_compile_definitions(MathFunctions PRIVATE "USE_MYMATH")

  # library that just does sqrt
  add_library(SqrtLibrary STATIC
              mysqrt.cxx
              )

  # TODO 6: Link SqrtLibrary to tutorial_compiler_flags

  target_link_libraries(SqrtLibrary PUBLIC tutorial_compiler_flags)

endif()

# TODO 7: Link MathFunctions to tutorial_compiler_flag
target_link_libraries(MathFunctions PUBLIC tutorial_compiler_flags SqrtLibrary)