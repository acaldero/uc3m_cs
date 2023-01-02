## Materials used for Computer Structure

<html>
<h2><ul>
<li>License <a href="http:/creativecommons.org/licenses/by-nc/4.0/">CC BY-NC 4.0</a> </li>
<li>Curse 2022-2023</li>
</ul></h2>
</html>


### Exercise 1

   (statement) The following numbers are represented in two’s complement using 6 bits.
   Indicate their corresponding decimal value:
   * 100000
   * 010011

   (solution) The corresponding decimal value:
   * 100000: - (011111 + 1) = -32
   * 010011: +16+2+1 = 19

### Exercise 2

   (statement)
<html>
A computer has a word width that allows you to represent numbers in complement to two in the range [-234, 234-1].
Respond:
<ol type="a">
  <li>What is the number of bits that store the registers of this computer?</li>
  <li>How much KB of memory can address at most this computer?</li>
</ol>
</html>

   (solution)
<html>
For this computer:
<ol type="a">
  <li>[2<sup>n-1</sup>...-1, 0... 2<sup>n-1</sup>-1] = [-234, 234-1] -> 2<sup>n-1</sup>=234 -> 9 bits</li>
  <li>If this is a 9 bits computer then 2<sup>9</sup> bytes (memory address by bytes) -> 2<sup>9</sup>/2<sup>10</sup> KiB -> half a kilobyte</li>
</ol>
</html>

### Exercise 3

   (statement) Indicate the decimal value of the following numbers represented in the single precision IEEE 754 standard: 0xBF400000, 0x7F804000 and 0x00180000.

   (solution)
   * 0xBF400000 -> 1011 1111 0100 0000 0000... -> 1 01111110 100000000... -> -1.1 * 2<sup>-1</sup> -> 0,110 -> -0,75
   * 0x7F804000 -> 0111 1111 1000 0000 0100... -> 0 11111111 000000001... -> NaN
   * 0x00180000 -> 0000 0000 0001 0100 0000... -> 0 00000000 001010000... -> no-normalize: +0.001100.. x 2<sup>-126</sup>

### Exercise 4

   (statement) Represent in the single precision IEEE 754 standard the numbers 15 and 3,75.

   (solution) The corresponding value:
   * 15   -> 8+4+2+1      -> 1111.00 * 2<sup>0</sup> -> 1.1110 * 2<sup>3</sup> -> 0 10000010 111000...
   * 3.75 -> 2+1+0.5+0.25 ->   11.11 * 2<sup>0</sup> -> 1.1110 * 2<sup>1</sup> -> 0 10000000 111000...

### Exercise 5

   (statement) Add the previous numbers represented in the IEEE 754 standard using the IEEE 754 representation.

   (solution) The corresponding value:
```
                                 1 11
   * 15    <-> 1.1110 * 2^3 <->  1.111000 * 2^3
   *  3.75 <-> 1.1110 * 2^1 <->  0.011110 * 2^3
   * 18.75                      10.010110 * 2^3 -> 10010.11
```
