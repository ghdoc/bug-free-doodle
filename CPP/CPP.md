**C++**

## C++ Crash Course

- CH2. Types

	- Integer
	- Integer types are signed and int by default, which means you can use the following shorthand notations in your programs: short, long, and long long rather than short int, long int, and long long int.
	- Notice that the integer type sizes vary across platforms: 64-bit Windows and Linux/Mac have different sizes for a long integer (4 and 8, respectively).
	- If you want to enforce guaranteed integer sizes, you can use integer types in the <cstdint> library. For example, if you need a signed integer with exactly 8, 16, 32, or 64 bits, you could use int8_t, int16_t, int32_t, or int64_t. You’ll find options for the fastest, smallest, maximum, signed, and unsigned integer types to meet your requirements. But because this header is not always available in every platform, you should only use cstdint types when there is no other alternative.
	- Integer literals can contain any number of single quotes (') for readability. These are completely ignored by the compiler. For example, 1000000 and 1'000'000 are both integer literals equal to one million.
	- To print an unsigned integer in its hexadecimal representation or (rarely) its octal representation. You can use the printf specifiers %x and %o for these purposes  
	    “#include <cstdio>
	
	 int main() {
	   unsigned int a = 3669732608;
	   printf("Yabba %x➊!\n", a);
	   unsigned int b = 69;
	   printf("There are %u➋,%o➌ leaves here.\n", b➍, b➎);
	 }
- --------------------------------------------------------------------------
- Yabba dabbad00➊!
- There are 69➋,105➌ leaves here.”

- Excerpt From
- C++ Crash Course: A Fast-Paced Introduction
- Josh Lospinoso
- [https://itunes.apple.com/WebObjects/MZStore.woa/wa/viewBook?id=0](https://itunes.apple.com/WebObjects/MZStore.woa/wa/viewBook?id=0)
- This material may be protected by copyright.
- Note

- Eliminate leading zeros on decimal literals; otherwise, they’ll cease to be decimal.
- By default, an integer literal’s type is one of the following: int, long, or long long. An integer literal’s type is the smallest of these three types that fits. (This is defined by the language and will be enforced by the compiler.)
- If you want more control, you can supply suffixes to an integer literal to specify its type
- Since an int can store 112114, the resulting integer literal is an int. If you really want, say, a long, you can instead specify 112114L (or 112114l).

- Notes

- CH2 Types
	
	- Fundamental Types are primitive types. They will work on any platform, but their features, such as size and memory layout, depend on the implementation.
	- Types and Format Specifier
	
	- Note the basic ones, then either add h or l or ll as needed
	- Basic 4 bytes on all 32 and 64 bit OS
	
	- int = %d
	- unsigned int = %u
	
	- Small 2 bytes on all 32 and 64 bit OS
	
	- short = %hd
	- unsigned short = %hu
	
	- Big 4 bytes on all 32 bit OS and 64 it Windows, but 8 bits on Linux/Mac 
	
	- long = %ld
	- unsigned long = %lu
	
	- Super Big 8 bytes on all 32 and 64 bit OS
	
	- long long = %lld
	- unsigned long long = %llu

- Representation of numbers
	
	- binary prefix 0b
	- octal prefix 0
	- decimal is default
	- hex 0x
	
	- printf
	
	- hex %x
	- octal %o
	
	- Enforcing 8, 16, 32, 64 bits => int8_t, int16_t, int32_t, int64_t
	- Floating Point Types - Although it's not possible to represent an arbitrary real number exactly in computer memory, it's possible to store an approximation.
	
	- float a = 0.1f 4 bytes
	- double b = 0.2; 8 bytes
	- long double c = 0.3l 8 bytes

- Floating Point Format Specifier
	
	- float with decimal digits %f
	- Same number in scientific notation %e
	- printf can decide and chose the compact of either one if you pass %g format specifier
	- You can omit the l prefix on format specifier for double because printf promotes float arguments to double precision
	
- Char

	- Default type is 1 byte, May or may not be signed
	- char16_t 2 byte char set utf-16
	- char32_t 4 byte char set utf-32
	- signed char - same as char but guaranteed to be signed
	- unsigned char - same as char but guaranteed to be unsigned
	- wchar_t - large enough to contain the largest character of the implementation's locale
	- If the char is any type other than 'char' then prefix with - L for wchar_t u for char16_t and U for char32_t
	- Unicode
	
	- Specified by \u followed by 4 digit unicode code point OR
	- by \U followed by 8 digit unicode point

- Boolean

	- Integer types and boolean types convert readily
	- Any non-zero int converts to true and zero converts to false
	- True state converts to 1 and False converts to 0
	- There is no format specifier for booleans. You can use int format specifier.
	
- [https://hackingcpp.com/cpp/cheat_sheets.html](https://hackingcpp.com/cpp/cheat_sheets.html)