# String Series
## Series Introduction
In this series I will talk about things I have learnt over the years, tips and tricks, things that haunt me, and stuff I learnt from my mistakes. In this article I will talk about string length. Lets us get to it …

## In theory it is simple
When I was first introduced to string length, it was defined as the number of characters in a string. The first language I worked with was C, and the *string* was an array of `char` type that terminated with a `null` character. The length, if needed, was computed once using `strlen`. That functions counts characters until it reaches the `null` character (in hex `0x00` or `\0`). Passed my programming 101 test, one thing led to another, graduated, got a job. I started working on some projects, all worked great until I started to worked great, so I shipped it (published it on then popular code sharing website). I thought everything would be great, *BUT* you knew this was coming, it was *NOT*.

What is the length of **Orange**? you are right it is *six*. What is the length of **…**? you are right it is *three*, **just kidding**, it is *one*. What is the length of **ᓄᖅᑲᕆᑦ**?  It is *five*. What is the length of **ﷺ‎**? one, two, three …, that is an entire phrase in Arabic, it is technically *one* character. Let us use my favorite character counter, [Twitter](https://developer.twitter.com/en/docs/basics/counting-characters).
![Length of Arabic Word Ligatures](media/string_length_001.png)

Let us do one more, What is the length of this **🇺🇸**? It is actually *two*. It is not always easy to determine this visually. At this point, I this point I realized that there are *three* measures for string length.

1. Count of Characters: This is the number of characters according to the character script.
2. Count of Character Units: This is the number of `chars`, `wchar_t`, `unsigned short`, etc, used to store the string by your preferred language.
3. Count of Bytes: This is the number of bytes it takes to store the string.

I Know, I said *three*, but I need to mention this one. You won't need it often unless you own a UI framework, like WPF, X, Swing, etc.

4. Text Extent: The size of the string in display units, based on given *font* and *display device*.  


## OLD Part **needs to be removed**


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

