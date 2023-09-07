
+ Authors: **Alejandro Calderón Mateos & Felix García Carballeira**
+ License: [GPLv3.0](https://github.com/wepsim/wepsim.github.io/blob/master/LICENSE)


# Laboratory 1: assembly, power-consumption and security

The main goal of the proposed laboratory is to understand the concepts related to assembly programming, but also the impact of power-consumption in security. For this purpose we are going to use the RISC-V assembler.
In order to become familiar with assembly programming and simulator used, it is recommended to solve the examples available in the simulator.

This laboratory consists of 3 exercises that you can develop and test in <a href="https://wepsim.github.io/wepsim/">WepSIM</a>.


## Exercise 1
The goal of this exercise is to develop in RISC-V<sub>imf32</sub> assembler a function called **`string_compare`** to work with strings:
```
Function string_compare ( char A[], char B[] ) ;
```

This function allows to compare two strings so that it is possible to know if the strings stored in memory are the same or not.

This function receives the following arguments in the order given:
  * Argument 1: (A) starting address of a string that ends with the ASCII code 0.
  * Argument 2: (B) starting address of a string ending in end of string (ASCII code 0).

The function returns a single integer that takes one of these three possible values:
  * On error, it returns the integer -1.
  * If the two strings are the same, it returns the integer 1 (one). 
  * If the two strings are different, it returns the integer 0 (zero).

The following figure illustrates an example when the content of two strings is different:
```
.data
  A: .string "uno"  # 'u', 'n', 'o', '\0'
  B: .string "dos"  # 'd', 'o', 's', '\0'

.text

 string_compare:
       ...
       jr ra

 main: 
       la a0 A
       la a1 B
       jal ra string_compare
       #      <-   a0 must be 0 at this point because are differente string
       ...
```


The following figure illustrates an example when the content of two strings that are equals:
```
.data
  A: .string "uno"  # 'u', 'n', 'o', '\0'
  B: .string "uno"  # 'u', 'n', 'o', '\0'

.text

 string_compare:
       ...
       jr ra

 main: 
       la a0 A
       la a1 B
       jal ra string_compare
       #      <-   a0 must be 1 at this point because are the same string
       ...
```

The two possible errors to be considered in this function are that address A is null (zero value) and that address B is null (zero value).

In the `string_compare` function, in case of finding an error, it must return only the value -1 without doing anything else. In the same way, the function must compare character by character and as soon as it is a different one it must return 0. 

The following figure illustrates an example when an error ocurrs:
```
.data
  A: .string "uno"  # 'u', 'n', 'o', '\0'
  B: .string "dos"  # 'u', 'n', 'o', '\0'

.text

 string_compare:
       ...
       jr ra

 main: 
       li   a0 0
       move a1 x0
       jal ra string_compare
       #      <-   a0 must be -1 at this point because an error happens
       ...
```



## Exercise 2
The goal of this exercise is to study the impact of number of clock cycles when using the `string_compare` function, especially its use for a possible side-channel attack:
  * Because more clock cycles needed by a function should be directed related to the power consumption in a normal CPU, we can know the input, output and the related power consumption for `string_compare`.
  * In this program, the `rdcycle rd` RISC-V pseudoinstruction is used.
This instruction stores in `rd` the number of cycles that have been executed so far.

Imagine that a security company uses the `string_compare` function of Exercise 1 to check if an user's stored key (`stored_key`) is the same as the key that the user enters on the keyboard to authenticate.

To test such a function, design and implement a program that performs the following actions:
  1. The user introduces the key by keyboard and it is stored in `user_key`.
  2. The `string_compare` function is called to check that the key `user_key` entered by keyboard is valid by comparing it with the user's key that is stored in `stored_key`, so if it returns 1 it is valid and if it returns 0 it is an invalid key.
  3. A valid or invalid message is printed on the screen.

The following code fragment shows the skeleton of this program:
```
.data
    stored_key:     .string   "one"
    user_key:       .zero     9    
    valid_msg:      .string   "Valid"
    no_valid_msg:   .string   "Invalid"

.text
main:     
            ...
            # <- read the user key from keyboard and store in user_key

            # call to string_compare(stored_key, user_key)
            ...
            jal ra string_compare
            mv  t1 a0         # t1: 1 ok and 0 not valid

            
            beq zero a0 print_no
print_yes:  la  a0  valid_msg
            j end
print_no:   la  a0 no_valid_msg
end:        li  a7 4
            ecall
```

As an internship student of this company, we suspect that when comparing the key "one" with a string "a" the function only makes one single comparison between letters ('o' versus 'a'), but when comparing "one" with the string "o" the function makes two comparisons ('o' is equal to 'o' and 'n' is not equal to the end of the string). This causes the number of cycles executed and, therefore, the power consumption when the first letter is matched to be higher. 

To demonstrate this hypothesis, we initially propose the following program skeleton:
```
.data
    valid_msg:      .string   ":Valid:"
    no_valid_msg:   .string   ":Invalid:"

    stored_key:     .string  "one"
    possible_key:   .string  "a"

.text
main:  ...
       # Obtain the cycles executed so far
       rdcycle	t0

       # call ro string_compare (stored_key, possible_key)
       ...
       jal ra string_compare
       mv  t1 a0              # t1: 1 ok y 0 not valid

       # Obtain the cycles executed so far
       rdcycle  t2
       sub t0 t2 t0           # t0: Number of elapsed cycles 

       # Print messages
       beq zero t1 p_no
p_yes: la  a0 valid_msg
       j end
p_no:  la  a0 no_valid_msg
end:   li  a7 4
       ecall

       # Print the number of cycles 
       mv a0 t0
       li a7 1
       ecall
       ...
```

The objective of this exercise is to modify the previous program to calculate the number of cycles (power consumption) for letters 'a' to 'z' as the first character of the key. That is, it is to find out the power consumption (number of cycles) for the following values of possible_key: 'a', 'b' ... 'z'. Only the 27 lowercase letters of the alphabet. 

**Note, that possible_key is a string, i.e. when you want to test with the letter 'k', the string will have the value "k", which is equivalent to having two characters in the string: one the ASCII code of the 'k' and then the code 0 indicating the end of the string. It is recommended to study how the characters 'a'...'z' are stored using the ASCII code.**

For this purpose, the function has to be developed: 
```
Function study_energy ( char password[], char dummy[] ) ;
```

This function prints in each line, for each of the letters, the following information:
```
letter: number of cycles.
```

For example, a possible output would be this:
```
a: 10
b: 10
c: 10
d: 20
e: 10
.
.
z: 10
```

Note that in this case the key starts with the letter d, since the number of cycles in this case is higher.

This function receives the following arguments in the given order:
  * Argument 1: (password) starting address of a string with the key to be discovered. Like all strings, it ends with the ASCII code 0 used as the end of the string.
  * Argument 2: (dummy) starting address of a string in memory. This string will always include a single character (in memory it will occupy two bytes: the ASCII code of the letter and the ASCII code 0 used as the end of the string).

The function does not return any value, it simply prints on the console a line for each letter of the alphabet with the format indicated above:
```
letter: number of cycles
```

It is mandatory to correctly follow the parameter passing convention described in the course for RISC-V, as well as to respect the function signature (name, number of parameters, order of parameters and value to be returned). Similarly, the **study_energy** function must use the **string_compare** function of the first exercise (it must call this function).

It will not be considered valid to develop the code of the functions directly in the main function. You must write the code corresponding to the requested function as a separate function.


## Exercise 3
The goal of this exercise is to implement a simple function that performs a **side-channel attack**.

**Consider that the keys are at most 8 characters for the study**. 
Through **a brute-force attack**, we would **have to test up to 27<sup>8</sup> (282,429,536,481) possible keys**. 

**But with a side-channel attack**, it would be possible to detect by using the energy consumption (number of cycles executed) the first character of the key, and once this character is fixed, it would be possible to study the 27 possible characters for the second letter and so on. In other words, **possible combinations are reduced to 27*8 (216 possibilities), in case the key is just 8 characters long**.

In Exercise 3, we have to implement in assembler RISC-V<sub>32IMF</sub> a function called `attack` to discover a possible key of up to 8 characters:
```
Function attack ( char password[], char dummy[] ) ;
```

This function receives the following arguments in the provided order:
  * Argument 1: (password) starting address of the user key to be discovered. This string ends with the ASCII code 0 used as the end of the string.
  * Argument 2: (dummy) starting address of a string in memory where the detected key will be stored. This string must have space for 9 bytes (8 of the string plus the end of the string).

The function does not return any value, it simply stores in dummy memory address the value of the discovered key. 

For the development of this exercise, you can start with the ideas of Exercise 2 and add everything necessary to perform the attack.

Note that this is an exercise, in a real scenario the contents of the user's password would never be known. However, the principle used ([side-channel attack](https://en.wikipedia.org/wiki/Side-channel_attack)) is the same that has inspired attacks on current processors such as [spectre](https://en.wikipedia.org/wiki/Spectre_(security_vulnerability)).


# Extra material
You can find extra material in this example within WepSIM: <a href="https://acaldero.github.io/wepsim/ws_dist/?mode=ep&examples_set=RISCV&example=21">Example 21</a>.

