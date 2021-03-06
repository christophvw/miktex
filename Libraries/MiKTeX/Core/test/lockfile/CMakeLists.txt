## CMakeLists.txt                                       -*- CMake -*-
##
## Copyright (C) 2018 Christian Schenk
## 
## This file is free software; you can redistribute it and/or modify
## it under the terms of the GNU General Public License as published
## by the Free Software Foundation; either version 2, or (at your
## option) any later version.
## 
## This file is distributed in the hope that it will be useful, but
## WITHOUT ANY WARRANTY; without even the implied warranty of
## MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the GNU
## General Public License for more details.
## 
## You should have received a copy of the GNU General Public License
## along with this file; if not, write to the Free Software
## Foundation, 59 Temple Place - Suite 330, Boston, MA 02111-1307,
## USA.

set(tests
  1
)

set(exes
  1-1
  1-2
  1-3
)

foreach(t ${tests})
  add_executable(core_lockfile_test${t} ${t}.cpp ${test_sources})
  set_property(TARGET core_lockfile_test${t} PROPERTY FOLDER ${MIKTEX_CURRENT_FOLDER})
  if(USE_SYSTEM_LOG4CXX)
    target_link_libraries(core_lockfile_test${t} MiKTeX::Imported::LOG4CXX)
  else()
    target_link_libraries(core_lockfile_test${t} ${log4cxx_dll_name})
  endif()
  target_link_libraries(core_lockfile_test${t}
    ${core_dll_name}
    miktex-popt-wrapper
  )
  add_test(
    NAME core_lockfile_test${t}
    COMMAND $<TARGET_FILE:core_lockfile_test${t}>
  )
endforeach(t)

foreach(x ${exes})
  add_executable(core_lockfile_test${x} ${x}.cpp ${test_sources})
  set_property(TARGET core_lockfile_test${x} PROPERTY FOLDER ${MIKTEX_CURRENT_FOLDER})
  if(USE_SYSTEM_LOG4CXX)
    target_link_libraries(core_lockfile_test${x} MiKTeX::Imported::LOG4CXX)
  else()
    target_link_libraries(core_lockfile_test${x} ${log4cxx_dll_name})
  endif()
  target_link_libraries(core_lockfile_test${x}
    ${core_dll_name}
    Threads::Threads
    miktex-popt-wrapper
  )
endforeach()
