# miniSysY 编译实验
## 实验概述
 
SysY[^1] 语言是本实验的源语言。是一个c语言的子集，SysY 语言是单文件的，以 `.sy` 作为后缀，去除了c语言中的 include/define/pointer/struct 等较复杂特性，sysy 语言本身不具有 IO 功能，通过链接运行时库的方式进行 IO。

LLVM 是一个模块化的、可重用的编译器和工具链的集合，目的是提供一个现代的、基于 SSA 的、能够支持任意静态和动态编译的编程语言的编译策略。在最近几年已经成为表现上能够和 gcc 对标的项目。

LLVM IR 是 LLVM 项目中通用的中间代码，作为源语言和体系架构的连接部分，是学生需要从源语言中编译并翻译到的目标语言。

![](./pic/llvm_compiler_pipeline.png)

本实验的所有变动以及修改都是公开的（包括目前未正式发布的实验），你可以在[这里](https://github.com/BUAA-SE-Compiling/Slang-tutorial)查看我们的进度并通过 issue 的形式向我们提出意见和建议。 

### **实验目的**

本实验希望通过将复杂且庞大的 SysY 语言的特性拆分为多个小的模块与实验，引导同学们在思考-设计-实现-重新设计的过程中实现从源语言到 LLVM IR 的编译器，了解编译技术的整个流程，并且掌握一定的优化能力。

若完成所有实验，同学应该：

- 学会并理解了编译器的翻译流程
- 掌握了词法分析与语法分析的原理以及操作
- 掌握了语法制导翻译的原理以及操作
- 了解了编译优化的思想
- 掌握了部分简单的编译优化
- 熟悉了 gcc, llvm 等常见编译套件的使用以及用法

实验中不会涉及的东西：

- 手动内存管理
- 寄存器分配
- 对 ABI 的处理
- 体系结构相关的优化

**为什么选择 LLVM IR 而不是 GIMPLE 或者其他体系架构汇编与栈式虚拟机**：

GIMPLE 过于复杂，学习成本太高，不适宜用作教学实验。

软件学院并没有系统性地学习过 CISC 或者是 RISC 指令集，而且大三上学期软件学院其他课程过于繁重，增加指令集的学习会导致学习内容大幅增加。LLVM IR 本身不需要太多对体系架构的知识，并且完全能够胜任一门目标语言的工作。~~（而且助教评测起来也很方便）~~

栈式虚拟机本身结构较为简单，并且生成对应代码也比较简单，但是脱离了现在实际应用中的环境，学习栈式虚拟机指令和学习 LLVM IR 的成本相当，但 LLVM IR 具有实际且广泛的应用场景。

[^1]: 具体请参考语言定义页面
