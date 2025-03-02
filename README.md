# Embedded Software Framework

This repositoty is used for the vast embedded software developers.

## What it is

It provides a template framework to create your code with the out-of-box settings of kbuild and many other famous and nessary tools in the embedded software development.
You can easily use it as the basic framework for your project and code especially there are many engineers who has different styles in your project.

## How to use it

First of all, you need to click the button "Use the template" at the top right corner to create your own repository bases on this template, or you can clone this repository, they are same.

> Using template or clone the code may keep the history commits of this repository, and you may don't want these commits pollute your new project.
> Another way is that you can download with the zip file, and it will don't include any git information.

Next step, you can do some customization.

**Clang-Format**

The repository already contains a set of clang-format (`.clang-format`) and configuration templates.
If you want to use them, you can customize them and use your favorite configurations.

**Doxygen**

The repository already contains a set of doxygen (`.doxyfile`) configuration templates.
If you want to enable doxygen, please remember to modify the `PROJECT-NAME` option in the  `.doxyfile`. It is now empty and you should change it to the loud name of your new project.

**Devcontainer**

If you want to use a container as the development environment, you can modify the files in the `.devcontainer` folder according to the actual situation.

**VS Code**

The repository includes some configuration of VS Code and VS Code plugins.
They are defined in folder `.vscode`.
We have defined three sample tasks of VS Code to do the `make defconfig`, `make` and `make clean`, you can see them and run via `ctrl` + `shifp` + `B`.

**Git**

I have tried my bese to define a complete git ignore file including most of all files which needs to be ignored in a C/C++ project.
Please check the file `.gitignore`, if there are some omissions or mistakes, you can fix it.

I also defined a `.gitattributes` file and fixed the eol format with LF, if you work in Windows, you can also change it.

**Kbuild**

Last, and also the most importance, the repository intergrated a kbuild system, the build framework is being used in Linux kernel.

> The kbuild system was transported by [Ole Reinhardt](https://github.com/olereinhardt) in repository [kbuild-template](https://github.com/embedded-it/kbuild-template).
> Thanks for his work!
