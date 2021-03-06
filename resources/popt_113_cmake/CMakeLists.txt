# Copyright 2016, akashche at redhat.com
#
# Licensed under the Apache License, Version 2.0 (the "License");
# you may not use this file except in compliance with the License.
# You may obtain a copy of the License at
#
# http://www.apache.org/licenses/LICENSE-2.0
#
# Unless required by applicable law or agreed to in writing, software
# distributed under the License is distributed on an "AS IS" BASIS,
# WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
# See the License for the specific language governing permissions and
# limitations under the License.

cmake_minimum_required ( VERSION 2.8.12 )

project ( lookaside_popt C )

set ( ${PROJECT_NAME}_SRCDIR ${CMAKE_CURRENT_LIST_DIR}/../../../../lookaside/popt )

add_library ( ${PROJECT_NAME} STATIC 
        ${${PROJECT_NAME}_SRCDIR}/findme.c
        ${${PROJECT_NAME}_SRCDIR}/popt.c
        ${${PROJECT_NAME}_SRCDIR}/popthelp.c
        ${${PROJECT_NAME}_SRCDIR}/poptint.c
        ${${PROJECT_NAME}_SRCDIR}/poptparse.c )
target_include_directories ( ${PROJECT_NAME} BEFORE PRIVATE 
        ${CMAKE_CURRENT_LIST_DIR}/../../resources/popt_113_include
        ${${PROJECT_NAME}_SRCDIR} )
target_compile_definitions ( ${PROJECT_NAME} PRIVATE -DHAVE_CONFIG_H ) 
if ( ${CMAKE_C_COMPILER_ID}x MATCHES "MSVCx" )
    target_compile_definitions ( ${PROJECT_NAME} PRIVATE
            -Dinline=_inline
            -Dalloca=_alloca
            -DX_OK=06 ) 
endif ( )
