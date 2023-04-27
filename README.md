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



********get_flags.c*******



This function get_flags takes in a formatted string and an integer pointer i and calculates the active flags in the format specifier starting from the position i.

The active flags in a format specifier are -, +, 0, #, and ' '. These flags can be used to modify the output of the format specifier. The function loops through the format specifier string, checking for each flag character in the FLAGS_CH array, and sets the corresponding flag in the flags integer variable using the bitwise OR operator.

Finally, the function updates the integer pointer i to point to the last character in the flags section of the format specifier and returns the integer flags.

Note that the flag values are defined as macros in the header file main.h, using bitwise shift operators to represent each flag as a unique bit in the integer value. This allows multiple flags to be combined using bitwise OR operations.





***********functions2.c*************


This is a program that defines several functions for formatting and printing text. 

The functions defined include:

---print_pointer: Prints the value of a pointer variable in hexadecimal format. If the pointer is NULL, prints (nil) instead. It takes in various formatting arguments such as flags, width, precision, and size to control the output.
---print_non_printable: Prints a string and replaces non-printable characters with their ASCII codes in hexadecimal format. If the string is NULL, prints (null) instead.
---print_reverse: Prints a string in reverse order. If the string is NULL, prints )Null( instead.
---print_rot13string: Prints a string encoded in rot13 format. If the string is NULL, prints (AHYY) instead.

Each function takes in a va_list argument named types, which is used to access additional arguments passed to the function via a variable argument list. The functions return the number of characters printed to standard output.




********************functions1.c************

This function defines several functions for printing unsigned numbers in different formats (octal, hexadecimal, and uppercase hexadecimal). The functions take a variable number of arguments and output the corresponding number to a buffer.

The main function is print_unsigned, which takes an unsigned long int and prints it as a decimal number. The function print_octal prints the number in octal notation, while print_hexadecimal and print_hexa_upper print the number in hexadecimal notation, using lowercase and uppercase letters respectively. The print_hexa function is a helper function for printing the hexadecimal format, and takes a character array map_to as an argument to map the digits of the hexadecimal number to the appropriate characters.

All of the functions take the same arguments: a va_list of arguments, a buffer array to handle the print, and various flags, width, precision, and size specifiers that are used to format the output. The functions return the number of characters printed.

The code also defines some macros such as UNUSED and BUFF_SIZE that are used throughout the code. Overall, this code provides a useful set of functions for printing unsigned numbers in different formats.




******************functions.c**************



This function implements several functions for printing different types of data.

The functions include:

----print_char: Prints a single character.
----print_string: Prints a null-terminated string.
----print_percent: Prints a percent sign.
----print_int: Prints a signed integer.
----print_binary: Prints an unsigned integer in binary format.

Each function takes a variable number of arguments using the va_list type from the stdarg.h header. The other arguments to the function specify formatting options, such as the minimum width and precision of the printed output.

The functions utilize the write() function from the unistd.h header to output characters to the standard output stream (i.e., the console).




*****************_printf.c*******************

This is a partial implementation of the _printf function in C. The _printf function is similar to the standard library printf function, which is used to print formatted output to the console.

The _printf function takes in a format string, which contains a mix of plain text and format specifiers. It then iterates through the format string character by character, checking for format specifiers and handling them accordingly. It stores the output in a buffer to improve performance, which is flushed to the console when the buffer is full.

The function also uses a variable argument list (va_list) to handle an arbitrary number of arguments passed in after the format string.

The print_buffer function is a helper function that prints the contents of the buffer to the console and resets the buffer index to 0. This function is called at various points in the _printf function to ensure that the buffer is flushed to the console as necessary.

Overall, this code provides a basic framework for implementing a printf-like function in C, but it is missing several key components, such as the get_flags, get_width, get_precision, get_size, and handle_print functions, which are responsible for parsing the format string and handling each format specifier.



