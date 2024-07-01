# Unreal 5.4: Downloading and Installing Plugin

There have been multiple implementations of ink runtimes and API for Unreal over the last several years, but the current recommended plugin
is named [InkPot](https://github.com/The-Chinese-Room/Inkpot).

Per the instructions for InkPot on its GitHub repository, installation requires copying and pasting the [InkPot release](https://github.com/The-Chinese-Room/Inkpot/releases/tag/v1.02.21-release) into the project folder of an existing Unreal project.

Before attempting to open the project make sure of the following:

Windows:

- **Visual Studio 2022 is installed**. After installation, modify the components and add the following, depending on the Unreal version in use:

- All: .NET 5.0 Runtime (Out of support)
- 5.3:
  - MSVC v143 - VS Code 2022 C++ ... (v14.34-17.4)
  - C++/CLI support for v143 build tools (14.34-17.4)
- 5.4:
  - MSVC v143 - VS Code 2022 C++ ... (v14.38-17.8)
  - C++/CLI support for v143 build tools (14.38-17.8)

macOS:

- Visual Studio for Mac will be discontinued in August 2024 and XCode support has not been added yet.

Installation can be confirmed by opening the project. During this process, Unreal will signal it needs to compile the source code. ClickOK and wait for the compilation to finish.
