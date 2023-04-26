This printf repo contains functions and a main program that implements a simplified version of the printf function that supports a subset of the standard formatting options.

**********main.h*************
The main.h file is a header file for a custom implementation of the printf function in C. The file defines a variety of macros, structs, and functions for handling different format specifiers and printing their corresponding values.

The macros define various flags and sizes used in the implementation, such as the "F_MINUS" flag indicating a left-justified field, or the "S_LONG" size indicating a long integer.

The "struct fmt" struct defines a format specifier and a corresponding function for printing its value. The "fmt_t" typedef is simply an alias for this struct.

The functions defined in the file handle printing different types of values, such as characters, strings, and numbers. They take in various parameters such as flags, width, and precision, and write the corresponding value to a buffer.

Other functions handle getting the various format options from the input format string, such as the width and precision. There are also utility functions for converting between different sizes of numbers and checking if a character is printable.


`
