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



************get_width.c***********

This function, get_width, takes a formatted string format, an integer pointer i, and a va_list list as arguments.

It is used to calculate the width specified in the format string for printing. The function starts by initializing a variable width to 0. It then iterates over the format string starting from the position indicated by the integer pointer i and checks if each character is a digit. If it is, it multiplies width by 10 and adds the numeric value of the digit. If it encounters an asterisk (*), it gets the width from the va_list list and stops processing the format string. If it encounters any other character, it stops processing the format string and returns the current value of width.

The function updates the value of i to the position of the last character it processed in the format string, and then returns the calculated width.



*************get_size.c************

The get_size.c  calculates the size to cast the argument based on the format specifier in the formatted string.

The function takes two parameters:

---format: A pointer to the formatted string.
----i: A pointer to the index of the format specifier in the formatted string.

The function returns an integer representing the size of the argument. This size is used to cast the argument to the correct type before printing.

The function first increments the index i by 1 to move past the format specifier to check the next character. If the next character is an "l", it sets the size to S_LONG (which is a constant defined elsewhere in the code), indicating that the argument should be cast to a long before printing. If the next character is an "h", it sets the size to S_SHORT, indicating that the argument should be cast to a short before printing.

If the next character is not an "l" or "h", the function sets i to curr_i - 1, effectively resetting it to the original index of the format specifier.

The function then returns the size of the argument. If no size was specified, the function returns 0, which indicates that the argument should be printed using its default type (e.g., int for %d and %i).



***********get_precision.c***********

This function get_precision takes a formatted string, an integer pointer i and a variable argument list list as input and returns the precision for printing.

The function first initializes a local variable curr_i to the value of *i + 1 and a local variable precision to -1. It then checks if the character at format[curr_i] is a period (.). If it is not, it returns -1.

If it is a period, the function initializes precision to 0 and iterates through the string starting from curr_i + 1. If the character at the current index is a digit, it multiplies precision by 10 and adds the difference between the character code of the digit and the character code of the digit 0. If the character at the current index is a star (*), the function increments curr_i and sets precision to the next argument in the variable argument list. If the character at the current index is not a digit or a star, the function breaks out of the loop.

Finally, the function sets *i to curr_i - 1 and returns precision.

Overall, this function is used to extract the precision value from the formatted string for printing.



