cmake_minimum_required(VERSION 2.8.3)
project(libsbp)

## Find catkin macros and libraries
find_package(catkin REQUIRED)

catkin_package(
#   INCLUDE_DIRS include
   LIBRARIES sbp
#  CATKIN_DEPENDS 
#  DEPENDS 
)

#############
## Build ##
#############

set(C_GEN_HEADERS
  ${CMAKE_CURRENT_SOURCE_DIR}/c/include/libsbp/acquisition.h
  ${CMAKE_CURRENT_SOURCE_DIR}/c/include/libsbp/common.h       
  ${CMAKE_CURRENT_SOURCE_DIR}/c/include/libsbp/ext_events.h   
  ${CMAKE_CURRENT_SOURCE_DIR}/c/include/libsbp/flash.h       
  ${CMAKE_CURRENT_SOURCE_DIR}/c/include/libsbp/logging.h      
  ${CMAKE_CURRENT_SOURCE_DIR}/c/include/libsbp/observation.h  
  ${CMAKE_CURRENT_SOURCE_DIR}/c/include/libsbp/sbp.h          
  ${CMAKE_CURRENT_SOURCE_DIR}/c/include/libsbp/system.h       
  ${CMAKE_CURRENT_SOURCE_DIR}/c/include/libsbp/user.h
  ${CMAKE_CURRENT_SOURCE_DIR}/c/include/libsbp/bootload.h    
  ${CMAKE_CURRENT_SOURCE_DIR}/c/include/libsbp/edc.h          
  ${CMAKE_CURRENT_SOURCE_DIR}/c/include/libsbp/file_io.h      
  ${CMAKE_CURRENT_SOURCE_DIR}/c/include/libsbp/gnss_signal.h  
  ${CMAKE_CURRENT_SOURCE_DIR}/c/include/libsbp/navigation.h   
  ${CMAKE_CURRENT_SOURCE_DIR}/c/include/libsbp/piksi.h        
  ${CMAKE_CURRENT_SOURCE_DIR}/c/include/libsbp/settings.h     
  ${CMAKE_CURRENT_SOURCE_DIR}/c/include/libsbp/tracking.h     
  ${CMAKE_CURRENT_SOURCE_DIR}/c/include/libsbp/version.h
)

set(PYTHON_SRC
  ${CMAKE_CURRENT_SOURCE_DIR}/python/sbp/acquisition.py  
  ${CMAKE_CURRENT_SOURCE_DIR}/python/sbp/observation.py
  ${CMAKE_CURRENT_SOURCE_DIR}/python/sbp/bootload.py     
  ${CMAKE_CURRENT_SOURCE_DIR}/python/sbp/piksi.py
  ${CMAKE_CURRENT_SOURCE_DIR}/python/sbp/ext_events.py   
  ${CMAKE_CURRENT_SOURCE_DIR}/python/sbp/settings.py
  ${CMAKE_CURRENT_SOURCE_DIR}/python/sbp/file_io.py     
  ${CMAKE_CURRENT_SOURCE_DIR}/python/sbp/system.py
  ${CMAKE_CURRENT_SOURCE_DIR}/python/sbp/flash.py       
  ${CMAKE_CURRENT_SOURCE_DIR}/python/sbp/table.py
  ${CMAKE_CURRENT_SOURCE_DIR}/python/sbp/gnss_signal.py
  ${CMAKE_CURRENT_SOURCE_DIR}/python/sbp/tracking.py
  ${CMAKE_CURRENT_SOURCE_DIR}/python/sbp/__init__.py    
  ${CMAKE_CURRENT_SOURCE_DIR}/python/sbp/user.py
  ${CMAKE_CURRENT_SOURCE_DIR}/python/sbp/logging.py      
  ${CMAKE_CURRENT_SOURCE_DIR}/python/sbp/utils.py
  ${CMAKE_CURRENT_SOURCE_DIR}/python/sbp/msg.py          
  ${CMAKE_CURRENT_SOURCE_DIR}/python/sbp/version.py
  ${CMAKE_CURRENT_SOURCE_DIR}/python/sbp/navigation.py
)


add_custom_command(
  OUTPUT  ${C_GEN_HEADERS}
  COMMAND make gen-c
)
add_custom_target(gen-c ALL DEPENDS ${C_GEN_HEADERS})

# Build and install c
add_subdirectory(c)


add_custom_command(
  OUTPUT ${PYTHON_SRC}
  COMMAND make gen-python
)

add_custom_target(gen-python ALL 
  DEPENDS ${PYTHON_SRC}
)

#############
## Install ##
#############

# Install python module
install(FILES ${PYTHON_SRC}
  DESTINATION lib/python2.7/dist-packages/sbp
)

