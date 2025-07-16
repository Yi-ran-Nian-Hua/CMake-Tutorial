**`add_custom_command()`**
- 作用： 在构建阶段，执行定制的构建指令
- 参数列表：
```cmake
add_custom_command(OUTPUT output1 [output2 ...]
                   COMMAND command1 [ARGS] [args1...]
                   [COMMAND command2 [ARGS] [args2...] ...]
                   [MAIN_DEPENDENCY depend]
                   [DEPENDS [depends...]]
                   [BYPRODUCTS [files...]]
                   [IMPLICIT_DEPENDS <lang1> depend1
                                    [<lang2> depend2] ...]
                   [WORKING_DIRECTORY dir]
                   [COMMENT comment]
                   [DEPFILE depfile]
                   [JOB_POOL job_pool]
                   [JOB_SERVER_AWARE <bool>]
                   [VERBATIM] [APPEND] [USES_TERMINAL]
                   [CODEGEN]
                   [COMMAND_EXPAND_LISTS]
                   [DEPENDS_EXPLICIT_ONLY])
```
  - `OUTPUT`: 生成的文件名称
  - `COMMAND`: 在构建的时候，如何生成该文件的指令
  - `DEPENDS`: 构建该文件的依赖库