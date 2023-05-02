cmake_minimum_required(VERSION 3.15)

project(control_clock LANGUAGES C CXX ASM)

find_bsp(
	ID com.sysprogs.arm.stm32
	VERSION 2022.01
	MCU STM32F413ZH
	HWREGISTER_LIST_FILE STM32F4xxxx/DeviceDefinitions/stm32f413xx.xml
	DISABLE_GNU_EXTENSIONS)

file(GLOB HAL_SOURCES "${PROJECT_SOURCE_DIR}/Drivers/STM32F4xx_HAL_Driver/Src/*.c")
file(GLOB HAL_HEADERS "${PROJECT_SOURCE_DIR}/Drivers/STM32F4xx_HAL_Driver/Inc/*.h")
file(GLOB CONF_SOURCES "${PROJECT_SOURCE_DIR}/Core/Src/*.c")
file(GLOB CONF_HEADERS "${PROJECT_SOURCE_DIR}/Core/Inc/*.h")

add_bsp_based_executable(
	    NAME control_clock
	    SOURCES 
		main.c
		"${HAL_HEADERS}" 
		"${HAL_SOURCES}" 
		"${CONF_HEADERS}" 
		"${CONF_SOURCES}" 
		"${PROJECT_SOURCE_DIR}/startup_stm32f413zhtx.s"
	    GENERATE_BIN
	    GENERATE_MAP
	    LINKER_SCRIPT ${PROJECT_SOURCE_DIR}/STM32F413ZHTX.ld)