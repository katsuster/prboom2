cmake_minimum_required(VERSION 3.16)

# Usage
#   cmake -B build ./
# Headers are created and placed in build/include directory.

project(test_bin2c)
enable_language(C)

add_executable(test_bin2c)
target_sources(test_bin2c PRIVATE main.c)
target_include_directories(test_bin2c PRIVATE
  ${CMAKE_BINARY_DIR}/include
  )

function(convert_bin2c input_file output_file c_var_name)
  file(READ ${input_file} BIN_HEX HEX)
  file(SIZE ${input_file} BIN_LEN)

  # Wrap lines per 16bytes
  string(REPEAT ".." 16 REGEX_PAT)
  string(REGEX REPLACE "(${REGEX_PAT})" "\\1\n" BIN_HEX_WRAP ${BIN_HEX})
  string(REGEX REPLACE "([0-9a-f][0-9a-f])" "0x\\1, " BIN_ARRAY ${BIN_HEX_WRAP})

  # C format
  set(C_H_INC "#include <stdint.h>")
  set(C_H_LEN "const size_t ${c_var_name}_len = ${BIN_LEN};")
  set(C_H_DAT "const uint8_t ${c_var_name}_dat[] = {\n${BIN_ARRAY}\n};")

  # Generate header
  file(WRITE ${output_file} "${C_H_INC}\n\n${C_H_LEN}\n${C_H_DAT}\n")
endfunction()

convert_bin2c(${CMAKE_SOURCE_DIR}/DOOM.WAD ${CMAKE_BINARY_DIR}/include/doombin.h doombin)
convert_bin2c(${CMAKE_SOURCE_DIR}/prboom.wad ${CMAKE_BINARY_DIR}/include/prboombin.h prboombin)
