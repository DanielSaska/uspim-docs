# Obtaining μSPIM source code
All source code is available through git. The MicroManager plugin is available from the [https://github.com/DanielSaska/uspim-mm](https://github.com/DanielSaska/uspim-mm) repository and the control server executable is available from the [https://github.com/DanielSaska/uspim-ctrl](https://github.com/DanielSaska/uspim-ctrl).

# Compiling μSPIM MicroManager Plugin
First, make a local copy of the source code, either using `git clone https://github.com/DanielSaska/uspim-mm` or downloading directly from the GitHub repository.

Similarly to to the defualt distribution of MicroManager, the μSPIM Plugin uses Java 6. You will therefore need JDK6 (jdk-6u45-windows-x64.exe) which can be obtained directly from official Oracle website ([https://www.oracle.com/java/technologies/javase-java-archive-javase6-downloads.html](https://www.oracle.com/java/technologies/javase-java-archive-javase6-downloads.html)) or a number of mirrors, for example Huawei Cloud: [https://mirrors.huaweicloud.com/java/jdk/6u45-b06/](https://mirrors.huaweicloud.com/java/jdk/6u45-b06/). Ensure that the `JAVA_HOME` system variable points to the correct JDK prior to compilation.

You will also need Gradle 2 available from the Gradle website ([https://gradle.org/releases/](https://gradle.org/releases/)). Gradle 2.14.1 was tested to work. Ensure that your `Path` system variable contains the `bin` directory inside your Gradle installation.

After both build tools are set up correctly, the μSPIM Plugin can be compiled by running `gradle jar` to build the plugin jar or `gradle deploy` to deploy the plugin jar directly into the `C:/Program Files/Micro-Manager-1.4/mmplugins` folder.

# Compiling μSPIM Control executable
Make a local copy of the source code, either using `git clone https://github.com/DanielSaska/uspim-ctrl` or downloading directly from the GitHub repository.

[Visual Studio](https://visualstudio.microsoft.com/) is needed for the compilation of the C++ control executable.

The only dependency of the control executable is the National Instruments DAQ library which is available from the official website ([https://www.ni.com/en-gb/support/downloads/drivers/download.ni-daqmx.html#348669](https://www.ni.com/en-gb/support/downloads/drivers/download.ni-daqmx.html#348669)). During installation, ensure that at least *NI-DAQmx Support for C* is selected.

Before compilation, it is important to modify the *Target Platform* and *Platform Toolset*. By default, this is *10.0* and *v141*, respective, as we compiled the project with Visual Studio 2019. Selecting available target platform and toolset will allow compilation on different operating system versions and versions of the windows C++ compiler. The compilation process is standard from then on. For development, select the Debug configuration, for usage, use the Release configuration.
