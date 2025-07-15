# Step2: 添加一个库
## 主要目标: 学会构建如何导入与制作第三方库
**`add_library()`**
- 作用: 将特定部分的源文件打包成一个库
- 参数列表: `add_library(<name> [<type>] [EXCLUDE_FROM_ALL] <sources>...)`
  - `<name>`: 构建库的名字
  - `<type>`: 构建库的类型, `STATIC`表示构建静态库, `SHARED`表示构建动态库, `MODULE`: ???, 如果`<type>`没有指定, 那么究竟是构建动态库还是构建静态库则会依据`BUILD_SHARED_LIBS`决定
  
**`add_subdirectory()`**
- 作用: 在构建的时候添加一个库
- 参数列表: `add_subdirectory(source_dir [binary_dir] [EXCLUDE_FROM_ALL] [SYSTEM])`
  - `source_dir`: 库的`CMakeLists.txt`所在的路径, 如果填写的是一个相对路径, 那么位置就是相对于当前路径下的位置, 也可以填写绝对路径
  - `binary_dir`: 指定该子项目的构建输出目录


**`target_link_libraries()`**
- 作用: 将第三方库链接到目标项目下
- 参数列表: `target_link_libraries(<target> ... <item>... ...)`
  - `target`: 最终链接的目标, 需要为`add_executable()`, `add_library()`指定的目标
  - `item`: 可以是一个库的名字, 也可以是库的文件全路径, 也可以是...(TODO: 看官方文档)

**`PROJECT_SOURCE_DIR`**
- 这是一个变量, 表明源代码所在的路径地址, 即调用`project()`那个`CMakeLists.txt`所在的路径地址(顶层项目的源代码目录)

**`if()`**

if 语句

**`option()`**
- 作用: 提供一个二元的选项, 如果不指定具体的值, 默认为 OFF
- 参数列表: `option(<variable> "<help_text>" [value])`
  - `<vriable>`: 二元选项变量名
  - `<help_text>`: 对该变量的解释信息
  - `[value]`: 默认值, 如果不指定就为 `OFF`

**`target_compile_definitions()`**
- 作用: 为特定的目标添加编译宏定义, 可以控制代码编译时候的条件啊
- 参数列表: `target_compile_definitions(<target>
  <INTERFACE|PUBLIC|PRIVATE> [items1...]
  [<INTERFACE|PUBLIC|PRIVATE> [items2...] ...])`
  - `items...`: 表示的编译宏定义, 请注意, 编译宏定义的名字中如果会有"`-D`", 则这两个字母会被移除掉.