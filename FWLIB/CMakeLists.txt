aux_source_directory(src STM32F4_LIB_SRC)
# FMC/FSMC only defined for some F4 families
# if (DEVICE_FAMILY STREQUAL STM32F427_437xx OR DEVICE_FAMILY STREQUAL STM32F429_439xx OR DEVICE_FAMILY STREQUAL STM32F446xx OR DEVICE_FAMILY STREQUAL STM32F469_479xx)
#   set(sources ${sources} Src/stm32f4xx_fmc.c)
# else()
#   set(sources ${sources} Src/stm32f4xx_fsmc.c)
# endif()



add_library(stm32f4xx_lib ${STM32F4_LIB_SRC})

target_compile_definitions(stm32f4xx_lib PUBLIC -DUSE_STDPERIPH_DRIVER -D${MCU_TYPE})

#target_link_libraries(stm32f4xx_hal PUBLIC cmsis)
target_include_directories(stm32f4xx_lib PUBLIC
  $<BUILD_INTERFACE:${CMAKE_CURRENT_SOURCE_DIR}/inc>
  PRIVATE src)
