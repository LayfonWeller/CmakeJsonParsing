CmakeJsonParsing
================

This "extension" to cmake is a script that will load a Json file and add it's variable in cmake.
It offers helper "functions" to navigate the "cmakefied" json.
It requires a C++ compiler has the code use an try_compile command to read the json and generate a .cmake with all the variable.
The parser is build in plain C++ with only picojson.h has a dependency. PicoJson is included with the C++ file and it's license has been appended to the license file.

Usage
=====

To use the script in your application, you must copy JsonParsing.cmake and JsonParsing folder to your project.
It is recommended to use a CMake folder in your project, and appending the path to that folder to CMAKE_MODULE_PATH variable. 
Thus you can place the file and the folder in that directory.


TODO
====

1. Add documentation
2. Change macro to function for json navigation "functions"
