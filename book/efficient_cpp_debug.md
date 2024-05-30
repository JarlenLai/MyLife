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


## 0526
- .deubg_line 源代码的行号调试符号被放置的地方
    - 由一系列操作码构成
    - 操作码可以生成状态表
    - 包含指令地址（函数开头的偏移量），相应的源代码行号和文件名

- .debug_frame 记录 CFI (Call Frame Information)。 
- .debug_loc 包含宏表达式的调试符号
- .debug_pubnames 全局变量和函数的查找表

### 实战故事1：数据类型不一致的问题
- 模块A中看到的数据结构大小在 B模块看到的不一样，#pragma pack(4) 的某些编译器下的写法。A 包含了头文件，B没有直接包含
### 调试器的内部结构
- 由三个模块组成 用户界面 符号管理 目标管理
    - 目标管理：如 linux 下借助了系统调用 ptrace
        - 系统调用追踪器 strace 可查看 gdb过程中使用了哪些 ptrace 调用处理
            - strace -o/home/my/ptrace.log -eptrace gdb a.out
            - cat /home/my/ptrace.log 
- add-symbol-file 命令把 新编译的变量符号类型信息加入 调试程序中
    - gcc -g -c -fPIC -o mm_symbol.o mm_symbol.c
    - (gdb) add-symbol-file mm_symbol.o 0xafsafsfasf
    - (gdb) print *(my_struct*) 0xsfsafsafsdf

## 0527
- 24页到30页
- 改变执行及其副作用
- 符号匹配的自动化， window 下由符号存储服务。 linux 下最近有  debuginfod 等工具
- 后期分析 core dump 核心转存文件
- 内存保护
- 断点不工作的一些原因

## 0528
- 30-40 第二章堆数据结构
- ptmalloc 和 TCmalloc
- ptmalloc
    - 通过边界标签以及盒子的数据结构来管理堆内存块
    - 快速盒子（fast bin), 特殊盒子-未排序的chunks, 大内存VMM 分配
    - 在 ptmalloc 中我们称堆为 arena
- TCmalloc (Thread-Caching Malloc)
    - 线程缓存
    - 大小类划分
    - 内存释放
    - 跟踪和监控
    - 页面堆（Page Heap)
        - 页面 (Page)
        - 跨度（Span)
        - 自由跨度列表（Free Span List)
        - 非空闲跨度列表 （Non-idle Span List）
- 利用堆元数据打印内存使用状态信息

## 0529 
43-53 第二章 内存损坏

## 0530
53-63 第二章
- 工具箱
    - 在分配的用户空间周围填充额外的字节
    - 使用系统保护页
    - 动态二进制分析 valgrind 
- 神秘的字节序转换
     
