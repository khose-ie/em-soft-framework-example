# Embedded Software Framework Example

This is an emample that I will tell you here how to use the em-soft-framework to create an kbuild based code repository for ARM STM32 series environment.



The following are steps that I create this repository, you can follow them and see the details what I modified in the git commits.



Use the ST official NUCLEO-H563ZI evaluation board as the example.



**Clone or use the template**



The first step is to clone the tempate repository, you can open it in the [Github Website](https://github.com/khose-ie/em-soft-framework.git), and click the button `Use this template` in the top-right corner.

That will create your own repository with the current edition of the [em-soft-framework](https://github.com/khose-ie/em-soft-framework.git) and Github will generate all of these code an initial commit.



If you want to keep the historical commits of the template repository, you can use the `fork` button to fork a duplication of this repository and start with it.



If you don't want to generate a repository in Github, you can clone the repository with Git CLI in you local PC, or download it with a .zip file.



**Add the support of STM32**



> Commit Hash: 2353564332a6f2ccc9dab59c78e1040db42be569



Now, you should add the support of STM32, we have a repository, that has compile the environment settings for STM32. You can download the `Kconfig` file and the `Makefile` of it, and add them to your repository.



You should add these two files to the path `arch/arm/mach-stm32`, so you need to make it first.



```shell
mkdir -p arch/arm/mach-stm
```



Then, download these two files and put them into the new folder.



**Initialize the cmsis and driver** 



>  Commit Hash: 0cdb1b2eda71bc20552409002cca1753aacd7ce1



Now, you need to import and initialize the STM32H5 related official repositories.

We plan to save them in the path `libs/STMicroelectronics`, so I need to create it first.



```shell
mkdir -p libs/STMicroelectronics
```



I plan to divide the path into 3 sub folders `bsp`, `cmsis`, `driver`.



```shell
mkdir -p libs/STMicroelectronics/bsp
mkdir -p libs/STMicroelectronics/cmsis
mkdir -p libs/STMicroelectronics/driver
```



And now, we can import the official repositories as the submodules.

First, you should import the `cmsis-core`, it is the common repository for ST's cmsis implementation.



```shell
git submodule add --name cmsis-core https://github.com/STMicroelectronics/cmsis-core.git libs/STMicroelectronics/cmsis/cmsis-core
```



Second, you should import STM32H5 series cmsis repository.



```shell
git submodule add --name cmsis-device-h5 https://github.com/STMicroelectronics/cmsis-device-h5.git libs/STMicroelectronics/cmsis/cmsis-device-h5
```



Third, import the STM32H5 series HAL driver.



```shell
git submodule add --name stm32h5xx-hal-driver https://github.com/STMicroelectronics/stm32h5xx-hal-driver.git libs/STMicroelectronics/driver/stm32h5xx-hal-driver
```



Last, don't forget to ignore the changes for these repositories.



```shell
git config submodule.cmsis-core.ignore all
git config submodule.cmsis-device-h5.ignore all
git config submodule.stm32h5xx-hal-driver.ignore all
```



The NUCLEO-H563ZI evalucation board needs some BSP code from ST, so we will import them here. If you don't use ST official evaluation board and don't reference the ST official BSP code, you can skip the step.



We add the ST official BSP repository as the submodule in our repository.

Please note we don't only need to import the bsp for NUCLEO-H563ZI, but also the ST common bsp code.





```shell
git submodule add --name stm32-bsp-common https://github.com/STMicroelectronics/stm32-bsp-common.git libs/STMicroelectronics/bsp/common
git submodule add --name stm32-bsp-stm32h5xx-nucleo https://github.com/STMicroelectronics/stm32h5xx-nucleo-bsp.git libs/STMicroelectronics/bsp/stm32h5xx-nucleo
```



Ignore the changes.



```shell
git config submodule.stm32-bsp-common.ignore all
git config submodule.stm32-bsp-stm32h5xx-nucleo.ignore all
```



**Import your platform code**



> Commit Hash: cb969636a21d3739811d855c488b29666d820c13



OK, at this stage, you can import your platform code.

You can generate them by STM32CubeMX.



Please open your STM32CubeMX and select the NUCLEO-H563ZI board in `Board Selector` button.



* Without TrustZone.
* Generate demonstration code.



Enable the 2ways ICACHE.



Enter the `Project Manager` panel, fill in the settings and choice `CMake` in `Toolchain / IDE` (you can also choice any other options).



And than select `Code Generator` in the left dock, select the following.



* Add necessary library files as reference in the toolchain project configuration file
* Generate peripheral initialization as a pair of '.c/.h' file per peripheral
* Keep User Code when re-generating
* Delete previously generated files when note re-generated



Now, save the project file and generate the code.



We plan to put the generated code in path `platform/stm`, so I create the path.



```shell
mkdir -p platform/stm/nucleo-h563zi
```



And then, copy all generated files to this folder.



**Create the structure makefile**



> Commit Hash: 2ad7c5f82a0c53e89d666e193887e96f7abc68bb



This is the key step, we need to make the makefile can compile the files we imported in the last steps.



Create a Makefile file in `platform` and add following.



```makefile
obj-y += stm/
```



Create a Makefile file in `platform/stm` and add following.



```makefile
obj-y += stm/nucleo-h563zi/
```



Create a Makefile file in `platform/stm/nucleo-h563zi` and add the files according to the CMake generate by STM32CubeMX.

You need to read the file `platform/stm/nucleo-h563zi/cmake/stm32cubemx/CMakeLists.txt` and check the included path and source C file and assmebly file.



Add them to the Makefile as following, please pay attention to the following points.



* The included path should start with `-I$(srctree)` and use the relative path start from the root path of the repository.
* The target files should replace `.c/.s/.ld` to `.o`.
* Please remember to add the linker script `.ld` file to the target object.



```makefile
APPINCLUDE += -I$(srctree)/libs/STMicroelectronics/bsp/stm32h5xx-nucleo \
              -I$(srctree)/platform/stm/nucleo-h563zi/Core/Inc

obj-y += startup_stm32h563xx.o
obj-y += STM32H563xx_FLASH.o
obj-y += Core/Src/main.o
obj-y += Core/Src/stm32h5xx_it.o
obj-y += Core/Src/stm32h5xx_hal_msp.o
obj-y += Core/Src/sysmem.o
obj-y += Core/Src/syscalls.o
obj-y += Core/Src/system_stm32h5xx.o

obj-y += ../../../libs/STMicroelectronics/driver/stm32h5xx-hal-driver/Src/stm32h5xx_hal.o
obj-y += ../../../libs/STMicroelectronics/driver/stm32h5xx-hal-driver/Src/stm32h5xx_hal_cortex.o
obj-y += ../../../libs/STMicroelectronics/driver/stm32h5xx-hal-driver/Src/stm32h5xx_hal_icache.o
obj-y += ../../../libs/STMicroelectronics/driver/stm32h5xx-hal-driver/Src/stm32h5xx_hal_rcc.o
obj-y += ../../../libs/STMicroelectronics/driver/stm32h5xx-hal-driver/Src/stm32h5xx_hal_rcc_ex.o
obj-y += ../../../libs/STMicroelectronics/driver/stm32h5xx-hal-driver/Src/stm32h5xx_hal_flash.o
obj-y += ../../../libs/STMicroelectronics/driver/stm32h5xx-hal-driver/Src/stm32h5xx_hal_flash_ex.o
obj-y += ../../../libs/STMicroelectronics/driver/stm32h5xx-hal-driver/Src/stm32h5xx_hal_gpio.o
obj-y += ../../../libs/STMicroelectronics/driver/stm32h5xx-hal-driver/Src/stm32h5xx_hal_dma.o
obj-y += ../../../libs/STMicroelectronics/driver/stm32h5xx-hal-driver/Src/stm32h5xx_hal_dma_ex.o
obj-y += ../../../libs/STMicroelectronics/driver/stm32h5xx-hal-driver/Src/stm32h5xx_hal_pwr.o
obj-y += ../../../libs/STMicroelectronics/driver/stm32h5xx-hal-driver/Src/stm32h5xx_hal_pwr_ex.o
obj-y += ../../../libs/STMicroelectronics/driver/stm32h5xx-hal-driver/Src/stm32h5xx_hal_exti.o
obj-y += ../../../libs/STMicroelectronics/driver/stm32h5xx-hal-driver/Src/stm32h5xx_hal_usart.o
obj-y += ../../../libs/STMicroelectronics/driver/stm32h5xx-hal-driver/Src/stm32h5xx_hal_usart_ex.o
obj-y += ../../../libs/STMicroelectronics/driver/stm32h5xx-hal-driver/Src/stm32h5xx_hal_uart_ex.o
obj-y += ../../../libs/STMicroelectronics/driver/stm32h5xx-hal-driver/Src/stm32h5xx_hal_uart.o

obj-y += ../../../libs/STMicroelectronics/bsp/stm32h5xx-nucleo.o

```



We have the last stop, delete `main` folder and add `platform` to the Makefile in root path.

Find the `objs-y := main` and replace it by `objs-y := platform`.



You need to fix a small error of the generated code in `platform/stm/nucleo-h563zi/Core/Src/syscalls.c`.

Please add the parameter `void` for the function `initialise_monitor_handles` because in the new version compiler, it must set the parameters even if it is void.



**Compile the code**



OK, well done! Now you can complete your building.



First, try to use the Linux kernel menuconfig to do some configurations.



```shell
make menuconfig
```



* Enter the `Chip architecture and models` and choice `ARM` as the `CPU Arch`.
* Choice `STMicroelectronics` as the `CPU Manufacturer`.
* Choice `STM32H5XX`as the `CPU Series with STMicroelectronics`.
* Choice `STM32H563XX` as the `CPU Model with STMicroelectronics` and exit the menu.
* Enter the `Compile-time checks and options` menu and use `arm` as `Compile target arch`.
* Input `arm-none-eabi-` as `Cross-compiler tool prefix`.
* Exit and save the as the name of `.config`.



Now, you can type `make` to buidl the whole project.



**Save the configuration file**



> Commit Hash: 493653faddd4b51251926c435e26637af07a5216



May you want to save the configuration to use it in the next time.



```shell
make savedefconfig
```



This command will generate a `deconfig` file in the root path. and you need to move it to the `configs` folder.



```shell
mv defconfig configs/example_defconfig
```



When you want to use this configuration files next time, you should make if first before you make, and you don't need to make the `menuconfig` again.



```shell
make example_defconfig
```

