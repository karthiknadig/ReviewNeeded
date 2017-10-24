# The String Series: String Length
When I was learning to code, string length was a was an exercise in the loop chapter for C programming. I thought I understood string length fairly well. I was wrong, so wrong.

Every developer at some point has to work with strings. Eventually, the product grows or the dev moves ahead in their career, they have to deal with string encoding. That is the dreaded day they realize how broken their software is. If you don't have scars from working with strings you have **NOT** worked with strings.

## What is string length?
It should be simple. What is the length of **ABCDE**? If you said **5**, then great you know how to calculate string length. Now, let's try that one more time. What is the length of **ᓄᖅᑲᕆᑦ**?[1] It could be 5, 6, 15, 38 or more (we will get to 38 or more mess later). *Length* here by default is number of *characters units*. That is *character units* and not just *characters*. Depending on which editor or browser you are using this character "🇺🇸" will show up as `us` or a glyph of a flag. What is the length of **🇺🇸**?

The number of bytes needed per character was 1 for a while, hence it made sense at that time that all the libraries that were written assumed this. Hence, `strlen` in C, meant you were computing the number of characters.

With globalization, the need to support other languages has increased. So we now have multi-byte characters, wide characters, and encoding. What does string length means for an encoded string? Modern string libraries support computing length by characters or bytes. For example, on windows, you have `strsafe.h`, `StringCchLength` to compute number of characters, and `StringCcbLength` to compute number of bytes. With managed languages, you will have to worry about this if you are doing cross-platform application. If you are working with Unicode, consider using [ICU](http://icu-project.org).

* If you count **ᓄᖅᑲᕆᑦ** by character units, in CS sense, there are 5 character units. Hence, the length of the string, considering character units, is 5.
* If you print **ᓄᖅᑲᕆᑦ** on to paper and ask someone to count. They could see 6 characters, 3 distinct ones in various orientations.
* If you count the number of bytes needed to store **ᓄᖅᑲᕆᑦ**, the result could be 15. This depends on the default encoding used to store strings.

There is yet another measure that is used commonly in the OS, specifically in UI. It is the length of a string with a given font and device resolution. 

### References:
[1]  Eastern Canadian Inuktitut for `stop`, see [ᓄᖅᑲᕆᑦ](https://commons.wikimedia.org/wiki/File%3AIqaluitStop.jpg)

