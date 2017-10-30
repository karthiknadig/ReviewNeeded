# String Series
## Series Introduction
In this series I will talk about things I have learnt over the years, tips and tricks, things that haunt me, and stuff I learnt from my mistakes. In this article I will talk about string length. Lets us get to it …

## In theory it is simple
When I was first introduced to string length, it was defined as the number of characters in a string. The first language I worked with was C, and the *string* was an array of `char` type that terminated with a `null` character. The length, if needed, was computed once using `strlen`. That functions counts characters until it reaches the `null` character (in hex `0x00` or `\0`). Passed my programming 101 test, one thing led to another, graduated, got a job. I started working on some projects, all worked great until I started to worked great, so I shipped it (published it on then popular code sharing website). I thought everything would be great, *BUT* you knew this was coming, it was *NOT*.

What is the length of **Orange**? you are right it is *six*. What is the length of **…**? you are right it is *three*, **just kidding**, it is *one*. What is the length of **ᓄᖅᑲᕆᑦ**?  It is *five*. What is the length of **ﷺ‎**? one, two, three …, that is an entire phrase in Arabic, it is technically *one* character. Let us use my favorite character counter, [Twitter](https://developer.twitter.com/en/docs/basics/counting-characters).
![Length of Arabic Word Ligatures](media/string_length_arabic_ligature.png)

Let us do one more, What is the length of this **🇺🇸**? It is actually *two*. It is not always easy to determine this visually. At this point, I this point I realized that there are *three* measures for string length.

1. Count of Characters: This is the number of characters according to the character script.
2. Count of Character Units: This is the number of `chars`, `wchar_t`, `unsigned short`, etc, used to store the string by your preferred language.
3. Count of Bytes: This is the number of bytes it takes to store the string.

I Know, I said *three*, but I need to mention this one. You won't need it often unless you own a UI framework, like WPF, X, Swing, etc.

4. Text Extent: The size of the string in display units, based on given *font* and *display device*.  


### References:
[1]  Eastern Canadian Inuktitut for `stop`, see [ᓄᖅᑲᕆᑦ](https://commons.wikimedia.org/wiki/File%3AIqaluitStop.jpg)

