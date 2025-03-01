## 为什么需要Makefiles？

Makefiles用于帮助确定大型程序的哪些部分需要重新编译。 在绝大多数情况下，C或C++文件都是需要编译的。 其他语言通常都有自己的工具，它们的用途与Make类似。 在编译之外Make也可用于当你需要根据文件更改情况运行一系列指令时。



## 有什么替代方案？

流行的C/C++替代构建系统是 [SCons](https://scons.org/) ， [CMake](https://cmake.org/) ， [Bazel](https://bazel.build/) ，和 [NINJA](https://ninja-build.org/) 。 一些代码编辑器，如 [Microsoft Visual Studio](https://visualstudio.microsoft.com/) 有自己的内置构建工具。 对于JAVA，有 [Ant](https://ant.apache.org/) ， [Maven](https://maven.apache.org/what-is-maven.html) ，和 [Gradle](https://gradle.org/) 。 像Go和Rust这样的其他语言都有自己的构建工具。

像Python、Ruby和Javascript这样的解释语言不需要类似Makefile的工具。 Makefiles的目标是根据更改的文件来编译需要编译的任何文件。 但当解释语言的文件发生变化时，不需要重新编译。 那些程序运行时，会直接使用文件的最新版本。



## 具体使用教程

[Makefile教程和示例指南 (foofun.cn)](http://makefiletutorial.foofun.cn/#make-clean)