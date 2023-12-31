# byte-alphabet

If you have just enough amount of programming,
you will know that multible alphabets exist to describe binary data:
the basic 0 or 1, octets 0 to 7, hexadecimals 0 to F, and of course decimals 0 to 9.
In particular, because the hexadecimals are the largest alphabets,
they are also the choice that makes for the shortest representation.

For certain applications however, in particular security, data chunks of considerable size,
e.g. 128 bits and above, are used both theoretically and in practice (e.g. AES instruction set extension).
While still the shortest representation, hexadecimal representations of 128 bits and above
are still quite large and unmanageable in manual and direct inspection.
This is exacerbated by the fact that most of the time the number of bits of the data chunks are themselves powers of 2.

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

Having a full set of symbols for one by (two hex's), would at least mitigate this problem slightly.
Notice that for some applications like exactly displaying low weight numbers with many consecutive zeros,
the impact of such change would be minimal, as most of the symbols would still be zero.

## The byte alphabet
The full alphabet and design choices are explain in length in the text file duotrigentidecimal_numbers.txt.
The essence is the following: the 8 bits are separated into 3 + 5 bits
* 5 bits are assigned their own basic symbols, namely an extension of hex 0 to F to 32 symbols going from 0 to Z (I O U V are excluded)
* 3 bits are assigned to 7 different diacritics (000 corresponds to no diacritics, just the basic alphabet):
  * none, underline, strikethrough, overline
  * tilde, slash, circumflex (hat), dieresis (umlaut)

The main problem with the notation is that the visibility of the diacritics
is very font dependent and is likely indiscernible or badly rendered with many fonts.
As an example, the above hex strings would be represented as follows with the proposed byte alphabet (where indeed the tilde's are not displayed properly):
```
8  : 0y1T (none)
16 : 0y10B̲ (underline)
32 : 0y1000 ̃D (tilde)
64 : 0y10000000T (none)
128: 0y1000000000000000 ̃7 (tilde)
256: 0y10000000000000000000000000000004R (none)
512: 0y1000000000000000000000000000000000000000000000000000000000000001R (none)
```
