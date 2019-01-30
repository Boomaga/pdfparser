 # BEGIN_COMMON_COPYRIGHT_HEADER
 # (c)LGPL2+
 #
 #
 # Copyright: 2012-2013 Boomaga team https://github.com/Boomaga
 # Authors:
 #   Alexander Sokoloff <sokoloff.a@gmail.com>
 #
 # This program or library is free software; you can redistribute it
 # and/or modify it under the terms of the GNU Lesser General Public
 # License as published by the Free Software Foundation; either
 # version 2.1 of the License, or (at your option) any later version.
 #
 # This library is distributed in the hope that it will be useful,
 # but WITHOUT ANY WARRANTY; without even the implied warranty of
 # MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the GNU
 # Lesser General Public License for more details.
 #
 # You should have received a copy of the GNU Lesser General
 # Public License along with this library; if not, write to the
 # Free Software Foundation, Inc., 51 Franklin Street, Fifth Floor,
 # Boston, MA 02110-1301 USA
 #
 # END_COMMON_COPYRIGHT_HEADER


cmake_minimum_required(VERSION 3.0.0)
cmake_policy(SET CMP0028 NEW)

set (CMAKE_CXX_STANDARD 11)

project(pdffparser)

set(HEADERS
    pdferrors.h
    pdfobject.h
    pdfreader.h
    pdfvalue.h
    pdfwriter.h
    pdfxref.h
    pdfprocessor.h
)

set(SOURCES
    main.cpp

    pdfobject.cpp
    pdfreader.cpp
    pdfvalue.cpp
    pdfwriter.cpp
    pdfxref.cpp
    pdfprocessor.cpp
)


#*******************************************
set(CMAKE_INCLUDE_CURRENT_DIR ON)
set(CMAKE_AUTOMOC ON)
set(CMAKE_AUTOUIC ON)
set(CMAKE_AUTORCC ON)
find_package(Qt5 REQUIRED
    Core
#    Widgets
#    PrintSupport
#    LinguistTools
)

include_directories(
    ${CMAKE_CURRENT_SOURCE_DIR}
    ${CMAKE_SOURCE_DIR}
    ${CMAKE_CURRENT_BINARY_DIR}
    ${CUPS_INCLUDE_DIR}
)

find_package(ZLIB REQUIRED)
include_directories(${ZLIB_INCLUDE_DIRS})
set(LIBRARIES ${LIBRARIES} ${ZLIB_LIBRARIES})

add_executable(${PROJECT_NAME} ${HEADERS} ${SOURCES})
target_link_libraries(${PROJECT_NAME} ${LIBRARIES} Qt5::Core)# Qt5::Widgets Qt5::PrintSupport)

#install(TARGETS ${PROJECT_NAME} RUNTIME DESTINATION ${NONGUI_DIR})



