!["Sourcetrail"](img/logo.png "Sourcetrail")

Documentation for version 2021.1

# Welcome

This document is the official documentation of Sourcetrail and explains everything you need to know about working with the software.

For questions you may have that are not answered by this document, please send us an e-mail at: [support@sourcetrail.com](mailto:support@sourcetrail.com).


## Overview

Sourcetrail is an interactive source explorer that simplifies navigation in existing source code by indexing your code and gathering data about its structure. Sourcetrail then provides a simple interface consisting of three interactive views, each playing a key role in helping you obtain the information you need:

!["Sourcetrail Concept"](img/concept.png "Sourcetrail Concept")

* **Search:** Use the search field to quickly find and select indexed symbols in your source code. The autocompletion box will instantly provide an overview of all matching results throughout your codebase.
* **Graph:** The graph displays the structure of your source code. It focuses on the currently selected symbol and directly shows all incoming and outgoing dependencies to other symbols.
* **Code:** The Code view displays all source locations of the currently selected symbol in a list of code snippets. Clicking on a different source location allows you to change the selection and dig deeper.

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


# Getting Started

This short introduction will briefly guide you through the project setup and the user interface of Sourcetrail. The bullet point lists will provide you with the next steps to take:

## Starting Up Sourcetrail

Once you've [downloaded](https://github.com/CoatiSoftware/Sourcetrail/releases) Sourcetrail successfully you are ready to run the application. For assistance wth installation, visit the [installation](#installation) section.

> **Tasks:**
> * Launch Sourcetrail.

After launching Sourcetrail you will see the [Start Window](#start-window). From here you can create your own project or choose a pre-indexed one.

> **Tasks:**
> * Click **New Project** to create a new project.
> * or select one from the **Recent Projects** _(ex: TicTacToe)_ and continue with the [UI Intro](#ui-intro)

!["Start Window"](img/start_window.png "Start Window")

## Creating a New Project

When creating a new Sourcetrail project you will use the [Project Setup Wizard](#project-setup-wizard). This wizard splits the setup process into several subsequent steps. Depending on your project's structure and the used build system, there are different types for project setup. Choosing the correct setup method is important and can make the setup process a lot easier.

> **Tasks:**
> * Give your project a **Name** and select a **Location** for your Sourcetrail project to live.
> * Click **Add Source Group** to add source files to the project.

!["Project Setup Wizard Start"](img/project_setup_wizard_start.png "Project Setup Wizard Start")

### Add Source Group

Sourcetrail projects consist of multiple *Source Groups*. Each Source Group uses a certain language, a set of files, and all configurations to index these files. There are different types of Source Groups for each supported programming language. In addition, creating a single Source Group is sufficient for most projects.

Scroll past the image for detailed instructions on setting this up.

> **Tasks:**
> * Select your chosen **Source Group** setup type and come back here as soon as the project is created.

!["Project Setup Wizard Source Group Type"](img/project_setup_wizard_source_group_type.png "Project Setup Wizard Source Group Type")

#### Source Group Setup for C/C++

The Source Group setup types for C & C++ are the same.

**Are you using CMake, Make or Qt Creator?**

If you are using [CMake](https://cmake.org/) or [Make](https://www.gnu.org/software/make/) as build environment you can export a [clang JSON Compilation Database](https://clang.llvm.org/docs/JSONCompilationDatabase.html) as `compile_commands.json` file. A Compilation Database holds all information necessary for building the project, such as source files, include paths and compiler flags. Having a Compilation Database makes project setup within Sourcetrail a lot easier. We recommend using this approach if possible.

Exporting a Compilation Database:
* From **CMake** by defining the `CMAKE_EXPORT_COMPILE_COMMANDS` flag. (not supported on for Visual Studio CMake generators)
* For **Make** projects use [Bear](https://github.com/rizsotto/Bear). Bear generates a `compile_commands.json` file during a simulated build process. Bear has been tested on FreeBSD, GNU/Linux and OS X.
* From **Qt Creator since version 4.8** by selecting the "Generate Compilation Database" from the "Build" menu.

If you managed to export a `compile_commands.json` file, then please continue at [Create a Source Group from Compilation Database](#create-a-project-from-compilation-database) and come back after you finished creating the project.

!["Project Setup Wizard Start CDB"](img/project_setup_wizard_start_cdb.png "Project Setup Wizard Start CDB")

**Are you using Visual Studio?**

If you are using Visual Studio you can continue at [Source Group creation from Visual Studio](#create-a-project-from-visual-studio) and export a Compilation Database with our [Visual Studio Plugin](#visual-studio).

!["Project Setup Wizard Start VS"](img/project_setup_wizard_start_vs.png "Project Setup Wizard Start VS")

**Create Empty**

If neither of the above options apply to your project, please continue at [create an empty C/C++ Source Group](#create-an-empty-cxx-project) and return here once the project is created.

!["Project Setup Wizard Source Group Type"](img/project_setup_wizard_source_group_type.png "Project Setup Wizard Source Group Type")


#### Source Group Setup for Java

**Are you using Gradle?**

If you are using Gradle you can continue at [Source Group creation from Gradle](#create-a-project-from-gradle-configuration) to automatically setup your Source Group using your Gradle build configuration.

!["Project Setup Wizard Start Java Gradle"](img/project_setup_wizard_start_java_gradle.png "Project Setup Wizard Start Java Gradle")

**Are you using Maven?**

If you are using Maven please continue at [Source Group creation from Maven](#create-a-project-from-maven-configuration) to automatically setup your Source Group using your Maven build configuration.

!["Project Setup Wizard Start Java Maven"](img/project_setup_wizard_start_java_maven.png "Project Setup Wizard Start Java Maven")

**Create Empty**

If you do not have your project configured using Gradle or Maven, please continue at [Create an Empty Java Source Group](#create-an-empty-java-project) and come back here as soon as the project is created.

!["Project Setup Wizard Start Java Empty"](img/project_setup_wizard_start_java_empty.png "Project Setup Wizard Start Java Empty")

#### Source Group Setup for Python

**Create empty**

If you want to browse your Python source code with Sourcetrail, please continue at [Create an Empty Python Source Group](#create-an-empty-python-project) and come back here as soon as the project is created.

!["Project Setup Wizard Start Python Empty"](img/project_setup_wizard_start_python_empty.png "Project Setup Wizard Start Python Empty")

## Source Indexing

After the project is created, Sourcetrail will ask you whether you want to start indexing. Click **Start** and wait for the indexing to complete. This may take a bit of time. The [Indexing Dialog](#indexing-dialogs) and the [Status Bar](#status-bar) will give you information about the progress. Otherwise the UI will be empty. Sourcetrail indexes all named symbols and their relationships throughout the provided source files.

> **Tasks:**
> * Click **Start** when asked whether to start indexing.
> * Wait until the indexing of your source files has finished.
> * or Click **Stop** or press ESC to stop indexing (Sourcetrail will provide all information gathered so far and the indexing can be continued later by [refreshing](#refresh)).

!["Indexing"](img/indexing.png "Indexing")

After indexing is completed, Sourcetrail will show an overview of all indexed symbols in the [graph view](#graph-view) and some statistics in the [code view](#code-view).

#### Troubleshooting Errors

If the indexing yields errors, the status view will be shown with a list of errors. You can click on the errors label on the right side of the status bar or on one of the errors in the table to see their location.

> **Tasks:**
> * Fix your errors and [refresh](#refresh) to re-index the files with errors (Open Issue: As long as there was no change in the specific file, Sourcetrail won't reindex it, use the **Force Refresh** option from the [Edit Menu](#edit)).
> * or ignore them and continue with an incomplete index.

!["Error View"](img/error_view.png "Error View")

## User Interface

As mentioned earlier, Sourcetrail's user interface is split into three main views. Their arrangement can be adjusted as preferred and can also be detached from the main window and split into different screens (see [Window Widgets](#widget-windows)).

All three views display information about the currently selected symbol:

!["Main Screen"](img/main_screen.png "Main Screen")

### 1. Search Field

The [Search Field](#search-bar) allows for easy access to all indexed symbols. Use it to find all classes and functions you wish to investigate. In addition, it also holds the UI buttons for navigating [back & forward](#back-&-forward) as well as [refreshing](#refresh).

!["Search View"](img/search_view.png "Search View")

When entering a search query, the [autocompletion popup](#autocompletion-popup) will provide you with a concise list of all matching symbols. Note that Sourcetrail uses a fuzzy matching algorithm, that allows you to skip characters while entering a query.

!["Search View Completion"](img/search_view_completion.png "Search View Completion")

### 2. Graph Visualization

The [graph visualization](#graph-view) displays the currently selected symbol in an active state and all the other symbols it shares a relationship with. The visualization is made up of nodes and edges.

* **Nodes:** All named symbols in your source code will be displayed as different [nodes](#nodes), such as `functions`, `classes` or `files`. Nodes with members (like `classes`) can be expanded to show all their contents, the number at the expansion arrow shows how many members are hidden. Clicking a node will activate it and update all the views to the new selection. Dragging a node can be used to change its position.
* **Edges:** The relationships between the symbols are displayed as different [edges](#edges), such as `type use`, `function call` or `file include`. Sometimes edges get bundled together and are displayed as `bundled edges` that show a number of how many edges are contained. Clicking an edge will highlight its source location in the code view.

!["Graph View Graph"](img/graph_view_graph.png "Graph View Graph")

#### Colors:
The different node and edge types are also displayed using different colors. The default color scheme uses this convention:

| Color | Node | Edge
| - | - | -
| gray | types and classes | type use
| yellow | functions and methods | calls
| blue | variables and fields | variable access

#### Hatching:
Nodes displayed with a striped hatching, are nodes that were used within your indexed source files, but were not defined. Clicking them shows all locations where they are used, without providing their declaration.

!["Node Non Indexed"](img/node_non_indexed.png "Node Non Indexed")

#### Legend:

For a full list on all existing nodes and edges take a look at the integrated [Graph Legend](#graph-legend) by clicking the `?`-button in the bottom right corner of the [Graph View](#graph-view).

### 3. Code View

The [code view](#code-view) displays all locations of the currently active symbol within the indexed source files. It does not allow for editing the source code. Syntax highlighting is used to increase readability. Source locations that are surrounded by a box when hovered can be clicked to activate the respective symbol. Active source locations are highlighted.

!["Code View"](img/code_view.png "Code View")

The source locations are displayed as code snippets, containing the line of interest and extra lines added to the top and bottom to give information about its context. Code snippets are then bundled together into files.

**Note:** A file can be selected as active symbol by clicking its name in the title bar. By clicking the title bar or the icon on the right hand side of the title bar, the file can switch between 3 different states:

* **Minimized:** The file does not show any content

!["Snippet Minimized"](img/snippet_minimized.png "Snippet Minimized")

* **Snippets:** The file displays the snippets containing active locations separated by lines.

!["Snippet Snippets"](img/snippet_snippets.png "Snippet Snippets")

* **Maximized:** The [code view](#code-view) switches to [single file mode](#single-file-mode) and the whole content of the file is visible.

!["Code View Single"](img/code_view_single.png "Code View Single")

For more information, please visit the [Code View Files](#files) section.

## Start Exploring!

At this point, you should have an understanding of the basics of Sourcetrail's user interface and can begin exploring your codebase. Sourcetrail will allow you to see your source code from a whole new perspective, by giving you a concise overview of its parts and a faster way of drilling down to its internals, while always maintaining the connection to the implementation details of the actual source code.

Please take look at the much more extensive instruction manual below for detailed information.

If you would like to provide feedback, please do not hesitate to reach out to us via email: [support@sourcetrail.com](mailto:support@sourcetrail.com), we'd love to hear from you!

The Sourcetrail team wishes you a good start with our product, lots of saved time, increased productivity and much cleaner code.

> **Tasks:**
> * Start exploring and have fun!
