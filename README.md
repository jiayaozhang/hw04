# 高性能并行编程与优化 - 第04讲的回家作业


## 详细解释
1. size_t 在 64 位系统上相当于 uint64_t     size_t 在 32 位系统上相当于 uint32_t
   从而不需要用 movslq 从 32 位符号扩展到 64 位，更高效。而且也能处理数组大小超过 INT_MAX 的情况，推荐始终用 size_t 表示数组大小和索引
2. 开启优化：-O3
3. 浮点作为参数和返回：xmm系列寄存器  xmm寄存器有128位宽, 可以容纳4个float，或2个double
4. SIMD（single-instruction multiple-data）称为单个指令处理多个数据的技术,他可以大大增加计算密集型程序的吞吐量
5. AOS：紧凑存储多个属性. 符合一般面向对象编程(OOP)的习惯，但常常不利于性能
6. SOA：分离存储多个属性. 不符合面向对象编程(OOP)的习惯，但常常有利于性能。又称之为面向数据编程 (DOP)
7. AOSOA: SOA便于SIMD优化；AOS便于存储在传统容器；AOSOA两者得兼！ 
8. 对齐到 16 或 64 字节
9. 试试看 #pragma omp simd
10. 循环中不变的常量挪到外面来
11. 对小循环体用 #pragma unroll
12. -ffast-math 和 -march=native

## 评分规则

- 在你的电脑上加速了多少倍，就是多少分！请在 PR 描述中写明加速前后的用时数据。
- 最好详细解释一下为什么这样可以优化。会额外以乘法的形式加分。
- 比如你优化后加速了 50 倍，讲的很详细，所以分数乘 2，变成 100 分！
- 比如你优化后加速了 1000 倍，但是你的 PR 描述是空，所以分数乘 0，变成 0 分！

## 作业要求

利用这次课上所学知识，修改 main.cpp，优化其中的多体引力求解器：

- 不允许使用多线程并行
- 不允许做算法复杂度优化
- 可以针对编译器和平台优化，这次不要求跨平台
- 可以用 xmmintrin.h，如果你觉得编译器靠不住的话
