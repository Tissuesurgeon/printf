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

All functions return the number of characters written.


*************utils.c**************

The utils.c file defines several functions:

---is_printable: a function that takes a character as input and checks if it is printable. If it is, it returns 1, otherwise, it returns 0.

--append_hexa_code: a function that takes an ASCII code as input and appends its hexadecimal representation to a buffer at a given index. It returns 3, which is the number of characters appended to the buffer.

--is_digit: a function that takes a character as input and checks if it is a digit. If it is, it returns 1, otherwise, it returns 0.

--convert_size_number: a function that takes a number and a size as input and casts the number to the specified size. It returns the casted value of the number.

--convert_size_unsgnd: a function that takes an unsigned number and a size as input and casts the number to the specified size. It returns the casted value of the number.


***********handle_print.c**************

This function takes in a formatted string, a list of arguments, a buffer to handle printing, and various formatting specifications. It iterates through a list of supported format types, and if it matches the current character in the formatted string, it calls the corresponding print function to print the argument. If the current character does not match any of the supported format types, it prints the character as-is, preceded by a percent sign.

The function returns the number of characters printed, or -1 if there was an error.


