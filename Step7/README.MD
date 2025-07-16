# Step7: 测试支持
# 背景
一些情况下，在构建整个工程的过程中，需要根据用户不同的系统习惯来进行个性化的构建，这个时候就需要`CMake`进行手动测试

### **`check_cxx_source_compiles()`**
- 它的作用就是允许在生成阶段的时候测试里面的代码是否能够成功运行
- 参数列表：`check_cxx_source_compiles(<code> <variable> [FAIL_REGEX <regexes>...])`
  - `<code>`: 要测试的代码，使用`""`进行包裹
  - `<variable>`: 一个布尔值，如果前面的程序能够成功运行，那么该值就会赋值为`true`, 否则就为`false`