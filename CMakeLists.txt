cmake_minimum_required(VERSION 3.20)

set(MCU_FLAGS
    -mcpu=cortex-m4
    -mfpu=fpv4-sp-d16
    -mfloat-abi=hard
    -mthumb
)

project(EmbeddedSandbox C CXX ASM)
add_executable(${PROJECT_NAME}
    src/main.c
    hardware/startup_stm32f411xx.s
    hardware/syscall.c
)
target_compile_options(${PROJECT_NAME} PRIVATE
    ${MCU_FLAGS}
    -Wall
    -Wextra
    -Wpedantic
)
target_link_options( ${PROJECT_NAME} PRIVATE
    ${MCU_FLAGS}
    -T ${CMAKE_CURRENT_SOURCE_DIR}/hardware/stm32f411xe_flash.ld
    --specs=nano.specs
    --specs=nosys.specs
)
