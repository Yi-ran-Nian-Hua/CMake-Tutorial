# Tutorial3: 为库添加限制需求
## 接口库
接口库不是一个实际的库,它是一种特殊类型的库, 主要用来组织和传播编译选项/包含路径/宏定义等编译属性, 它本身不编译任何源代码, 也不会生成任何库的文件, 可以理解为是一种"逻辑库"

**`target_compile_features()`**
- 作用: 为项目构建的时候添加其他的编译选项