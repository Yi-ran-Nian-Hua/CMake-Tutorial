# Step4: 生成器表达式(Generator Expressions)
## 1. `CMake`构建过程的基本流程
`CMake`在构建的时候主要分为三个基本步骤: 配置阶段(Configuration), 生成阶段(Generation)和构建阶段(Build)
### 1.1 配置阶段
配置阶段`CMake`会读取`CMakeLists.txt`的内容, 并且执行其中的命令, 这些命令只要用于检查系统环境, 设置构建选项以及定义构建目标.
### 1.2 生成阶段
在这个阶段, `CMake`会根据配置阶段的结果, 生成实际的**构建文件**的过程, 构建文件就比如说`Visual Studio`下的`.sln`工程, `GNU Make`下面的`Makefile`等等.
这里我们需要知道, ** `CMake`并不会执行构建, 他只能帮助生成构建文件**.
为什么说`CMake`是与平台无关(跨平台)的呢, 正是因为这个过程是与平台无关的, 所以就叫他是一个跨平台的生成工具.
`CMake`可以生成哪些构建文件呢? 构建文件与对应的构建平台有关, 我们可以运行下面这一条指令查看:
```shell
cmake --help 
```
其中有一个部分叫做`Generators`, 比如在我的 Mac 下, 它列出的支持的构建系统有下面这些:
```bash
Generators

The following generators are available on this platform (* marks default):
* Unix Makefiles               = Generates standard UNIX makefiles.
  Ninja                        = Generates build.ninja files.
  Ninja Multi-Config           = Generates build-<Config>.ninja files.
  Watcom WMake                 = Generates Watcom WMake makefiles.
  Xcode                        = Generate Xcode project files.
  CodeBlocks - Ninja           = Generates CodeBlocks project files
                                 (deprecated).
  CodeBlocks - Unix Makefiles  = Generates CodeBlocks project files
                                 (deprecated).
  CodeLite - Ninja             = Generates CodeLite project files
                                 (deprecated).
  CodeLite - Unix Makefiles    = Generates CodeLite project files
                                 (deprecated).
  Eclipse CDT4 - Ninja         = Generates Eclipse CDT 4.0 project files
                                 (deprecated).
  Eclipse CDT4 - Unix Makefiles= Generates Eclipse CDT 4.0 project files
                                 (deprecated).
  Kate - Ninja                 = Generates Kate project files (deprecated).
  Kate - Ninja Multi-Config    = Generates Kate project files (deprecated).
  Kate - Unix Makefiles        = Generates Kate project files (deprecated).
  Sublime Text 2 - Ninja       = Generates Sublime Text 2 project files
                                 (deprecated).
  Sublime Text 2 - Unix Makefiles
                               = Generates Sublime Text 2 project files
                                 (deprecated).

```
标有**`*`**的表示现在使用的生成的构建文件, 即生成的是`GNU Make(Makefile)`
如果在 Windows 下执行, 就会看到下面这个结果:
```bash
Generators

The following generators are available on this platform (* marks default):
* Visual Studio 17 2022        = Generates Visual Studio 2022 project files.
                                 Use -A option to specify architecture.
  Visual Studio 16 2019        = Generates Visual Studio 2019 project files.
                                 Use -A option to specify architecture.
  Visual Studio 15 2017 [arch] = Generates Visual Studio 2017 project files.
                                 Optional [arch] can be "Win64" or "ARM".
  Visual Studio 14 2015 [arch] = Generates Visual Studio 2015 project files.
                                 Optional [arch] can be "Win64" or "ARM".
  Borland Makefiles            = Generates Borland makefiles.
  NMake Makefiles              = Generates NMake makefiles.
  NMake Makefiles JOM          = Generates JOM makefiles.
  MSYS Makefiles               = Generates MSYS makefiles.
  MinGW Makefiles              = Generates a make file for use with
                                 mingw32-make.
  Green Hills MULTI            = Generates Green Hills MULTI files
                                 (experimental, work-in-progress).
  Unix Makefiles               = Generates standard UNIX makefiles.
  Ninja                        = Generates build.ninja files.
  Ninja Multi-Config           = Generates build-<Config>.ninja files.
  Watcom WMake                 = Generates Watcom WMake makefiles.
  CodeBlocks - MinGW Makefiles = Generates CodeBlocks project files
                                 (deprecated).
  CodeBlocks - NMake Makefiles = Generates CodeBlocks project files
                                 (deprecated).
  CodeBlocks - NMake Makefiles JOM
                               = Generates CodeBlocks project files
                                 (deprecated).
  CodeBlocks - Ninja           = Generates CodeBlocks project files
                                 (deprecated).
  CodeBlocks - Unix Makefiles  = Generates CodeBlocks project files
                                 (deprecated).
  CodeLite - MinGW Makefiles   = Generates CodeLite project files
                                 (deprecated).
  CodeLite - NMake Makefiles   = Generates CodeLite project files
                                 (deprecated).
  CodeLite - Ninja             = Generates CodeLite project files
                                 (deprecated).
  CodeLite - Unix Makefiles    = Generates CodeLite project files
                                 (deprecated).
  Eclipse CDT4 - NMake Makefiles
                               = Generates Eclipse CDT 4.0 project files
                                 (deprecated).
  Eclipse CDT4 - MinGW Makefiles
                               = Generates Eclipse CDT 4.0 project files
                                 (deprecated).
  Eclipse CDT4 - Ninja         = Generates Eclipse CDT 4.0 project files
                                 (deprecated).
  Eclipse CDT4 - Unix Makefiles= Generates Eclipse CDT 4.0 project files
                                 (deprecated).
  Kate - MinGW Makefiles       = Generates Kate project files (deprecated).
  Kate - NMake Makefiles       = Generates Kate project files (deprecated).
  Kate - Ninja                 = Generates Kate project files (deprecated).
  Kate - Ninja Multi-Config    = Generates Kate project files (deprecated).
  Kate - Unix Makefiles        = Generates Kate project files (deprecated).
  Sublime Text 2 - MinGW Makefiles
                               = Generates Sublime Text 2 project files
                                 (deprecated).
  Sublime Text 2 - NMake Makefiles
                               = Generates Sublime Text 2 project files
                                 (deprecated).
  Sublime Text 2 - Ninja       = Generates Sublime Text 2 project files
                                 (deprecated).
  Sublime Text 2 - Unix Makefiles
                               = Generates Sublime Text 2 project files
                                 (deprecated).
```
比 Mac 下多一些, 主要多了`MSVC(Visual Studio)`的生成文件.
我们也可以使用`-G`指定`CMake`生成对应平台的构建文件.
## 1.3 构建阶段
这一阶段就是产生真正的二进制文件(库或者可执行文件)的过程, 会根据第二阶段生成的构建文件, 前往对应的构建平台, 进行编译与链接, 生成最终产物.
`CMake`推荐使用"Out-of-source"构建方式, 即将构建文件放在源代码之外的独立目录中, 如下图所示:
![out-of-source 示例](https://i-blog.csdnimg.cn/direct/9b07e1cf22654a50b6d8c5476db92a17.png)
## 2. 生成器表达式
介绍完了`CMake`构建的基本流程, 接下来就可以介绍生成器表达式了
与普通的变量不同, 生成器表达式作用在`CMake`的生成阶段而非配置阶段, 因为它是基于生成阶段来动态决定结果, 因此结果不唯一.
也正是因为这个特性, 采用普通的比如`message()`方式来查看生成器表达式的值就会失效:
```cmake
set(test_val 0)
message("test_val = ${test_val}")
message("$<${test_val}:hello>")
```
这里使用了`$<condition:true_string>`这个生成器表达式，该表达式的模式是：如果`condition`为真，就会那么后面的`true_string`就会起作用，否则就为空。
使用`cmake`进行生成，就会发现这样的输出：
```cmake
test_val = 0
$<0:hello>
```
正常情况来说，如果`test_val`为`0`, 那么后面的值就应该为空，但是这里原封不动的输出了出来。
关于更多的生成器表达式的介绍，可以参考：https://cmake.org/cmake/help/latest/manual/cmake-generator-expressions.7.html#manual:cmake-generator-expressions(7)
本节主要介绍两个生成器表达式

### **`$<condition:true_string>`**
- 如果`condition`的值为 1，那么表达式的结果就为`true_string`
- 如果表达式的结果为 0，那么表达式结果为空
这个生成器表达式的结果很像三目运算符

### **`<COMPILE_LANG_AND_ID: language, compilerlist>`**
- 如果当前所用的编程语言与`language`一致，并且编译器 ID 在`compiler_ids`的列表中，则表达式的值为 1，否则为 0
- `language`的值主要为`CXX`和`C`
- `compiler_ids`主要有`GNU, Clang, MSVC`等，有多个时用逗号隔开