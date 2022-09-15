## Materials used at ARCOS.INF.UC3M.ES under [CC BY-NC 4.0](http://creativecommons.org/licenses/by-nc/4.0/)

## Computer Structure (2022-2023)

### Exercise 1

   (statement) Convert the following 16-bit binary number to hexadecimal: 1101001011101011

   (solution) 1101001011101010 -> 1101 0010 1110 1011 -> 0xD2EB

### Exercise 2

   (statement) Convert the following hexadecimal number to binary: F73AB592

   (solution) F73AB592 -> 1111 0111 0011 1010 1011 0101 1001 0010

### Exercise 3

   (statement)
<html>
Consider a hypothetical computer with a word width of 24 bits with 55 registers that addresses the memory by bytes.<br>
Answer the following questions:<br>
<ol type="a">
  <li>How many bits are used for the memory addresses?</li>
  <li>What is the size of the registers?</li>
  <li>How many bits are stored in each memory location?</li>
  <li>How many memory locations can be addressed? Express the result in KiB.</li>
  <li>How many bits are needed to identify the registers?</li>
</ol>
</html>

   (solution)
<html>
Consider a hypothetical computer with a word width of 24 bits with 55 registers that addresses the memory by bytes.<br>
Answer the following questions:<br>
<ol type="a">
  <li>24 bits are used (the word-width of the computer if no other particular information is given).</li>
  <li>24 bits (the word-width if no other particular information is given).</li>
  <li>In each memory position is stored a byte because the memory is addressed by bytes.</li>
  <li>You can address 2^24 memory locations. In each memory position is stored a byte.<br>
      Then the memory size is: 2^24 bytes => 2^24 / 2^10 = 2^14 = 16*1024 KiB.
  </li>
  <li> As there are 55 registers, it is necessary to have round_ex(log2(55)) = 6 bits.</li>
</ol>
</html>

