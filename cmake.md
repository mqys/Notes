# Content
- [Commands](#Commands)
- [Usage](#Usage)

---
## Commands
```
# CMakeLists.txt
# project information
project(projectname [CXX] [C] [Java])

# set variable
set(variable [value] [CACHE TYPE DOCSTRING [FORCE]])

# message
message([SEND_ERROR | STATUS | FATAL_ERROR] "message to display" ...)

# executable
add_executable(hello ${SRC_LIST})

# sub directory, need CMakeLists.txt in sub dir
add_subdirectory(source_dir [Binary_dir] [Exclude_from_all])

# relocate the output
set(EXECUTABLE_OUTPUT_PATH ${PROJECT_BINARY_DIR}/bin)
set(LIBRARY_OUTPUT_PATH ${PROJECT_BINARY_DIR}/lib)

# install with CMAKE_INSTALL_PREFIX
install (TARGETS targets...
    [[ARCHIVE | LIBARY | RUNTIME]
     [DESTINATION <dir>]
     [PERMISSIONS permissions...]
     [CONFIGURATIONS [Debug | Release | ...]]
     [COMPONENT <component>]
     [OPTIONAL]
    ]
)

# lib
add_library(libname [SHARED | STATIC | MODULE] [EXCLUDE_FROM_ALL] source1 source2 ...)
set_target_properties()

# use libs
# include 
include_directory([AFTER | BEFORE] [SYSTEM] dir1 dir2 ...)
# link
link_directory(dir1 dir2 ..)

target_link_libraries(target library1
    <debug | optimized> library2
    ...
)

# add source in a dir
aux_source_directory(dir VARIABLE)
```

### Usage
```
mkdir build
cd ./build
cmake .. && make
```
