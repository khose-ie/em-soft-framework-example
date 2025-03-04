#
# USER CONFIGURATION VARIABLE
#
BSP_PATH    ?= libs/STMicroelectronics/bsp
CMSIS_PATH  ?= libs/STMicroelectronics/cmsis
DRIVER_PATH ?= libs/STMicroelectronics/driver

# CPU
CPU = $(if $(CONFIG_CPU_SERIES_STM32F1XX), -mcpu=cortex-m3)  \
      $(if $(CONFIG_CPU_SERIES_STM32F4XX), -mcpu=cortex-m4)  \
      $(if $(CONFIG_CPU_SERIES_STM32F7XX), -mcpu=cortex-m4)  \
      $(if $(CONFIG_CPU_SERIES_STM32H5XX), -mcpu=cortex-m33) \
      $(if $(CONFIG_CPU_SERIES_STM32H7XX), -mcpu=cortex-m7)

# FPU
FPU = -mfpu=fpv4-sp-d16

# Float-ABI
FLOAT_ABI = -mfloat-abi=hard

# MCU
MCU = $(CPU) -mthumb $(FPU) $(FLOAT_ABI)

# MCU Define
MCU_DEFS  = -DUSE_HAL_DRIVER
MCU_DEFS += $(if $(CONFIG_CPU_SERIES_STM32F1XX), $(if $(CONFIG_CPU_MODEL_STM32F100XB),  -DSTM32F100xB) \
                                                 $(if $(CONFIG_CPU_MODEL_STM32F100XE),  -DSTM32F100xE) \
                                                 $(if $(CONFIG_CPU_MODEL_STM32F101X6),  -DSTM32F101x6) \
                                                 $(if $(CONFIG_CPU_MODEL_STM32F101XB),  -DSTM32F101xB) \
                                                 $(if $(CONFIG_CPU_MODEL_STM32F101XE),  -DSTM32F101xE) \
                                                 $(if $(CONFIG_CPU_MODEL_STM32F101XG),  -DSTM32F101xG) \
                                                 $(if $(CONFIG_CPU_MODEL_STM32F102X6),  -DSTM32F102x6) \
                                                 $(if $(CONFIG_CPU_MODEL_STM32F102XB),  -DSTM32F102xB) \
                                                 $(if $(CONFIG_CPU_MODEL_STM32F103X6),  -DSTM32F103x6) \
                                                 $(if $(CONFIG_CPU_MODEL_STM32F103XB),  -DSTM32F103xB) \
                                                 $(if $(CONFIG_CPU_MODEL_STM32F103XE),  -DSTM32F103xE) \
                                                 $(if $(CONFIG_CPU_MODEL_STM32F103XG),  -DSTM32F103xG) \
                                                 $(if $(CONFIG_CPU_MODEL_STM32F105XC),  -DSTM32F105xC) \
                                                 $(if $(CONFIG_CPU_MODEL_STM32F107XC),  -DSTM32F107xC) ) \
            $(if $(CONFIG_CPU_SERIES_STM32F4XX), $(if $(CONFIG_CPU_MODEL_STM32F401XC),  -DSTM32F401xC) \
                                                 $(if $(CONFIG_CPU_MODEL_STM32F401XE),  -DSTM32F401xE) \
                                                 $(if $(CONFIG_CPU_MODEL_STM32F405XX),  -DSTM32F405xx) \
                                                 $(if $(CONFIG_CPU_MODEL_STM32F407XX),  -DSTM32F407xx) \
                                                 $(if $(CONFIG_CPU_MODEL_STM32F410CX),  -DSTM32F410Cx) \
                                                 $(if $(CONFIG_CPU_MODEL_STM32F410RX),  -DSTM32F410Rx) \
                                                 $(if $(CONFIG_CPU_MODEL_STM32F410TX),  -DSTM32F410Tx) \
                                                 $(if $(CONFIG_CPU_MODEL_STM32F411XE),  -DSTM32F411xE) \
                                                 $(if $(CONFIG_CPU_MODEL_STM32F412CX),  -DSTM32F412Cx) \
                                                 $(if $(CONFIG_CPU_MODEL_STM32F412RX),  -DSTM32F412Rx) \
                                                 $(if $(CONFIG_CPU_MODEL_STM32F412VX),  -DSTM32F412Vx) \
                                                 $(if $(CONFIG_CPU_MODEL_STM32F412ZX),  -DSTM32F412Zx) \
                                                 $(if $(CONFIG_CPU_MODEL_STM32F413XX),  -DSTM32F413xx) \
                                                 $(if $(CONFIG_CPU_MODEL_STM32F415XX),  -DSTM32F415xx) \
                                                 $(if $(CONFIG_CPU_MODEL_STM32F417XX),  -DSTM32F417xx) \
                                                 $(if $(CONFIG_CPU_MODEL_STM32F423XX),  -DSTM32F423xx) \
                                                 $(if $(CONFIG_CPU_MODEL_STM32F427XX),  -DSTM32F427xx) \
                                                 $(if $(CONFIG_CPU_MODEL_STM32F429XX),  -DSTM32F429xx) \
                                                 $(if $(CONFIG_CPU_MODEL_STM32F437XX),  -DSTM32F437xx) \
                                                 $(if $(CONFIG_CPU_MODEL_STM32F439XX),  -DSTM32F439xx) \
                                                 $(if $(CONFIG_CPU_MODEL_STM32F446XX),  -DSTM32F446xx) \
                                                 $(if $(CONFIG_CPU_MODEL_STM32F469XX),  -DSTM32F469xx) \
                                                 $(if $(CONFIG_CPU_MODEL_STM32F479XX),  -DSTM32F479xx) ) \
            $(if $(CONFIG_CPU_SERIES_STM32F7XX), $(if $(CONFIG_CPU_MODEL_STM32F722XX),  -DSTM32F722xx) \
                                                 $(if $(CONFIG_CPU_MODEL_STM32F723XX),  -DSTM32F723xx) \
                                                 $(if $(CONFIG_CPU_MODEL_STM32F730XX),  -DSTM32F730xx) \
                                                 $(if $(CONFIG_CPU_MODEL_STM32F732XX),  -DSTM32F732xx) \
                                                 $(if $(CONFIG_CPU_MODEL_STM32F733XX),  -DSTM32F733xx) \
                                                 $(if $(CONFIG_CPU_MODEL_STM32F745XX),  -DSTM32F745xx) \
                                                 $(if $(CONFIG_CPU_MODEL_STM32F746XX),  -DSTM32F746xx) \
                                                 $(if $(CONFIG_CPU_MODEL_STM32F750XX),  -DSTM32F750xx) \
                                                 $(if $(CONFIG_CPU_MODEL_STM32F756XX),  -DSTM32F756xx) \
                                                 $(if $(CONFIG_CPU_MODEL_STM32F765XX),  -DSTM32F765xx) \
                                                 $(if $(CONFIG_CPU_MODEL_STM32F767XX),  -DSTM32F767xx) \
                                                 $(if $(CONFIG_CPU_MODEL_STM32F769XX),  -DSTM32F769xx) \
                                                 $(if $(CONFIG_CPU_MODEL_STM32F777XX),  -DSTM32F777xx) \
                                                 $(if $(CONFIG_CPU_MODEL_STM32F779XX),  -DSTM32F779xx) ) \
            $(if $(CONFIG_CPU_SERIES_STM32H5XX), $(if $(CONFIG_CPU_MODEL_STM32H503XX),  -DSTM32H503xx) \
                                                 $(if $(CONFIG_CPU_MODEL_STM32H523XX),  -DSTM32H523xx) \
                                                 $(if $(CONFIG_CPU_MODEL_STM32H533XX),  -DSTM32H533xx) \
                                                 $(if $(CONFIG_CPU_MODEL_STM32H562XX),  -DSTM32H562xx) \
                                                 $(if $(CONFIG_CPU_MODEL_STM32H563XX),  -DSTM32H563xx) \
                                                 $(if $(CONFIG_CPU_MODEL_STM32H573XX),  -DSTM32H573xx) ) \
            $(if $(CONFIG_CPU_SERIES_STM32H7XX), $(if $(CONFIG_CPU_MODEL_STM32H723XX),  -DSTM32H723xx) \
                                                 $(if $(CONFIG_CPU_MODEL_STM32H725XX),  -DSTM32H725xx) \
                                                 $(if $(CONFIG_CPU_MODEL_STM32H730XX),  -DSTM32H730xx) \
                                                 $(if $(CONFIG_CPU_MODEL_STM32H730XXQ), -DSTM32H730xxQ)\
                                                 $(if $(CONFIG_CPU_MODEL_STM32H733XX),  -DSTM32H733xx) \
                                                 $(if $(CONFIG_CPU_MODEL_STM32H735XX),  -DSTM32H735xx) \
                                                 $(if $(CONFIG_CPU_MODEL_STM32H742XX),  -DSTM32H742xx) \
                                                 $(if $(CONFIG_CPU_MODEL_STM32H743XX),  -DSTM32H743xx) \
                                                 $(if $(CONFIG_CPU_MODEL_STM32H745XG),  -DSTM32H745xG) \
                                                 $(if $(CONFIG_CPU_MODEL_STM32H745XX),  -DSTM32H745xx) \
                                                 $(if $(CONFIG_CPU_MODEL_STM32H747XG),  -DSTM32H747xG) \
                                                 $(if $(CONFIG_CPU_MODEL_STM32H747XX),  -DSTM32H747xx) \
                                                 $(if $(CONFIG_CPU_MODEL_STM32H750XX),  -DSTM32H750xx) \
                                                 $(if $(CONFIG_CPU_MODEL_STM32H753XX),  -DSTM32H753xx) \
                                                 $(if $(CONFIG_CPU_MODEL_STM32H755XX),  -DSTM32H755xx) \
                                                 $(if $(CONFIG_CPU_MODEL_STM32H757XX),  -DSTM32H757xx) \
                                                 $(if $(CONFIG_CPU_MODEL_STM32H7A3XX),  -DSTM32H7A3xx) \
                                                 $(if $(CONFIG_CPU_MODEL_STM32H7A3XXQ), -DSTM32H7A3xxQ)\
                                                 $(if $(CONFIG_CPU_MODEL_STM32H7B0XX),  -DSTM32H7B0xx) \
                                                 $(if $(CONFIG_CPU_MODEL_STM32H7B0XXQ), -DSTM32H7B0xxQ)\
                                                 $(if $(CONFIG_CPU_MODEL_STM32H7B3XX),  -DSTM32H7B3xx) \
                                                 $(if $(CONFIG_CPU_MODEL_STM32H7B3XXq), -DSTM32H7B3xxQ)) \

# MCU C Flags
KBUILD_CFLAGS   += $(MCU) \
                   $(MCU_DEFS) \
                   -fdata-sections \
                   -ffunction-sections

# MCU C++ Flags
KBUILD_CXXFLAGS += $(MCU) \
                   $(MCU_DEFS) \
                   -fdata-sections \
                   -ffunction-sections

# MCU A Flags
KBUILD_AFLAGS   += $(MCU) \
                   $(MCU_DEFS) \

# MCU Linker Flags
KBUILD_LDFLAGS  += $(MCU) \
                   -T$(srctree)/.FLASH.o.ld \
                   -specs=nano.specs \
                   -lc -lm -lnosys

# STM32 Common CMSIS Includes
APPINCLUDE += -I$(srctree)/$(CMSIS_PATH)/cmsis-core/Include \
              -I$(srctree)/$(CMSIS_PATH)/cmsis-core/RTOS2/Include

# MCU Includes
APPINCLUDE += $(if $(CONFIG_CPU_SERIES_STM32F1XX), -I$(srctree)/$(CMSIS_PATH)/cmsis-device-f1/Include \
                                                   -I$(srctree)/$(DRIVER_PATH)/stm32f1xx-hal-driver/Inc \
                                                   -I$(srctree)/$(DRIVER_PATH)/stm32f1xx-hal-driver/Inc/Legacy) \
              $(if $(CONFIG_CPU_SERIES_STM32F4XX), -I$(srctree)/$(CMSIS_PATH)/cmsis-device-f4/Include \
                                                   -I$(srctree)/$(DRIVER_PATH)/stm32f4xx-hal-driver/Inc \
                                                   -I$(srctree)/$(DRIVER_PATH)/stm32f4xx-hal-driver/Inc/Legacy) \
              $(if $(CONFIG_CPU_SERIES_STM32F7XX), -I$(srctree)/$(CMSIS_PATH)/cmsis-device-f7/Include \
                                                   -I$(srctree)/$(DRIVER_PATH)/stm32f7xx-hal-driver/Inc \
                                                   -I$(srctree)/$(DRIVER_PATH)/stm32f7xx-hal-driver/Inc/Legacy) \
              $(if $(CONFIG_CPU_SERIES_STM32H5XX), -I$(srctree)/$(CMSIS_PATH)/cmsis-device-h5/Include \
                                                   -I$(srctree)/$(DRIVER_PATH)/stm32h5xx-hal-driver/Inc \
                                                   -I$(srctree)/$(DRIVER_PATH)/stm32h5xx-hal-driver/Inc/Legacy) \
              $(if $(CONFIG_CPU_SERIES_STM32H7XX), -I$(srctree)/$(CMSIS_PATH)/cmsis-device-h7/Include \
                                                   -I$(srctree)/$(DRIVER_PATH)/stm32h7xx-hal-driver/Inc \
                                                   -I$(srctree)/$(DRIVER_PATH)/stm32h7xx-hal-driver/Inc/Legacy)
