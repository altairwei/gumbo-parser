
# Copyright 2016 Google Inc. All rights reserved.
#
# Licensed under the Apache License, Version 2.0 (the "License");
# you may not use this file except in compliance with the License.
# You may obtain a copy of the License at
#
#     http://www.apache.org/licenses/LICENSE-2.0
#
# Unless required by applicable law or agreed to in writing, software
# distributed under the License is distributed on an "AS IS" BASIS,
# WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
# See the License for the specific language governing permissions and
# limitations under the License.

cmake_minimum_required(VERSION 2.8.7)

project(Gumbo C)

set(Gumbo_VERSION "0.10.1")

# Gumbo source files.
set(Gumbo_SRCS
    src/attribute.c
    src/attribute.h
    src/char_ref.c
    src/char_ref.h
    src/error.c
    src/error.h
    src/insertion_mode.h
    src/parser.c
    src/parser.h
    src/string_buffer.c
    src/string_buffer.h
    src/string_piece.c
    src/string_piece.h
    src/tag.c
    src/tag_enum.h
    src/tag_gperf.h
    src/tag_strings.h
    src/tag_sizes.h
    src/token_type.h
    src/tokenizer.c
    src/tokenizer.h
    src/tokenizer_states.h
    src/utf8.c
    src/utf8.h
    src/util.c
    src/util.h
    src/vector.c
    src/vector.h)

include_directories(
	${PROJECT_SOURCE_DIR}
	${PROJECT_BINARY_DIR}
)

if(MSVC)
    include_directories(
        ${PROJECT_SOURCE_DIR}/visualc/include
        ${PROJECT_BINARY_DIR}/visualc/include
    )
endif(MSVC)

# Compile as C99 (default is C89, which Gumbo is not written in).
if(CMAKE_C_COMPILER_ID EQUAL GNU OR
   CMAKE_CXX_COMPILER_ID EQUAL GNU OR
   CMAKE_CXX_COMPILER_ID EQUAL Clang)
  set(CMAKE_C_FLAGS "-std=c99")
endif()

# Library target.
add_library(Gumbo SHARED ${Gumbo_SRCS})
add_library(Gumbo_static STATIC ${Gumbo_SRCS})

set_target_properties(Gumbo PROPERTIES VERSION ${Gumbo_VERSION})
set_target_properties(Gumbo_static PROPERTIES OUTPUT_NAME "Gumbo")

install(TARGETS Gumbo  Gumbo_static
	LIBRARY DESTINATION lib
    ARCHIVE DESTINATION lib
)