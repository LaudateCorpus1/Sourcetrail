## Overview

Sourcetrail is an interactive source explorer that simplifies navigation in existing source code by indexing your code and gathering data about its structure. Sourcetrail then provides a simple interface consisting of three interactive views, each playing a key role in helping you obtain the information you need:

!["Sourcetrail Concept"](img/concept.png "Sourcetrail Concept")

* *Search:* Use the search field to quickly find and select indexed symbols in your source code. The autocompletion box will instantly provide an overview of all matching results throughout your codebase.
* *Graph:* The graph displays the structure of your source code. It focuses on the currently selected symbol and directly shows all incoming and outgoing dependencies to other symbols.
* *Code:* The Code view displays all source locations of the currently selected symbol in a list of code snippets. Clicking on a different source location allows you to change the selection and dig deeper.

Note: Sourcetrail currently supports the languages C/C++, Java and Python. Much of the UI design is therefore based on these languages and might change as soon as other languages are supported. For more information have a look at [supported languages](#supported-languages).

## Supported Languages

### C

C support is powered by [Clang 11.0.0](https://clang.llvm.org/). For issues loading C code, please have a look at [Clang language compatibility](https://clang.llvm.org/compatibility.html) or report a bug in our [bug tracker](https://github.com/CoatiSoftware/SourcetrailBugTracker).

### C++

C++ support is powered by [Clang 11.0.0](https://clang.llvm.org/). For more Information please visit [Clang C++ Status](https://clang.llvm.org/cxx_status.html). For issues loading C++ code, please have a look at [Clang language compatibility](https://clang.llvm.org/compatibility.html) or report a bug in our [bug tracker](https://github.com/CoatiSoftware/SourcetrailBugTracker).

### Java

Sourcetrail includes support for Java 12 and lower which is powered by [Eclipse JDT](https://github.com/eclipse/eclipse.jdt.core). If you encounter any issues while using Sourcetrail on a Java project, please let us know by providing a minimal example in our [bug tracker](https://github.com/CoatiSoftware/SourcetrailBugTracker).

### Python

Sourcetrail includes support for Python 2 and Python 3 which is powered by our open-source [SourcetrailPythonIndexer](https://github.com/CoatiSoftware/SourcetrailPythonIndexer). If you encounter any issues while using Sourcetrail on a Python project, please let us know by providing a minimal example in our [bug tracker](https://github.com/CoatiSoftware/SourcetrailPythonIndexer/issues).
