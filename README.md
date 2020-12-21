# BoilerPlate Repository for developing audio plugins with JUCE & CMake & Visual Studio Code

## Requirements

- JUCE >= 6.0.0 (supports CMake after v6.)
- CMake >= 3.15
- Visual Studio Code

Also, clangd a language server for C++ is highly recommended. In macOS, you can install with `brew install llvm`.

Ninja is also recommended for fast build (will be used automatically if present in this repository. You can change priority of generators in `cmake.preferredGenerators` in workspace setting).

### Recommended Extentions for vscode

- [cpptools](https://github.com/microsoft/vscode-cpptools) (basic language supports for C++ development)
- CMake (CMake language supports)
- [CMake Tools](https://github.com/microsoft/vscode-cmake-tools) (Advanced Integration for using CMake in VScode with GUI)
- [CodeLLDB](https://marketplace.visualstudio.com/items?itemName=vadimcn.vscode-lldb) (better debugger than built-in gdb)
- [clangd](https://marketplace.visualstudio.com/items?itemName=llvm-vs-code-extensions.vscode-clangd) (Advanced intellisense support and formatter powered by llvm)

## Getting Started

### macOS

Install Xcode and type `xcode-select --install` in terminal.
open `~/.zshrc` and add `export SDKROOT="$(xcrun --sdk macosx --show-sdk-path)"` in the last line of the file.

### Windows

Install Visual Studio.

### Setup - common

Clone this repository. 

```sh
git clone https://github.com/tomoyanonymous/juce_cmake_vscode_example --recursive
```

Open `juce_cmake_vscode_example.code-workspace` with Visual Studio Code.
If recommended extensions are not fully installed, notification to install them will come up.

If CMake Tools is correctly installed, you will be asked which CMake Kits(compiler) you want to use. 

In macOS, choose `Clang x.x.x` which point to `/usr/bin/clang++` (clang provided by xcode. of course you can choose other compilers if you have).

In Windows, choose `Visual Studio Community 2019 Release - amd64`, you will have choices of architectures(like amd64/x86-amd64).

### Build

Open CMake Menu on your left sidebar (it will show up if CMake Tools is installed).

Click "Configure All". This will take time at first time to build juceaide, an internal build tool by juce.

Click "Build All Projects".

### Debug

### Debug StandAlone

If successfully built, right click JUCE_CMAKE_EXAMPLE/src/ExamplePlugin_Standalone and select "set as Debug/Launch Target".

Open Debug Menu in left Sidebar. And click Run button on the left in a menu of CMake Debug(workspace). Standalone version of your plugin will be launched.

### Debug Plugin using AudioPluginHost

You can debug VST Plugin using AudioPluginHost, an utility tool & demo app provided by JUCE.

You need to configure JUCE with special argument `JUCE_BUILD_EXTRAS`. In this example, you can enable it by uncommenting `juce_cmake-vscode_example.code-workspace` like below.

```json
        "cmake.configureArgs": [
            // if you want to build AAX, set PATH for SDK here.
            //  "-DAAX_SDK_PATH="
            // if you want to build AudioPluginHost to Test VST Plugin, uncomment this.
            "-DJUCE_BUILD_EXTRAS=ON"
        ],
```

Also, you need to set `COPY_PLUGIN_AFTER_BUILD` to `TRUE` in `juce_add_plugin` in CMakeLists.txt.
This requires administrator permission when copy plugins into appropriate folder(You can do this by opening VSCode from right-click menu "run as administrator").

Now, you can see `JUCE/extras/AudioPluginHost` target in build tree after configure step. 
Build it and select "Set as Debug/Launch Target" in right-click menu.

Open Debug Menu in left Sidebar. And click Run button on the left in a menu of CMake Debug(workspace). 

AudioPluginHost will be launched. You can see your plugin in "Plugins" menu.

---

(Note that you can also debug from "Debug" button in right-click menu of CMake Tools but you cannot use CodeLLDB debugger in this case.)

## Resources

[JUCE CMake API Documents](https://github.com/juce-framework/JUCE/blob/master/docs/CMake%20API.md)

[sudara/pamplejuce](https://github.com/sudara/pamplejuce/) another great template repository for developing JUCE with CMake + Catch2 + GIthub Actions + C++20

## License

(c) Tomoya Matsuura https://matsuuratomoya.com

---

All of source codes included in this repository are published under MIT License.

Permission is hereby granted, free of charge, to any person obtaining a copy of this software and associated documentation files (the "Software"), to deal in the Software without restriction, including without limitation the rights to use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies of the Software, and to permit persons to whom the Software is furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.

---

<a rel="license" href="http://creativecommons.org/licenses/by/4.0/"><img alt="Creative Commons License" style="border-width:0" src="https://i.creativecommons.org/l/by/4.0/88x31.png" /></a><br />All of documents included in this repositry are published under <a rel="license" href="http://creativecommons.org/licenses/by/4.0/">Creative Commons Attribution 4.0 International License</a>.
