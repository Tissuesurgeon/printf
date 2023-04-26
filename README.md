This printf repo contains functions and a main program that implements a simplified version of the printf function that supports a subset of the standard formatting options.

**********main.h*************
The main.h file is a header file for a custom implementation of the printf function in C. The file defines a variety of macros, structs, and functions for handling different format specifiers and printing their corresponding values.

The macros define various flags and sizes used in the implementation, such as the "F_MINUS" flag indicating a left-justified field, or the "S_LONG" size indicating a long integer.

The "struct fmt" struct defines a format specifier and a corresponding function for printing its value. The "fmt_t" typedef is simply an alias for this struct.

The functions defined in the file handle printing different types of values, such as characters, strings, and numbers. They take in various parameters such as flags, width, and precision, and write the corresponding value to a buffer.

Other functions handle getting the various format options from the input format string, such as the width and precision. There are also utility functions for converting between different sizes of numbers and checking if a character is printable.


**************write_handlers.c*******************

The write_handlers.c file contains the implementation of functions to handle the printf function in C. The code is split into three main functions: handle_write_char, write_number, and write_unsgnd. These functions are responsible for handling the printing of characters, signed numbers, and unsigned numbers, respectively.

The handle_write_char function takes a character as input and writes it to the output buffer. It also handles padding and width specifiers.

The write_number function handles the printing of signed numbers. It takes the number, the output buffer, and various specifiers such as padding, width, and precision. It also handles negative numbers, positive numbers, and space padding.

The write_unsgnd function handles the printing of unsigned numbers. It takes the number, the output buffer, and various specifiers such as padding, width, and precision.

All functions return the number of characters written.`
