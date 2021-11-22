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
| --- | --- | ---
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


# Installation

## Windows

Download and open the zip file and extract its contents into a temporary folder of your choice. Run the `setup.exe` and go through the wizard. You can now launch Sourcetrail from your start menu.

## macOS
Download and open the Sourcetrail.dmg file and drag Sourcetrail.app into the applications folder. You can now launch Sourcetrail from your Applications.

!["Installation macOS"](img/installation_mac.png "Installation macOS")

## Linux

### Tarball

Download the `.tar.gz` file and extract it. To start Sourcetrail run the `Sourcetrail.sh` script. Sourcetrail creates a folder `~/.config/sourcetrail` at the first run, this is the folder for Sourcetrail settings.

#### Install
To install Sourcetrail run the `install.sh` script with `sudo`. It will install Sourcetrail to `/opt/sourcetrail` and create the `/usr/bin/sourcetrail` symlink.

#### Uninstall
To uninstall Sourcetrail run the `/opt/sourcetrail/uninstall.sh` script with `sudo`.

### AppImage

Download the `.AppImage` file. Give it permission to execute with `chmod a+x` or via the context menu. To start Sourcetrail double click it or execute it from the Terminal. Sourcetrail creates a folder `~/.config/sourcetrail` at the first run, this is the folder for Sourcetrail settings.

For more information on AppImages please visit [appimage.org](https://appimage.org/).

## Data folder

The data folder holds certain files that are used by Sourcetrail to run the program. After following the [installation instructions](#installation) the data folder should be located in the following locations on your platform.

| Platform | Location
| --- | ---
| Windows | `C:/Users/You/AppData/Local/Coati Software/Sourcetrail` _(used for dynamic data and settings)_ `install_directory/Coati Software/Sourcetrail/data` _(used for static app data)_
| macOS | `~/Library/Application Support/Sourcetrail`
| Linux | `~/.config/sourcetrail`

## Finding System Header Locations

### Windows

These files usually ship with your compiler. For the Visual Studio IDE the system headers can be found at:
`<path_to_visual_studio>/VC/include/`
If you don't use the Visual Studio IDE you can also try to find your system headers in a subdirectory of:
`C:/Program Files (x86)/Windows Kits/`

### macOS

Run this command in your terminal:
`gcc -x c++ -v -E /dev/null`
You will find the header search paths your compiler uses in the output between these two lines:

```
#include <...> search starts here:
.
.
.
End of search list.
```

### Linux

`gcc -x c++ -v -E /dev/null`
or
`clang -x c++ -v -E /dev/null`
You will find the header search paths your compiler uses in the output between these two lines:

```
#include <...> search starts here:
.
.
.
End of search list.
```


## Finding Java Runtime Library Location

The current version of Sourcetrail requires an installation of the Java 8 runtime environment to index any Java project. Make sure that Sourcetrail and your JRE share the same kind or architecture (a 32 bit Sourcetrail requires a 32 bit JRE). To locate the required library file, please refer to the applicable description below.

### Windows

The Java Runtime Library (called `jvm.dll`) can be found inside of your JRE install folder and looks like this:
`<path_to_jre>/bin/client/jvm.dll`

### macOS

The Java Runtime Library (called `libjli.dylib`) can be found inside of your JDK install folder. Run the following command in your terminal to find the location of your default Java installation:
`/usr/libexec/java_home`

This should give you a path looking like this:
`/Library/Java/JavaVirtualMachines/<jdk_version>/Contents/Home`

The `"libjli.dylib"` should be available at:
`/Library/Java/JavaVirtualMachines/<jdk_version>/Contents/MacOS/libjli.dylib`

Insert the full path to `libjli.dylib` into the **Java Path** setting in the [Preferences Window](#preferences-window).

### Linux

The Java Runtime Library (called `libjvm.so`) can be found inside of your JRE install folder and looks like this:
`<path_to_jre>/lib/<arch>/server/libjvm.so`

# Interface

## Main Window

### Subwindows

Sourcetrail's three views are organized into subwindows, which can be freely arranged within the Main Window or detached from it. Each subwindow has a title bar displaying its name and 2 buttons for closing the subwindow and for detaching it from the Main Window.

!["Main Window"](img/main_window.png "Main Window")

**Interactions:**

* Drag the subwindow at the title bar to rearrange it within the Main Window, detach it or attach it again.
* Press the "x" icon to close the subwindow. They can be reopened from the [View Menu](#view).
* Press the "□" icon to detach the subwindow from the Main Window.

### Tab Bar

The Tab Bar is located at the top of the [Main Window](#main-window) and is used to open multiple symbols in parallel.

!["Tab Bar"](img/tab_bar.png "Tab Bar")

**Interactions:**

* Click on the `+` icon to open a new tab or use the [New Tab Shortcut](#shortcuts).
* Click on a tab to activate it and show it's content or use the [Next/Previous Tab Shortcuts](#shortcuts).
* Click on the `x` icon on the right of each tab to close it or use the [Close Tab Shortcut](#shortcuts).
* Click and drag a tab to change it's position.

### Status Bar

The Status Bar is located on the bottom of the [Main Window](#main-window) and is used to convey information about Sourcetrail's status and currently running processes to the user

It displays:

* The most recent status message.
* The current status of the [Code Editor Plugin](#code-editor-plugins) connection
* Error Count if the currently loaded project has errors.
* Indexing progress bar while indexing.

!["Status Bar"](img/status_bar.png "Status Bar")

**Interactions:**

* Click on the status message count to display the (Status Tab](#status-tab).
* Click on the error count to display the error locations in the [Code View](#code-view).
* Click on the indexing progress bar to display the [Indexing Dialogs](#indexing-dialogs) if they were hidden.

### On-Screen Search Bar

The On-Screen Search Bar is used to search visible contents of the [Graph View](#graph-view) and [Code View](#code-view). It gets displayed at the bottom of the [Main Window](#main-window) when using the [Find On-Screen](#shortcuts) action.

!["Onscreen Search Bar"](img/onscreen_search_bar.png "Onscreen Search Bar")

**Interactions:**

* Enter a search query to search in contents of the [Graph View](#graph-view) and [Code View](#code-view).
* Click the arrow buttons next to the search field to iterate the matched locations.
* Use the checkboxes right of the search field to define which view contents will be matched.
* Click the `x` icon on the right to close the On-Screen Search Bar or press `ESC`.

## Windows

### Start Window

On every start of Sourcetrail you are shown the start window. It allows for creating new projects or opening existing ones.

!["Start Window"](img/start_window.png "Start Window")

**Interactions:**

* Clicking `New Project` will lead you to [Project Setup](#project-setup-wizard).
* Clicking `Open Project` will let you open an existing Sourcetrail project by choosing from a file dialog.
* Clicking on one of the `Recent Projects` will open this project. The list shows a maximum of 7 items ordered by recent first.
* Pressing `ESC` will close the window.
* Click `Check for new version` to connect to [https://sourcetrail.com](https://sourcetrail.com) and check if a new version is available.


### Path List Box

The Path List Box is a user interface element that is used within the [Preferences Window](#preferences-window) and the [Project Setup Wizard](#project-setup-wizard). It allows for entering a list of file and directory paths.
If you want to use environment variables you can use either of the following notations.
`${VARIABLE_NAME}` or `%VARIABLE_NAME%`

!["Path List Box"](img/path_list_box.png "Path List Box")

**Interactions:**

* Click the "+" icon to add a new path line.
* Click the "-" icon to remove a selected path line.
* Click a path line to select it.
* Enter the path by typing on your keyboard
* Click "..." within the path line to open a file dialog for choosing a file or directory path.
* Directly add multiple paths into the box by dropping elements from your filesystem.
* Click the pen icon in the bottom right corner to edit the list as plain text.

#### Plain Text Editing

By pressing the pen icon in the bottom right corner you can open the plain text edition dialog. It allows you to edit the whole list within a text field. Each line will be one list item.

!["Path List Box Edit"](img/path_list_box_edit.png "Path List Box Edit")

**Interactions:**

* Add and remove list items through keyboard interaction.
* Click `Cancel` to cancel plain text editing.
* Click `Save` to save your changes to the list.

### Preferences Window

The Preferences window lets you define settings for all projects. You can open the Preferences from the menu via [Edit/Preferences](#edit).

!["Preferences Screen"](img/preferences_screen.png "Preferences Screen")

| Setting | Description
| --- | ---
| Font Face | Define the font face used throughout the UI
| Font Size | Set the font size used throughout the UI. It can also be changed with the actions in the [View Menu](#view)
| Tab Width | Define the space width of tabs in the code view.
| Text Encoding | Define the Text Encoding used for displaying your source code.
| Color scheme | Choose which color scheme Sourcetrail should display. The color schemes are located in [data](#datafolder)/color_schemes/
| Animations | Define if animations are used within the user interface.
| Built-In Types | Define whether built-in types such as int or bool are shown when referenced in the graph view.
| Directory in File Title | Enable display of the parent directory of a code file relative to the project file.
| Auto Scaling to DPI | **(Linux only)** Define if automatic scaling to screen DPI resolution is active. This setting manipulates the environment flag `QT_AUTO_SCREEN_SCALE_FACTOR` of the Qt framework. Choose 'system' to stick to the setting of your current environment.
| Scale Factor | **(Linux only)** Define a screen scale factor for the user interface of the application. This setting manipulates the environment flag `QT_SCALE_FACTOR` of the Qt framework. Choose 'system' to stick to the setting of your current environment.
| Scroll Speed | Define a multiplyer for the default scroll speed. Values smaller than 1 slow down scrolling while values greater than 1 increase the scroll speed.
| Graph Zoom | Switch the default mouse wheel behavior in the graph between scrolling and zooming.
| Logging | Ticking this box enables logging to console and to a log file. This option is disabled by default to speed up Sourcetrail. If you encounter problems while running Sourcetrail, we recommend to enable this option so you have somewhere to start looking for a cause.
| Indexer Logging | When enabled Sourcetrail will log detailed information during indexing. This log data can help us fix issues.
| Automatic Update Check | Check to automatically check whether a new version of Sourcetrail is available once every day.
| Sourcetrail Port | Port number that Sourcetrail uses to listen for incoming messages from plugins.
| Plugin Port | Port number that Sourcetrail sends outgoing messages to.
| Indexer threads | Define how many parallel threads are used during indexing. Setting this value to `default` will cause Sourcetrail to detect the ideal number of threads based on the CPU and use as many threads for indexing.
| Multi process C/C++ indexing | Enable C/C++ indexer threads to run in a different process. This prevents the application from crashing due to unforeseen exceptions while indexing.
| Java Path | If you want to use Sourcetrail on Java source code, please specify a path to your Java 8 runtime library. Please keep in mind that a 32 bit Sourcetrail requires a 32 bit version of Java while a 64 bit Sourcetrail requires a 64 bit Java to be working correctly. You can either use the button below for automatic detection or add the path manually. For instructions on how to find your Java runtime path see (Finding Java Runtime Library Location](#finding-java-runtime-library-location).
| JRE System Library | Add the jar files of your JRE System Library. These jars can be found inside your JRE install directory. You can either use the button below for automatic detection or add the paths manually.
| Maven Path | Only required for indexing projects using Maven. Provide the location of your installed Maven executable. You can also use the auto detection.
| Post Processing | Enable a post processing step to solve unsolved references after the indexing is done. These references will be marked "ambiguous" to indicate that some of these edges may never be encountered during runtime of the indexed code because the post processing only relies on symbol names and types.
| Global Include Paths | Set header search paths that are used for **all** of your projects (e.g. std headers). An option for automatic detection of these paths is available for Clang, GCC and the Visual Studio compiler. For instructions on how to add paths manually see [Path List Box](#path-list-box). For instructions on how to find the system header paths see [Finding System Header Locations](#finding-system-header-locations).
| Global Framework Search Paths | **(macOS only)** Define the search paths for `.framework` files for all of your projects. An option for automatic detection of these paths is available for Clang and GCC. For instructions on how to add paths see [Path List Box](#path-list-box).

### Project Setup Wizard
The Project Setup Wizard lets you create a new Sourcetrail project. It allows for defining name and location of your project Sourcetrail and adding several **Source Groups**, that define which source files will be indexed. There are several ways to create Source Groups. It is sufficient to add only one Source Group for most projects.

For detailed information continue at [PROJECT SETUP](#project-setup).

!["Project Setup Wizard Start"](img/project_setup_wizard_start.png "Project Setup Wizard Start")

### Indexing Dialogs

These dialogs will be used while Sourcetrail indexes your project. The whole user interface will be frozen as long as these dialogs are visible.

#### Start Indexing Dialog

This dialog displays the number of files for indexing and clearing before indexing starts. There are different refresh modes:


* **Updated files:** Reindexes all files that were modified since the last indexing, all files depending on those and new files.
* **Incomplete & updated files:** Reindexes all files that had errors during last indexing, all files depending on those and all updated files.
* **All files:** Deletes the previous index and reindexes all files.


**Shallow Python Indexing**

For Python projects a checkbox **Shallow Python Indexing** is additionally displayed. When checked, references within your code base (calls, usages, etc.) are resolved by name, which is imprecise but much faster than in-depth indexing. Use this option for a quick first indexing pass and start browsing the code base while running a second pass for in-depth indexing.

!["Start Indexing Dialog"](img/start_indexing_dialog.png "Start Indexing Dialog")

**Interactions:**

* Switch indexing mode by clicking a different option.
* Clicking `Cancel` will abort indexing.
* Clicking `Start` will start the file clearing and indexing.

#### Progress Dialog

This dialog shows that Sourcetrail is currently doing processing that can't be interrupted.

!["Progress Dialog"](img/progress_dialog.png "Progress Dialog")

**Interactions:**

* Clicking `Hide` will hide the dialog. You can display it again by clicking on the indexing progress bar in the [status bar](#status-bar) or [refreshing](#refresh).

#### Indexing Dialogs

This dialog shows the indexing progress of your project, by displaying the number of already indexed files, the last file that was started indexing, the number of errors and a progress estimate in percent.

!["Indexing Dialog"](img/indexing_dialog.png "Indexing Dialog")

**Interactions:**

* Clicking `Stop` or pressing ESC will interrupt indexing. Sourcetrail will still wait for the already running indexer threads to finish. You can continue indexing later by [refreshing](#refresh).
* Clicking `Hide` will hide the dialog. You can display it again by clicking on the indexing progress bar in the [status bar](#status-bar) or [refreshing](#refresh).

#### Finished Indexing Dialog

This dialog is shown after indexing finished, giving you information about indexed files, duration and errors.

!["Finished Indexing Dialog"](img/finished_indexing_dialog.png "Finished Indexing Dialog")

#### Interrupted Indexing Dialog

This dialog is shown after indexing was stopped, giving you information about indexed files, duration and errors. You can choose to either use the new index or continue using the old one.

!["Interrupted Indexing Dialog"](img/finished_indexing_dialog.png "Interrupted Indexing Dialog")

**Interactions:**

* Clicking `Discard` will discard the new index.
* Clicking `Keep` will switch your project to the new index and discard the old one.

## Menu

### Project

* **New Project**
    * Shortcut: [New Project](#shortcuts)
    * Opens the [New Project](#project-setup-wizard) Dialog to define a new project and loads it after creation.
* **Open Project**
    * Shortcut: [Open Project](#shortcuts)
    * Opens a file dialog to choose an existing Sourcetrail project file from your system's hard drive.
* **Recent Projects**
    * Opens a submenu to choose recent opened Sourcetrail projects.
* **Edit Project**
    * Opens the [Edit Project Dialog](#project-setup-wizard) prefilled with your project settings and allows for changing them.
* **Exit**
    * Quits Sourcetrail.

### Edit

* **Refresh**
    * Shortcut: [Refresh](#shorcuts)
    * Refresh will check all indexed source files for updates and reindex the ones that changed and their depending ones.
* **Full Refresh**
    * Shortcut: [Full Refresh](#shorcuts)
    * Full Refresh will reindex the whole project.
* **Find Symbol**
    * Shortcut: [Find Symbol](#shorcuts)
    * This option will put the focus into the search field, so you can start typing your search query. Alternatively you can click the search field.
* **Find Text**
    * Shortcut: [Find Text](#shorcuts)
    * This option will put the focus into the search field and start a new full text search query
* **Find On-Screen**
    * Shortcut: [Find On-Screen](#shorcuts)
    * Display the [On-Screen Search Bar](#on-screen-search-bar) to search visible contents of the [Graph View](#graph-view) and [Code View](#code-view)
* **Next Reference**
    * Shortcut: [Next Reference](#shorcuts)
    * Use this option to iterate to the next source location of the active symbol in the code view.
* **Previous Reference**
    * Shortcut: [Previous Reference](#shorcuts)
    * Use this option to iterate to the previous source location of the active symbol in the code view.
* **Next Local Reference**
    * Shortcut: [Next Local Reference](#shorcuts)
    * Use this option to iterate to the next source location of the active local symbol or edge in the code view.
* **Previous Local Reference**
    * Shortcut: [Previous Local Reference](#shorcuts)
    * Use this option to iterate to the previous source location of the active local symbol or edge in the code view.
* **To overview**
    * Shortcut: [To overview](#shorcuts)
    * This option will display the overview of the project.
* **Preferences**
    * Shortcut: [Preferences](#shorcuts)
    * Opens the [Preferences Window](#preferences-window).

### View

* **New Tab**
    * Opens a new tab.
* **Close Tab**
    * Closes the current tab.
* **Select Next Tab**
    * Switch to the tab to the right of the current tab.
* **Select Previous Tab**
    * Switch to the tab to the left of the current tab.
* **Show Start Window**
    * Shows the [Start Window](#start-window).
* **Show Title Bars**
    * Toggle the visibility of the bars above each [Window Widget](#widget-windows).
* **Reset window layout**
    * Resets all the dock widgets to their original layout.
* **Search Window**
    * Toggle the visibility of the Search Window. This can also be done by closing the Search Window on clicking the "x" icon in it's title bar. (See [Window Widgets](#widget-windows))
* **Graph Window**
    * Toggle the visibility of the Graph Window. This can also be done by closing the Graph Window on clicking the "x" icon in it's title bar. (See [Window Widgets](#widget-windows))
* **Code Window**
    * Toggle the visibility of the Code Window. This can also be done by closing the Code Window on clicking the "x" icon in it's title bar. (See [Window Widgets](#widget-windows))
* **Status Window**
    * Toggle the visibility of the Status Window. This can also be done by closing the Status Window on clicking the "x" icon in it's title bar. (See [Window Widgets](#widget-windows))
* **Larger Font**
    * Shortcut: [Larger Font](#shortcuts)
    * Increase the font size within the Main Window's user interface.
* **Smaller Font**
    * Shortcut: [Smaller Font](#shortcuts)
    * Decrease the font size within the Main Window's user interface.
* **Reset font size**
    * Shortcut: [Reset font size](#shortcuts)
    * Resets the font size to the original size.

### History

* **Back**
    * Shortcut: [Back](#shortcuts)
    * Undoes the last navigation action.
* **Forward**
    * Shortcut: [Forward](#shortcuts)
    * Redoes an undone navigation action.
* **Recently Active Symbols**
    * List the history of active symbols in chronologic order.

### Bookmarks

* **Bookmark Active Symbol**
    * Shortcut: Bookmark Active Symbol](#shortcuts)
    * Opens the [Bookmark Creator](#bookmark-creator) dialog create a new bookmark.
* **Bookmark Manager**
    * Shortcut: Bookmark Manager](#shortcuts)
    * Opens the [Bookmark Manager](#bookmark-manager) dialog for viewing all bookmarks.
* **Recent Bookmarks**
    * List of recently added bookmarks for quick activation.

### Help

* **About**
    * Shows copyright information about Sourcetrail.
* **Keyboard Shortcuts**
    * Shows table of keyboard shortcuts for Sourcetrail.
* **Documentation**
    * Opens this documentation of Sourcetrail in your web browser by URL.
* **Changelog**
    * Opens the [changelog](https://github.com/CoatiSoftware/SourcetrailBugTracker#changelog) of Sourcetrail in your web browser by URL.
* **Bug Tracker**
    * Opens Sourcetrail's bug tracker in your web browser by URL.
* **License**
    * Opens a window containing the Sourcetrail license and all 3rd party licenses.
* **Show Data Folder**
    * Opens the file explorer showing the [data folder](#datafolder).
* **Show Log Folder**
    * Opens the file explorer in the directory [data](#datafolder)/logs where all log files are saved to. You can enable file logging in the [Preferences Window](#preferences-window).


### Shortcuts

#### General

| Shortcut | Windows | macOS | Linux
| --- | --- | --- | ---
| Switch Focus Between Graph/Code Views | `Tab` | `Tab` | `Tab`
| Preferences | `Ctrl + ,` | `Cmd + ,` | `Ctrl + ,`
| New Project | `Ctrl + N` | `Cmd + N` | `Ctrl + N`
| Open Project | `Ctrl + O` | `Cmd + O` | `Ctrl + O`
| Close Window | `Alt + F4` | `Cmd + W` | `Ctrl + W`
| Hide Window |  | `Cmd + H` |
| Refresh | `F5` | `Cmd + R` | `F5`
| Full Refresh | `Shift + F5` | `Cmd + Shift + R` | `Shift + F5`
| Back | `Z` / `Alt + Left` / `Backspace` | `Z` / `Cmd + [` / `Backspace` | `Z` / `Alt + Left` / `Backspace`
| Forward | `Shift + Z` / `Alt + Right` | `Shift + Z` / `Cmd + ]` | `Shift + Z` / `Alt + Right`
| Find Symbol | `Ctrl + F` | `Cmd + F` | `Ctrl + F`
| Find Text | `Ctrl + Shift + F` | `Cmd + Shift + F` | `Ctrl + Shift + F`
| Find On-Screen | `Ctrl + D` | `Cmd + D` | `Ctrl + D`
| To overview | `Ctrl + Home` | `Cmd + Home` / `Cmd + Up` | `Ctrl + Home`
| New Tab | `Ctrl + T` | `Cmd + T` | `Ctrl + T`
| Close Tab | `Ctrl + W` | `Cmd + W` | `Ctrl + W`
| Select Next Tab | `Ctrl + Tab` | `Ctrl + Tab` | `Ctrl + Tab`
| Select Previous Tab | `Ctrl + Shift + Tab` | `Ctrl + Shift + Tab` | `Ctrl + Shift + Tab`
| Larger Font | `Ctrl + +` | `Cmd + +` | `Ctrl + +`
| Smaller Font | `Ctrl + -` | `Cmd + -` | `Ctrl + -`
| Reset Font Size | `Ctrl + 0` | `Cmd + 0` | `Ctrl + 0`
| Bookmark Active Symbol | `Ctrl + S` | `Cmd + S` | `Ctrl + S`
| Bookmark Manager | `Ctrl + B` | `Cmd + B` | `Ctrl + B`

#### Graph View

| Shortcut | Windows | macOS | Linux
| --- | --- | --- | ---
| Move Focus Within Nodes | `WASD` / `HJKL` / `Arrows` | `WASD` / `HJKL` / `Arrows` | `WASD` / `HJKL` / `Arrows`
| Move Focus Within Edges | `Shift + WASD` / `Shift + HJKL` / `Shift + Arrows` | `Shift + WASD` / `Shift + HJKL` / `Shift + Arrows` | `Shift + WASD` / `Shift + HJKL` / `Shift + Arrows`
| Activate Node/Edge | `Enter` / `E` | `Enter` / `E` | `Enter` / `E`
| Activate Node in New Tab | `Ctrl + Shift + Enter` / `Ctrl + Shift + E` | `Cmd + Shift + Enter` / `Cmd + Shift + E` | `Ctrl + Shift + Enter` / `Ctrl + Shift + E`
| Expand/Collapse Node | `Shift + Enter` / `Shift + E` | `Shift + Enter` / `Shift + E` | `Shift + Enter` / `Shift + E`
| Pan | `Ctrl + Arrows` | `Cmd + Arrows` | `Ctrl + Arrows`
| Zoom In | `Ctrl + Shift + Up` / `Ctrl + Mouse Wheel Up` | `Cmd + Shift + Up` / `Cmd + Mouse Wheel Up` | `Ctrl + Shift + Up` / `Ctrl + Mouse Wheel Up`
| Zoom Out | `Ctrl + Shift + Down` / `Ctrl + Mouse Wheel Down` | `Cmd + Shift + Down` / `Cmd + Mouse Wheel Down` | `Ctrl + Shift + Down` / `Ctrl + Mouse Wheel Down`
| Reset Zoom | `0` | `0` | `0`
| Open Custom Trail Dialog | `Ctrl + U` | `Cmd + U` | `Ctrl + U`

#### Code View

| Shortcut | Windows | macOS | Linux
| --- | --- | --- | ---
| Next Reference | `Ctrl + G` | `Cmd + G` | `Ctrl + G`
| Previous Reference | `Ctrl + Shift + G` | `Cmd + Shift + G` | `Ctrl + Shift + G`
| Next Local Reference | `Ctrl + T` | `Cmd + T` | `Ctrl + T`
| Previous Local Reference | `Ctrl + Shift + T` | `Cmd + Shift + T` | `Ctrl + Shift + T`
| Move Focus Within Code | `WASD` / `HJKL` / `Arrows` | `WASD` / `HJKL` / `Arrows` | `WASD` / `HJKL` / `Arrows`
| Move Focus to Closest Reference | `Shift + WASD` / `Shift + HJKL` / `Shift + Arrows` | `Shift + WASD` / `Shift + HJKL` / `Shift + Arrows` | `Shift + WASD` / `Shift + HJKL` / `Shift + Arrows`
| Activate Location | `Enter` / `E` | `Enter` / `E` | `Enter` / `E`
| Activate Location in New Tab | `Ctrl + Shift + Enter` / `Ctrl + Shift + E` | `Cmd + Shift + Enter` / `Cmd + Shift + E` | `Ctrl + Shift + Enter` / `Ctrl + Shift + E`
| Scroll | `Ctrl + Arrows` | `Cmd + Arrows` | `Ctrl + Arrows`

## Graph View
The graph view visualizes the currently selected symbol and all its relationships to other symbols as an interactive graph visualization. You can also display whole call graphs, inheritance chains or include trees by using the toolbar in the top left. Read more about that at [Custom Trail](#custom-trail).

!["Graph View"](img/graph_view.png "Graph View")

#### Interactions:

**Buttons:**

* Use the trail navigation in the top left to create [Custom Trails](#custom-trail).
* Use the grouping buttons in the top left to enable [Node Grouping](#node-grouping) by namespace/package or file.
* Press the `+` and `-` buttons in the lower left corner to change the zoom level.
* Press the `?` button in the bottom right corner to show the [Graph Legend](#graph-legend).

**Panning:**

* Drag the background area with the mouse.
* Scroll left-right and up-down on the mouse pad.
* Use the keys `W` `A` `S` `D`.


**Zooming:**

* Hold `Ctrl/Cmd` and scroll with mouse wheel or mouse pad.
* Press `Shift + W` or `Shift + S`.
* Press `0` to reset zoom.


**Context Menu:**

* **Open in New Tab:** Opens a new Tab with the node under the mouse cursor as active symbol.
* **Back:** Go back in history.
* **Forward:** Go forward in history.
* **Show Definition:** Show the definition of the node under the mouse cursor in the [Code View](#code-view).
* **Show Definition in IDE:** Show the definition of the node under the mouse cursor using the connected [Code Editor Plugin](#code-editor-plugin).
* **Expand Node:** Expand node under mouse cursor.
* **Collapse Node:** Collapse node under mouse cursor.
* **Hide Node:** Hide node under mouse cursor.
* **Hide Edge:** Hide edge under mouse cursor.
* **Bookmark Node:** Create a bookmark for node under mouse cursor.
* **Save As Image:** Export current graph as image file. Possible formats are `PNG`, `JPEG`, `BMP` and `SVG`.
* **Save To Clipboard:** Save current graph as `PNG` image to clipboard.
* **Copy Name:** Copy name for node under mouse cursor to clipboard.
* **Copy Full Path:** Copy file path for file node under mouse cursor to clipboard.
* **Open Containing Folder:** Show the file in your file explorer for file node under mouse cursor.


### Nodes
Colors are corresponding to the default color scheme.

| Node Type | Image
| --- | ---
| **File**: Non-indexed files are files that are not part of any source group and therefore have not been indexed by Sourcetrail's indexer. Incomplete files produced errors during indexing or where part of an indexer run with errors. | !["Node File"](img/node_file.png" "Node File")
| **Macro** | !["Node Macro"](img/node_macro.png "Node Macro")
| **Namespace, Package & Module** | !["Node Namespace"](img/node_namespace.png "Node Namespace")
| **Class & Struct**: Display their members nested, and separated by access type: public, protected, private. By default only members with edges are shown. The arrow icon allows to expand and collapse them. The number tells how many nodes are hidden. | !["Node Class"](img/node_class.png "Node Class")
| **Type** | !["Node Type"](img/node_type.png "Node Type")
| **Typedef** | !["Node Typedef"](img/node_typedef.png "Node Typedef")
| **Variable & Field** | !["Node Variable"](img/node_variable.png "Node Variable")
| **Function & Method** | !["Node Function"](img/node_function.png "Node Function")
| **Enum & Enum Constant** | !["Node Enum"](img/node_enum.png "Node Enum")
| **Bundle**: A bundle node combines multiple nodes to reduce the size of the graph visualization. The name describes what kind of nodes are bundled. The number tells how many nodes are bundled. | !["Node Bundle"](img/node_bundle.png "Node Bundle")
| **Group: A group node shows that all contained nodes share something in common e.g. same file or namespace. | !["Node Group"](img/node_group.png "Node Group")

**Interactions:**

* Click a node to activate it.
* Drag a node to change its position.
* Click the arrow icon in class nodes to expand and collapse it.
* Click a bundle node to expand it.
* Hover a node to see a tooltip that displays the node’s type.

### Edges
Colors are corresponding to the default color scheme.

| Edge Type | Image
| --- | ---
| **File Include** | !["Edge Include"](img/edge_include.png "Edge Include")
| **Type Use** | !["Edge Use"](img/edge_type_usage.png "Edge Use")
| **Variable Use** | !["Edge Variable Use"](img/edge_variable_use.png "Edge Variable Use")
| **Function Call** | !["Edge Call"](img/edge_call.png "Edge Call")
| **Inheritance** | !["Edge Inheritance"](img/edge_inheritance.png "Edge Inheritance")
| **Method Override** | !["Edge Override"](img/edge_override.png "Edge Override")
| **Template Specialization & Template Argument Use** | !["Edge Template Param"](img/edge_template_param.png "Edge Template Param")
| **Template Member Specialization** | !["Edget Template Member Specialization"](img/edge_template_member_specialization.png "Edget Template Member Specialization")
| **Bundled Edges**: Bundles multiple edges between the child nodes of the 2 nodes. The thickness gives an impression of how many edges are bundled. Hover the edge to get the number of bundled edges. | !["Edge Bunled Edges"](img/edge_bundled_edges.png "Edge Bunled Edges")

**Interactions:**

* Click an edge to see its location in the [Code View](#code-view).
* Click a bundled edges to activate all its corresponding edges.
* Hover an edge to see a tooltip that displays the edge’s type.

### Custom Trail
Using the toolbar in the top left you can display whole call graphs, inheritance chains or include trees for the currently active symbol if the right symbol type is currently active. Or you can use the Custom Trail Dialog to display graphs based on custom criteria.

!["Call Graph"](img/call_graph.png "Call Graph")

**Interactions:**

* Click the arrow button to expand/collapse the `Custom Trail` controls.
* Click the `Custom Trail Dialog` button to show the `Custom Trail Dialog`.
* Click the `Predefined Custom Trail` buttons to show a graph of depending/dependent nodes based on the currently active symbol.
* Change the slider position to change the maximum depth of the graph. Moving it to the top will use infinite depth.
* Click on a node to activate it.
* Click on an edge to show it's source location in the [Code View](#code-view).


#### Custom Trail Dialog
The Custom Trail Dialog can be accessed within the trail controls in the top left of the graph view. It allows to display Custom Trails based on certain criteria.

!["Custom Trail"](img/custom_trail.png "Custom Trail")

Every Custom Trail has a specific Start Symbol, then 1 of 3 different modes can be chosen:

| Mode | Description
| --- | ---
| **To Target Symbol** | Specify another target symbol. The graph will only contain paths from the origin to the target symbol.
| **All Referenced** | The graph will only contain nodes that are referenced by the origin symbol.
| **All Referencing** | The graph will only contain nodes that depend on the origin symbol.

Additional options allow defining which information should be shown:

| Setting | Description
| --- | ---
| **Maximum Depth** | Define the depth of the resulting graph. When searching paths from origin to target, all paths that are beyond this depth will not be found.
| **Layout Direction** | Define if the graph should be displayed vertically or horizontally.
| **Node Filters** | Define which node types will be part of the resulting graph. Only node types present in the loaded project are displayed. This setting is ignored for the origin and target nodes.
| **Edge Filters** | Define which edge types will be part of the resulting graph. Only node types present in the loaded project are displayed. The special edge "member" defines whether parent-child relations are considered as edge.

**Interactions:**

* Search for start and target symbols using a search field. The interactions are the same as in the main [Search Field](#search-bar).
* Drag the Max Depth slider to change the maximum depth of the resulting graph.
* Click the **Check All** and **Uncheck All** buttons to check all available node or edge filters.
* Click on Cancel to close the dialog.
* Click on Search to search for a Custom Trail using the selected options.

### Node Grouping

Using grouping buttons in the top left you can specify if nodes in the graph shall be grouped by either namespace/package or defining file.

!["Grouping Buttons"](img/grouping_buttons.png "Grouping Buttons")

#### Namespace/Package Grouping

All nodes that belong to the same namespace or package are grouped together in a separate group node.

!["Grouping Namespace"](img/grouping_namespace.png "Grouping Namespace")

#### File Grouping

All nodes defined in the same source or header file are grouped together in a separate group node.

!["Grouping File"](img/grouping_file.png "Grouping File")

**Interactions:**

* Click on the group name to activate the corresponding namespace/package or file node.


### Graph Legend

Click the `?` button in the bottom right corner of the graph view or enter the keyword `legend` in the [search field](#search-bar) to show the graph legend. It gives you an overview on the different node and edge types and provides examples of graph layouts.

!["Graph Legend"](img/graph_legend.png "Graph Legend")

## Code View

The code view displays the corresponding source code of the currently selected symbols. The code view has two modes. In list mode it contains a list of one or more files. In single file mode it shows one full source file at a time.

!["Code View"](img/code_view.png "Code View")

**Interactions:**

* Iterate the references of the currently active symbol with the `reference` navigation in the upper left corner.
* Iterate local references of the currently selected local variable or multiple references of a symbol within a local scope with the `local reference` navigation in center.
* Switch between Snippet List and Single File mode with the `mode selection` in the upper right corner.
* Scroll up and down to see the different source files.

!["Code View Show Errors"](img/code_view_show_errors.png "Code View Show Errors")

If a viewed file had errors during indexing, its file icon will contain an `x` and there is a `Show Errors`-button visible in the files title bar. Clicking one `Show Errors` will show you only the errors that cause this specific file to be incomplete in the [Errors Tab](#errors-tab).

### Snippet List Mode

In this mode the Code View will provide all references of the currently active symbol at once. The top most snippet will show the definition of the symbol if available.

#### Files

Each file has a title bar with the file's name. Clicking the title bar will change the display state. There are 2 different states:

* **Minimized:** The file does not show its content.

!["Snippet Minimized"](img/snippet_minimized.png "Snippet Minimized")

* **Snippets:** The file displays the snippets containing active locations separated by lines.

!["Snippet Snippets"](img/snippet_snippets.png "Snippet Snippets")

**Interactions:**

* Hover the title to see the full file path.
* Click the title to activate the file's corresponding node and switch to full file view.
* Click the title bar to minimize the file or show its snippets.
* Click the snippet button to switch to snippet or full file view, depending on the file node
* Click the maximize button to switch to [Single File Mode](#single-file-mode).

#### Snippets

A code snippet contains the lines of interest for the currently active symbol surrounded by some more lines to provide some context. Other symbols that were indexed by Sourcetrail are framed by a box when hovered. Here Sourcetrail distinguishes between local symbols and symbols that can be related to any other part of the code base. In case the snippet is part of a class, function or namespace, an additional line at the top of the snippet provides information about the snippet’s context (e.g. the surrounding scope).

!["Code View Snippet"](img/code_view_snippet.png "Code View Snippet")

**Interactions:**

* Click the top line to show the whole scope around the snippet.
* Click a boxed symbol to activate it.
* Click a boxed local symbol to highlight all its usages in the visible code.

### Single File Mode

In single file mode you will only every have one file visible at a time. The first file shown is usually the file containing the definition of the active snippet if available. Other than that the user interface is the same as in [Snippet List Mode](#snippet-list-mode).

!["Code View Single"](img/code_view_single.png "Code View Single")

**Interactions:**

* Hover the title to see the full file path.
* Click the title to activate the file's corresponding node.
* Click the snippet button to switch to [Snippet List Mode](#snippet-list-mode).

## Search View

The Search View contains the search field and some other related user interface elements.

!["Search View"](img/search_view.png "Search View")

### Back, Forward and History

The left `Backward` button lets you undo your last navigation actions (see [Back](#back)) and the right `Forward` button lets you redo your undone navigation actions again (see [Forward](#forward)). Both buttons are only enabled when the respective actions are available at the moment.

The middle button shows a list of the recently active symbol stack. Select a symbol to activate it.

!["Undo Redo View"](img/undo_redo_buttons.png "Undo Redo View")
!["History List"](img/history_list.png "History List")

**Interactions:**

* Hover the buttons to see a tool tip.
* Press the buttons to execute the respective action.
* Press the history button to show the active symbol stack and click on an item to activate it.

### Refresh

The refresh button allows you to refresh the current project and reindex all updated, added and removed files. To reindex the whole project choose the **Force Refresh** option from the [Edit Menu](#edit).

!["Refresh Button"](img/refresh_button.png "Refresh Button")

**Interactions:**

* Hover the buttons to see a tooltip.
* Press the refresh button to refresh the project.

### Overview Button

Show the overview screen, which gives a summary of the loaded project. The overview screen is shown after the project was loaded. Alternatively use the shortcut [To overview](#shortcuts).

!["Overview Button"](img/overview_button.png "Overview Button")

**Interactions:**

* Press the overview button to show the project overview.

### Search Bar

The search bar allows you to enter search requests to find one of Sourcetrail's indexed symbols. It doesn't allow for full text searching across all files so far. The search field allows for most text editing interactions common to text fields. When typing your request the [Autocompletion Popup](#autocompletion-popup) will show you search results matching to your entered string.

!["Search Bar"](img/search_bar.png "Search Bar")

**Interactions:**

* Focus the search field by clicking it or using the [Find Symbol](#find-symbol) action.
* Enter your search request by typing on your keyboard.
* By pressing enter or clicking on the search icon on the right you send your request.
* The search field allows for most interactions known from other text fields such as moving the cursor, copy&paste and text selection.


### Autocompletion Popup

The Autocompletion Popup displays all [Nodes](#nodes) matching your search request within all indexed symbols. The match results are determined by a fuzzy matching algorithm, that allows you to skip characters. The popup shows which characters in the words are matching and displays their corresponding node color. The node type is displayed on the right.

!["Search View Completion"](img/search_view_completion.png "Search View Completion")

**Interactions:**

* Use the up and down arrow keys to switch between search results.
* Pressing tab or clicking on the search result will insert it into the search field.
* Pressing enter will select the search result and send the search request.

### Keywords

Additionally the search view provides specific keywords that select a certain group of symbols.

| keyword | effect
| --- | ---
| **overview** | Shows an overview of all indexed symbols in the [graph view](#graph-view) and some statistics in the [code view](#code-view).
| **error** | Shows all errors in the [code view]().

### Full text search

Search for a certain string in all indexed files by putting `?` at the front of your search query. The default full text search is case-insensitive, use `??` to search case-sensitive.

!["Search View Fulltext"](img/search_view_fulltext.png "Search View Fulltext")

**Interactions:**

* Start a query with `?` or use the [Find Text](#find-text) action to do a case-insensitive full text search.
* Start a query with `??` to do a case-sensitive full text search.

### Bookmarking Buttons

The `Bookmark Active Symbol` button on the left opens the [Bookmark Creator](#bookmark-creator) to create a new bookmark. The `Bookmark Manager` button on the right is used to display the [Bookmark Manager](#bookmark-manager) for activating and editing your bookmarks.

!["Bookmark Buttons"](img/bookmark_buttons.png "Bookmark Buttons")

**Interactions:**

* Hover the buttons to see a tool tip.
* Press the buttons to execute the respective action.

### Bookmark Creator

Use the `Bookmark Creator` to create or edit bookmarks.

!["Bookmark Creator"](img/bookmark_creator.png "Bookmark Creator")

| Setting | Description
| --- | ---
| **Name** | The name of the bookmark. Initially the name of the node or edge is used.
| **Comment** | Add an optional comment to the bookmark.
| **Category** | Add the bookmark to a certain category. Bookmarks with the same category are grouped together in the [Bookmark Manager](#bookmark-manager).

**Interactions:**

* Press `Cancel` to close without changes.
* Press `Create/Save` to save the bookmark or apply the changes.

### Bookmark Manager

Use the `Bookmark Manager` to view and activate your bookmarks. Bookmarks are displayed as lines below their respective category. If a bookmark does not have a category it will be placed within the `default` category. The buttons for removing/editing categories or bookmarks are only visible when hovering the respective line. Bookmark information is stored within a separate `.srctrlbm` file next to your `.srctrlprj` project file.

!["Bookmark Manager"](img/bookmark_manager.png "Bookmark Manager")

**Interactions:**

* Activate bookmarks by clicking on the name.
* Open/Collapse the bookmark comment by clicking within the bookmark line.
* Click the `Edit` button to change the contents of the bookmark.
* Click the `Delete` button at a bookmark to remove the bookmark.
* Open/Collapse categories by clicking in their line.
* Click the `Delete` button at a category to remove the category and all bookmarks within.
* Change the `Show` filter to switch between display of nodes and/or edges.
* Change the `Sorting` to change the order of bookmarks within their categories.

## Status View

This view provides different tabs with information about your project. This
view is hidden by default.

**Interactions:**

* Click on the titles on top to switch between tabs.
* Click on the `x`-button in the top right corner to close the Status View.

### Status Tab

This table gives some information about status updates while running Sourcetrail. It can be helpful to figure out why something does not the way it's expected to.

!["Status View Status"](img/status_view_status.png "Status View Status")

**Interactions:**

* Double click on a table cell to select the text for copy&paste.
* Use the checkboxes below to filter the shown messages by type.
* Click on `Clear Table` to remove all rows from the table.

### Errors Tab

This list shows errors occurred during indexing.

!["Status View Error"](img/status_view_error.png "Status View Error")

The following information is provided:

* **Type:** ERROR or FATAL. A FATAL error causes lots of missing information since the indexer had to stop at this error.
* **Error message**
* **File**
* **Line number**
* **Indexed:** Whether the file is within the indexed files.
* **Translation Unit:** The source file that produced this error while being indexed.

**Interactions:**

* Click on a error line to see the location of the error in the [Code View](#code-view).
* Click on the column headers to sort the error rows ascending or descending by this data.
* Double click on a table cell to select the text for copy&paste.
* Use the checkboxes below to filter the shown errors by certain criteria.
* Click on `Edit Project` to open the [Edit Project Dialog](#project-setup-wizard).

## Tooltips

Show information about hovered symbols in the [Graph View](#graph-view) and [Code View](#code-view)

!["Tooltip"](img/tooltip.png "Tooltip")

**The following information is provided:**

* Symbol type
* Visibility (e.g. public or private)
* Reference count
* Symbol name
* Clickable type name for global variables and fields.
* Full signatures with clickable return type name and parameter types names for functions and methods.

**Interactions:**

* Click on symbol names to activate them.
