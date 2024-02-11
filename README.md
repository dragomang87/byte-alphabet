# byte-alphabet

If you have just enough amount of programming,
you will know that multible alphabets exist to describe binary data:
the basic 0 or 1, octets 0 to 7, hexadecimals 0 to F, and of course decimals 0 to 9.
In particular, because the hexadecimals are the largest alphabets,
they are also the choice that makes for the shortest representation.

For certain applications however, in particular security, data chunks of considerable size,
e.g. 128 bits and above, are used both theoretically and in practice (e.g. AES instruction set extension).
While hexadecimal is still the shortest representation, hexadecimal 128 bits and above
are still quite large in manual and direct inspection.

The goal of this repository is to propose an intuitive byte alphabet
and a way to type them using Linux's Compose key.
This is done in [Introducing the byte alphabet](#introducing-the-byte-alphabet)
and  [Typing the byte alphabet](#typing-the-byte-alphabet) below.

### Examples
For example, the following are representations of low weight irreducible polynomials for 8, 16, 32, 64, 128, 256, 512 bits
taken from https://www.hpl.hp.com/techreports/98/HPL-98-135.pdf:
```
8  : 0x11b
16 : 0x1002b
32 : 0x10000008d
64 : 0x1000000000000001b
128: 0x100000000000000000000000000000087
256: 0x10000000000000000000000000000000000000000000000000000000000000425
512: 0x100000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000125
```

Having a full set of symbols for one byte (two hex's), would at least mitigate this problem slightly.
Notice that for some applications like exactly displaying low weight numbers with many consecutive zeros as above,
the impact of such change would be minimal, as most of the symbols would still be zero.



# Introducing the byte alphabet

The full alphabet and design choices are explain in length in the text file duotrigentidecimal_numbers.txt.
The essence is the following: the 8 bits are separated into 3 + 5 bits
* 5 bits are assigned their own basic symbols, namely an extension of hex 0 to F to 32 symbols going from 0 to Z (I O U V are excluded)
* 3 bits are assigned to 7 different diacritics (000 corresponds to no diacritics, just the basic alphabet):
  * ```0xx```: none, underline, strikethrough, overline
  * ```1xx```: tilde, slash, circumflex (hat), dieresis (umlaut)
Giving the following alphabet:
```
0x000.....: 0 1 2 3 4 5 6 7 8 9 A B C D E F G H J K L M N P Q R S T W X Y Z
0x001.....: 0̲ 1̲ 2̲ 3̲ 4̲ 5̲ 6̲ 7̲ 8̲ 9̲ A̲ B̲ C̲ D̲ E̲ F̲ G̲ H̲ J̲ K̲ L̲ M̲ N̲ P̲ Q̲ R̲ S̲ T̲ W̲ X̲ Y̲ Z̲
0x010.....: 0̶ 1̶ 2̶ 3̶ 4̶ 5̶ 6̶ 7̶ 8̶ 9̶ A̶ B̶ C̶ D̶ E̶ F̶ G̶ H̶ J̶ K̶ L̶ M̶ N̶ P̶ Q̶ R̶ S̶ T̶ W̶ X̶ Y̶ Z̶
0x011.....: 0̅ 1̅ 2̅ 3̅ 4̅ 5̅ 6̅ 7̅ 8̅ 9̅ A̅ B̅ C̅ D̅ E̅ F̅ G̅ H̅ J̅ K̅ L̅ M̅ N̅ P̅ Q̅ R̅ S̅ T̅ W̅ X̅ Y̅ Z̅
0x100.....: 0̃ 1̃ 2̃ 3̃ 4̃ 5̃ 6̃ 7̃ 8̃ 9̃ Ã B̃ C̃ D̃ Ẽ F̃ G̃ H̃ J̃ K̃ L̃ M̃ Ñ P̃ Q̃ R̃ S̃ T̃ W̃ X̃ Ỹ Z
0x101.....: 0̸ 1̸ 2̸ 3̸ 4̸ 5̸ 6̸ 7̸ 8̸ 9̸ A̸ B̸ C̸ D̸ E̸ F̸ G̸ H̸ J̸ K̸ L̸ M̸ N̸ P̸ Q̸ R̸ S̸ T̸ W̸ X̸ Y̸ Z̸
0x110.....: 0̂ 1̂ 2̂ 3̂ 4̂ 5̂ 6̂ 7̂ 8̂ 9̂ Â B̂ Ĉ D̂ Ê F̂ Ĝ Ĥ Ĵ K̂ L̂ M̂ N̂ P̂ Q̂ R̂ Ŝ T̂ Ŵ X̂ Ŷ Z
0x111.....: 0̈ 1̈ 2̈ 3̈ 4̈ 5̈ 6̈ 7̈ 8̈ 9̈ Ä B̈ C̈ D̈ Ë F̈ G̈ Ḧ J̈ K̈ L̈ M̈ N̈ P̈ Q̈ R̈ S̈ T̈ Ẅ Ẍ Ÿ Z
```

The main problem with the notation is that the visibility of the diacritics
is very font dependent and is likely indiscernible or badly displayed with many fonts.

## Examples
As an example, the low weight irreducible polynomials above would be represented as follows with the proposed byte alphabet
(you should be able to see a tilde on top of D and 7 and an underscore under B):
```
8  : 0y1T (none)
16 : 0y10B̲ (underline)
32 : 0y1000D̃ (tilde)
64 : 0y10000000T (none)
128: 0y10000000000000007̃ (tilde)
256: 0y10000000000000000000000000000004R (none)
512: 0y1000000000000000000000000000000000000000000000000000000000000001R (none)
```
As you can see, a byte alphabet would make these bitstring sizes more manageable.

## Applications
The data sizes displayed above are not uncommon anymore.
For example, the [AVX-512](https://en.wikipedia.org/wiki/AVX-512) SIMD extension adds support for 32 registers of 512 bits,
together with their 256 and 128 bits sub-registers. With this alphabet, these registers can be addressed with one symbol and their content can be displayed with half the space. 




# Typing the byte alphabet

The downside of using an alphabet based on symbol combinations with diacritics
is that the standard keyboard cannot just type any symbol with one stroke anymore.
While there are standardized keyboard to insert diacritics from different languages,
these actually type dedicated characters with diacritics
and not the general composition of any diacritic with any other character.
For this generalized diacritics there is no standardized typing solution
and the fonts displaying them are generally not implemented correctly or not fully readable.
The goal of this section is to outline my solution to the typing problem using the Compose key.

## Problems with writing diacritics


Inputting diacritics will always be tricky.
Already typing special characters or other alphabets efficiently will require a good setup and multiple keystrokes per character.
In addition to that, diacritics additional complexity may include:
  * At least in Unicode, diacritics are to be placed after the character, meaning they act on the **previous** characters.
    However, even in supporting fonts, some diacritics may act on the **next** character.
    Therefore for certain font-software combination and for some diacritics,
    a choice must be made on whether to type them so that they are displayed "correctly" or typed correctly.  
    Notice that if you decide to put a diacritics in front of a character so that it displays correctly,
    but this character is the first one in a string, line or text, you might get unpredictable behaviour.
  * The diacritics alone might be rendered invisible (instead of using a temporary symbol until the next character is written)
  * Even though you correctly set up you key combinations to write diacritics,
    the program you are writing them in might not support them or even remove them (e.g. as part of input sanitation)
  * supporting fonts might not be accurately designed or rendered,
    so that even diacritics that are supposed to be above or below the characters
    might end up severely overlapping with the character and end up nearly invisible
  * the hex values of diacritics change depending on the encoding (e.g. UTF-8 vs UTF-16)

These are only some of the problems that I encountered and remembered to write down.
I am sure that many more are lurking out there, therefore, for the time being, software and font choices are crucial.

Current font of choice (displays correctly): **RobotoMono Nerd Font (Regular)** (fair visibility, but the tilde still has a lot of overlap)



## Typing diacritics with Compose Key

Many solutions online for writing unicode characters are explained without context or are incomplete, meaning for example:
  * solution that do not mention anything about where they apply may implicitly be written for Windows;
  * solutions written for Linux that do not involve Compose key, may be written only for Gnome or KDE;
  * solutions with Compose key do not usually explain how to handle diacritics.

So I decided to add my .XCompose file to this repository.
Below is the excerpt relevant to diacritics ready to copy-paste.
It is composed of two parts:
* a commented part storing the hex values of the diacritics
* the actual compose sequence of the diacritics

A full explanation of the two parts is given after the code.

```
# Combining symbols
# ⋅ combining symbol position depends on the diacritic, font and program:
#   it can go either *before* or *after* but predictably
# ⋅ string or file cannot start with combining symbol?
# ⋅ UTF8 and UTF16 symbols are different
# ⋅ UTF8[<character>] - UTF16[<character>] = 0xC920
# ⋅ python    uses UTF16
# ⋅ alacritty uses UTF8
#
# Diacritics:
#                                UNICODE
#                         UTF-8  UTF-16 Position in SauceCodePro Nerd Font (relative to character)
# circumflex (hat)     ^: 0xCC82 0x0302  before
# tilde                ~: 0xCC83 0x0303  before
# overline             ¯: 0xCC85 0x0305  before
# diaeresis/umlaut     ": 0xCC88 0x0308  before
# ring above           ˚: 0xCC8A 0x030A  before
# low line/underscore  _: 0xCCB2 0x0332  after
# long stroke overlay  -: 0xCCB6 0x0336  after
#   (strikethrough)
# long solidus overlay /: 0xCCB8 0x0338  after
#   (slash)
#
# How to write 0x<hex>:
#   - In Python/C/C++/Java:    u"\u<UTF16 hex>"
#   - In terminal:  echo "\x<UTF8 hex pair 1>\x<UTF8 hex pair 2>..."
#                   (split the hex in pairs preceded by \x)
<Multi_key> <c> <m> <asciicircum> <asciicircum>:"\xCC\x82" UCC82  # "\"\\u0302\"" U0302  # "\u0302" U0302
<Multi_key> <c> <m> <asciitilde>:               "\xCC\x83" UCC83  # "\"\\u0303\"" U0303  # "\u0303" U0303
<Multi_key> <c> <m> <asciicircum> <minus>:      "\xCC\x85" UCC85  # "\"\\u0305\"" U0305  # "\u0305" U0305
<Multi_key> <c> <m> <asciicircum> <underscore>: "\xCC\x85" UCC85  # "\"\\u0305\"" U0305  # "\u0305" U0305
<Multi_key> <c> <m> <quotedbl>:                 "\xCC\x88" UCC88  # "\"\\u0308\"" U0308  # "\u0308" U0308
<Multi_key> <c> <m> <o>:                        "\xCC\x8A" UCC8A  # "\"\\u030A\"" U030A  # "\u030A" U030A
<Multi_key> <c> <m> <underscore>:               "\xCC\xB2" UCCB2  # "\"\\u0332\"" U0332  # "\u0332" U0332
<Multi_key> <c> <m> <minus>:                    "\xCC\xB6" UCCB6  # "\"\\u0336\"" U0336  # "\u0336" U0336
<Multi_key> <c> <m> <slash>:                    "\xCC\xB8" UCCB8  # "\"\\u0338\"" U0338  # "\u0338" U0338
```

The explanation for the hex values and the compose sequences follows in the next sections below.





## The hex values of the diacritics

The following table is kept for reference as comment in the XCompose.
```
# Diacritics:
#                                UNICODE
#                         UTF-8  UTF-16  Position in SauceCodePro Nerd Font (relative to character)
# circumflex (hat)     ^: 0xCC82 0x0302  before
# tilde                ~: 0xCC83 0x0303  before
# overline             ¯: 0xCC85 0x0305  before
# diaeresis (umlaut)   ¨: 0xCC88 0x0308  before
# ring above           ˚: 0xCC8A 0x030A  before
# low line (underscore)_: 0xCCB2 0x0332  after
# long stroke overlay  -: 0xCCB6 0x0336  after
#   (strikethrough)
# long solidus overlay /: 0xCCB8 0x0338  after
#   (slash)
```

The hex values were taken from [fileformat.info](https://www.fileformat.info/info/unicode)
To find them again in the website, take the ```name``` above without the content of parenthesis
(e.g ```circumflex``` for the first element in the table below) and search ```combining name```
(e.g.```combining circumflex```) in [fileformat.info](https://www.fileformat.info/info/unicode).

Notice how:
* UTF8 and UTF16 hex values are different
    (this is typical for UTF-8 because it encodes unicode into pairs of hex values,
    with the first one acting as a control pair,
    therefore many first position hex pairs are reserved as commands,
    making many codes different and sometimes even longer)
* ```0x<UTF-8 diacritic> - 0x<UTF-16 diacritic> = 0xC920```;
  namely the the UTF-8 values are just the UTF-16 values shifted by (added to) ```0xC920```

Position: an example of a font that does not display correctly is SauceCodePro Nerd Font.
The table shows in which position the diacritic must be with respect to the character
in order to display correctly with this font.
But again adapting the order to suit your font is a **bad idea**
(like any hack to "compensate" for a font).
The "fix" will not hold up to the text being used in other programs or by other people,
and will need to be reverted if the font gets fixed at some point.
Not to mention that if, in order to display a character correctly, you place a diacritc at the beginning of a string, a line or a file, then you might get unpredictable behaviour.
Therefore it is much more sensible to put the effort in finding a better font.
One currently good choice seems to be RobotoMono Nerd Font, as mentione above.


### How to use the hex values

From what I gathered testing diacritics the only way to produce diacritics with the keyboard
is to use [ANSI escape sequences](https://gist.github.com/fnky/458719343aabd01cfb17a3a4f7296797) (I don't know anything about this topic, essentially everything I know is written in this section).

Essentially, for what concerns us, ANSI escape sequences define
fixed length sequences to encode, in particular, hex and unicode values:
  * hex values: hex values are written in pairs as sequences of ```\x..```
                where each dot denots one hex symbols, e.g. ```"\x01\x23\x45\x67\x89\xAB\xCD\xEF"```
  * unicodes: ```\u....``` followed by the four hex symbols, e.g. ```"\u0123"```

When the unicode character is provided as ```\u....``` there is no ambiguity, for example
  * ```"L\u0338L"``` = ```L̸L  ```: the unicode/UTF-16 renders correctly
  * ```"L\uCCB8L"``` = ```L첸L```: the UTF-8 code just renders another character

However, if we present a unicode characters as ```\x..\x..``` four things can happen
  * The two hex pairs are interpreted as UTF-8:  
    ```"L\x03\x38L"``` as UTF8  = ```L8L    ```: the unicode/UTF-16 code will not work  
    ```"L\xCC\xB8L"``` as UTF8  = ```L̸L     ```: success!!
  * The two pairs are interpreted as two unicode/UTF-16 characters in the form ```\u00..```  
    ```"L\x03\x38L"``` as UTF16 = ```L\x038L```  
    ```"L\xCC\xB8L"``` as UTF16 = ```LÌ¸L   ```
    neither will work because the codes are alway wrong.


There are thus only three ways to write diacritics
  * Paste the symbols directly, e.g. ```L̸L```
  * Unicode/UTF-16 ```"\u...."```, e.g. ```"L\u0338L"```
  * UTF-8 ```"\x..\x.."```, e.g. ```"L\xCC\xB8L"```

but which one to use? well, to quote Geralt of Rivia: "ah, fuck!"


### Where to use which values

Recognized encodings **as a string**:
  * C/C++: all three
  * Python/Java: copy and ```"L\u0338L"```
    * For example: ```'L̸L' == u"L\u0338L"``` returns ```True```
  * Rust: copy and ```"L\u{0338}L"``` (but with braces)
  * alacritty: all three
    * Example: ```echo "L̸L L\u0338L L\xCC\xB8L"``` outputs ```L̸L L̸L L̸L```
    * Note: in the command line (and only in the command line, not in the output)
      The unicode symbols are not displayed, namely
      ```echo "L̸L L\u0338L L\xCC\xB8L"```
      will be displayed as 
      ```echo "L<0338>L L\u0338L L\xCC\xB8L"```
      with ```<0338>``` highlighted and behaving as a single character.

Recognized console **input**:
  * Python console:
    * copy
    * ```"L\xCC\xB8L"``` from **compose key**
  * alacritty:
    * copy
    * ```"L\xCC\xB8L"``` from **compose key**

    however ```L<0338>L``` is displayed instead.





## The compose sequences of the diacritics

The following are my working compose sequences for the diacritics.
The way they behave is outlined in the section above explaining [the hex values](#the-hex-values-of-the-diacritics))
```
<Multi_key> <c> <m> <asciicircum> <asciicircum>:"\xCC\x82" UCC82  # "\"\\u0302\"" U0302  # "\u0302" U0302
<Multi_key> <c> <m> <asciitilde>:               "\xCC\x83" UCC83  # "\"\\u0303\"" U0303  # "\u0303" U0303
<Multi_key> <c> <m> <asciicircum> <minus>:      "\xCC\x85" UCC85  # "\"\\u0305\"" U0305  # "\u0305" U0305
<Multi_key> <c> <m> <asciicircum> <underscore>: "\xCC\x85" UCC85  # "\"\\u0305\"" U0305  # "\u0305" U0305
<Multi_key> <c> <m> <quotedbl>:                 "\xCC\x88" UCC88  # "\"\\u0308\"" U0308  # "\u0308" U0308
<Multi_key> <c> <m> <o>:                        "\xCC\x8A" UCC8A  # "\"\\u030A\"" U030A  # "\u030A" U030A
<Multi_key> <c> <m> <underscore>:               "\xCC\xB2" UCCB2  # "\"\\u0332\"" U0332  # "\u0332" U0332
<Multi_key> <c> <m> <minus>:                    "\xCC\xB6" UCCB6  # "\"\\u0336\"" U0336  # "\u0336" U0336
<Multi_key> <c> <m> <slash>:                    "\xCC\xB8" UCCB8  # "\"\\u0338\"" U0338  # "\u0338" U0338
```
Output codes behaviour in alacritty:
* ANSI ```"\x..\x.."``` UTF-8     : correctly outputs the diacritics, seems like the only working option
* ANSI ```"\u...."```             : outputs text ```u....``` regardless of the code, it is not interpreted
* ANSI ```"\"\\u....\""``` UTF-16 : outputs text ```"\u...."```
  * ```"\u...."``` is processed correctly by the terminal commands like ```echo``` but it is still text
  * ```"\u...."``` in vim is just ```"\u...."``` in text

Besides this, I made the following design choices:
* each sequence contains ```c```+```m``` for "combine",
  it was the quickest way to implement them
  while being fairly certain that I did not overwrite other bindings
* The final key in the sequence is the ascii version of the diacritic,
  except for overline (```^```+```-``` or ```^```+```_```)
  and ring above (the latin letter ```o```)


### Where the compose keys work
Works for me:
* alacritty, but in the command line the UTF-16 hex code is displayed,
  namely ```echo L̸L``` is displayed as ```echo L<0338>L``` with ```<0338>``` highlighted in the command line,
  but the output of ```echo L̸L``` is still displayed as ```L̸L```;
* console programs in alacritty: vim

Partially works:
* Firefox and Thunderbird: cannot type directly but can copy them in (but not with fixed width font in Thunderbird)
* Gedit: same but the diacritic is displayed as its own character although it is not sanitized, you can copy the diacritic back out intact
* Evince search field: input interpreted as UTF-16, correct string can still be copied in correctly

Feel free to test them on your everyday programs and report back!
For example, in Firefox, both in the address bar or in Google search field, I tried the following compose sequences (```f```+```t``` stands for **f**irefox **t**est) and obtained the strings commented out on the right:
```
<Multi_key> <f> <t> <1>:  "\xCC\xB8"    # LÌ¸L
<Multi_key> <f> <t> <2>:  "\"\\u0338\"" # L"\u0338"L
<Multi_key> <f> <t> <3>:  "\u0338"      # LL
<Multi_key> <f> <t> <4>:   "+0338"      # L+0338L
<Multi_key> <f> <t> <5>:  "U+0338"      # LU+0338L
<Multi_key> <f> <t> <6>:  "%03%38"      # L%03%38L
<Multi_key> <f> <t> <7>:  "%CC%B8"      # L%CC%B8L
<Multi_key> <f> <t> <8>:  "&#0338"      # L&#0338L
<Multi_key> <f> <t> <9>:  "0x0338"      # L0x0338L
```

### The rest of the compose file
The rest of the file contains:
* greek alphabet (with different layout based on the name of the greek character,
  e.g. ```d```+```e``` for ```δ``` (**de**lta) and ```D```+```e``` for ```Δ``` (**De**lta)
* double stroke numbers and latin letters (used for additional notation, e.g. ```0y𝔽 = 0xFF```)
* math symbols (eg
  ```s```+```u```+```m``` for ```∑```,
  ```k```+```e```+```t``` for ```⟩```,
  ```b```+```r```+```a``` for ```⟨```,
  etc)
* name table for some symbols (```<asciicircum>``` for ```^```, ```<minus>``` for ```-```, etc)

