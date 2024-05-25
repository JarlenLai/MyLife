# 2024
## 0524
### 调试符号和调试器
- 全局函数和变量
- 源文件和行信息
- 类型信息
- 静态函数和局部变量
- 架构和编译器依赖
#### DWARF (Debugging With Attibuted Record Formats) 格式
#### 由一个个 DIE 组成（Debugging Information Entry) 以树的方式组织

## 0525
- 可以在汇编中间结果中看到调试信息（指定生产调试信息的时候 -g , -S 表示保存汇编中间结果）
    - g++ -g -S foo.cpp
- 从目标文件中读取调试信息
    - readelf --debug-dump foo.o
- 调试符号分为多个section
    - .debug_abbrev 缩略节(相当模板信息）
    - .debug_info (引用缩略节的内容表示调试符号具体信息）
        - 获取.debug_info的原始字节信息 objdump -s --section=.debug_info foo.o
    - .debug_line 

