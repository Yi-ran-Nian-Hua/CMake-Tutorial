# Step5: 安装与测试

# 一. 什么是`install()`?

`install()`是`CMake`提供的命令, 用于告诉`CMake`在构建完成之后, 如何将生成的程序/库/头文件等内容复制到目标系统的标准目录结构中(如`/usr/local/bin`, `/usr/include`, `/usr/lib`等等)

## 1.1`install()`与`build`直接生成有什么区别呢?

- 目的上:

  - `build`是用于编译二进制代码, 生成二进制文件和库
  - `install`会将`build`的产物部署到指定的位置
- 输出路径上:

  - `build`: 通常在`build/`下
  - `install`: 通常安装到指定的路径
- 是否生成安装包支持?

  - `build`: 不支持
  - `install`: 支持使用`CPack`进行打包

## 1.2 `install()`适用于哪些场景?

- 部署到生产环境中(不想每次都依赖`build`目录)
- 系统路径的运行程序
- 打包应用
- 安装 SDK

## 1.3 `install()`基本语法

提醒: 记得先`build`之后再`install`!!!

```cmake
install(TARGETS <target>... [...])
install(IMPORTED_RUNTIME_ARTIFACTS <target>... [...])
install({FILES | PROGRAMS} <file>... [...])
install(DIRECTORY <dir>... [...])
install(SCRIPT <file> [...])
install(CODE <code> [...])
install(EXPORT <export-name> [...])
install(PACKAGE_INFO <package-name> [...])
install(RUNTIME_DEPENDENCY_SET <set-name> [...])
```

这里主要记住两种, 如果使用`TARGET`, 则后面的`<target>`只需要填写目标名即可, 但如果使用`FILES`, 那么就要把文件名写全

# 二. 测试

可以在`CMake`中编写一些测试指令来执行测试

首先需要允许开启测试:

```cmake
enable_testing()
```

如果要添加一个测试, 可以使用:

```cmake
add_test(NAME <name> COMMAND <command> [<arg>...]
         [CONFIGURATIONS <config>...]
         [WORKING_DIRECTORY <dir>]
         [COMMAND_EXPAND_LISTS])
```

在一些情况下, 如果输出的结果比较复杂, 可以使用

```cmake
set_tests_properties(<tests>...
                     [DIRECTORY <dir>]
                     PROPERTIES <prop1> <value1>
                     [<prop2> <value2>]...)
```

来使得测试的结果能够准确.
