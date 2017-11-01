# String Series
## Series Introduction
In this series I will talk about things I have learnt over the years, tips and tricks, things that haunt me, and stuff I learnt from my mistakes. In this article I will talk about string length. Lets us get to it …

## In theory it is simple
But… When I was first introduced to string length, it was defined as the number of characters in a string. The first language I worked with was C, and the *string* was an array of `char` type that terminated with a `null` character. The length, if needed, was computed once using `strlen`. That functions counts characters until it reaches the `null` character (in hex `0x00` or `\0`). Passed my programming 101 test, one thing led to another, graduated, got a job. I started working on some projects, all worked great until I started to worked great, so I shipped it (published it on then popular code sharing website). I thought everything would be great, *BUT* you knew this was coming, it was *NOT*.

What is the length of **Orange**? you are right it is *six*. What is the length of **…**? you are right it is *three*, **just kidding**, it is *one*. What is the length of **ᓄᖅᑲᕆᑦ**? (Eastern Canadian Inuktitut for `stop`) It is *five*. What is the length of **ﷺ‎**? one, two, three …, that is an entire phrase in Arabic, it is technically *one* character. Let us use my favorite character counter, [Twitter](https://developer.twitter.com/en/docs/basics/counting-characters).
![Length of Arabic Word Ligatures](media/string_length_arabic_ligature.png)

Let us do one more, What is the length of this **🇺🇸**? It is actually *two*. It is not always easy to determine this visually. At this point I realized that there are *three* measures for string length. Take the word **ಕನ್ನಡ**.

1. **Count of Characters**: This is the number of characters according to the character script. **ಕನ್ನಡ** has 3 characters.
2. **Count of Character Units**: This is the number of `chars`, `wchar_t`, `unsigned short`, etc, used to store the string by your preferred language. **ಕನ್ನಡ** takes 3 symbols and 2 modifiers, hence 5 character units. It looks like this, `<U+0C95><U+0CA8><U+0CCD><U+0CA8><U+0CA1>`. This is what programming languages consider as length.
3. **Count of Bytes**: This is the number of bytes it takes to store the string. **ಕನ್ನಡ** takes 15 bytes, it looks like this `e0 b2 95 e0 b2 a8 e0 b3 8d e0 b2 a8 e0 b2 a1`.

I Know, I said *three*, but I have to mention this one. You won't need it often unless you own a UI framework, like WPF, X, Swing, etc.

4. **Text Extent** or **Measure**: The size of the string in display units, based on given *font* and *display device*.  

## Off-by-one bug : String length edition
The terminating `null` plays a major role in this issue. Some APIs prefer to use string length excluding the `null` (such as `strncat`), or including the `null` (such as `memcpy`). Windows has the [strsafe](https://msdn.microsoft.com/en-us/library/windows/desktop/ff468908(v=vs.85).aspx) APIs, with `*Cch*` (Count character APIs) and `*Cb*` (Count byte APIs), where the `null` terminator is required. Then there is the `BSTR` set of APIs in Windows which, deal with strings without the `null` terminator (side note: `BSTR` saves the length of the string along with the string itself at -4 bytes from the pointer to the first character in the string). Lastly, about `null`s, there can be double-null terminator to indicate the end of a string, if the string is encoded using multi-byte encoding format like UTF-8. So, if you save **ಕನ್ನಡ** to a file with UTF-8 encoding, it will take 17 bytes. That means when you are reading it, you need a buffer at least 17 bytes long to store the full string in a usable form. These variations, in how APIs deal with strings, often lead to off-by-one bugs. Especially when using two libraries that use different ways to work with strings. 

## This is madness. This is unicode.
If you have to deal with strings in a globalization context, and you have native code, then consider using [**International Components for Unicode**](icu-project.org). Managed languages make this easy, until you have to interface with another platform or un-managed library. If you are writing a parser, string formatter, serializer, deserializer, use existing format (JSON, XML, YAML, BSON, etc).