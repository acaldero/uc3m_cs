## Materials used at ARCOS.INF.UC3M.ES under [CC BY-NC 4.0](http://creativecommons.org/licenses/by-nc/4.0/)

## Computer Structure (2022-2023)

### Exercise 1

   (statement) The following numbers are represented in two’s complement using 6 bits.
   Indicate their corresponding decimal value:
   * 100000
   * 010011
    
   (solution) The corresponding decimal value:
   * 100000: - (011111 + 1) = -32 
   * 010011: +16+2+1 = 19

### Exercise 2

   (statement) Represent in the single precision IEEE 754 standard the numbers 15 and 3,75.
    
   (solution) The corresponding value:
   * 15   -> 8+4+2+1      -> 1111.00 * 2^0 -> 1.1110 * 2^3 -> 0 10000010 111000...
   * 3.75 -> 2+1+0.5+0.25 ->   11.11 * 2^0 -> 1.1110 * 2^1 -> 0 10000000 111000...

### Exercise 3

   (statement) Indicate the decimal value of the following number represented in the single precision IEEE 754 standard: 0xBF400000.
    
   (solución) 0xBF400000 -> 1011 1111 0100 0000... -> 1 01111110 100000... -> -1.1 * 2^(-1) -> 0,110 -> -0,75

