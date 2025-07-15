# Step 1: 基本点
## 1.1 需要掌握的`CMake`指令
**`add_executable()`**
- 作用: 使用特定的源文件来生成项目的可执行文件
- 参数列表: `add_executable(<name> <options>... <sources>...)`

**`cmake_minimum_required()`**
- 作用: 指定项目所需的最低 CMake 版本
- 参数列表: `cmake_minimum_required(VERSION <min>[...<policy_max>] [FATAL_ERROR])`

**`project()`**
- 作用: 设置项目名称, 也可以在这里设置项目的版本
- 参数列表:
  - `project(<PROJECT-NAME> [<language-name>...])`
  - `project(<PROJECT-NAME>
        [VERSION <major>[.<minor>[.<patch>[.<tweak>]]]]
        [COMPAT_VERSION <major>[.<minor>[.<patch>[.<tweak>]]]]
        [DESCRIPTION <project-description-string>]
        [HOMEPAGE_URL <url-string>]
        [LANGUAGES <language-name>...])`
- 注意: 在设置了之后, `PROJECT_NAME`以及`CMAKE_PROJECT_NAME`就有了定义, 同时, 这个指令所在的`CMakeLists.txt`也就成了**顶层`CMakeLists.txt`**.

**`CMAKE_CXX_STANDARD`**
- 注意: 这是一个变量, 需要使用`set()`指令进行设置
- 作用: 设置构建目标的时候默认使用的 C++标准

**`CMAKE_CXX_STANDARD_REQUIRED`**
- 注意: 这是一个变量, 需要使用`set()`指令进行设置
- 作用: 如果这个值设置为`True`或者`On`, 那么在构建的时候, 就一定要按照`CMAKE_CXX_STANDARD`设置的 C++标准进行构建, 否则就会报错

**`set()`**
- 作用: 类似于赋值语句, 给变量等赋值
- 参数列表: `set(<variable> <value>... [PARENT_SCOPE])`
  - 如果给定了至少一个`<value>`, 那么这个`<variable>`的值就会被设置为`<value>`的值, 如果没有指定, 那就取消赋值, 等价于`unset(<variable>)`
  
**<PROJECT-NAME>_VERSION_MAJOR**
当`project()`后面设置了`VERSION`关键字后, 就会获取`major`部分的值

**<PROJECT-NAME>_VERSION_MINOR**
当`project()`后面设置了`VERSION`关键字后, 就会获取`minor`部分的值
**configure_file()**
- 作用: 可以将另外一个文件的内容, 经过内容修改之后, 复制到本项目中来
- 参数列表: `configure_file(<input> <output>
               [NO_SOURCE_PERMISSIONS | USE_SOURCE_PERMISSIONS |
                FILE_PERMISSIONS <permissions>...]
               [COPYONLY] [ESCAPE_QUOTES] [@ONLY]
               [NEWLINE_STYLE [UNIX|DOS|WIN32|LF|CRLF]])`
- 注意: 有向替换的值, 请使用`@CMAKE_VARIABLE@`, 到时候就可以将文件里面的值替换为`CMakeLists.txt`所对应的值.
**target_include_directories()**
- 作用: 当项目构建的时候, 将指定路径下的文件目录包含在构建的最终项目中
- 参数列表:`target_include_directories(<target> [SYSTEM] [AFTER|BEFORE]
  <INTERFACE|PUBLIC|PRIVATE> [items1...]
  [<INTERFACE|PUBLIC|PRIVATE> [items2...] ...])`
- TODO: 这里`INTERFACE/PUBLIC/PRIVATE`的作用后续补充