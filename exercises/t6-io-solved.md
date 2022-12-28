## Materials used for Computer Structure

<html>
<h2><ul>
<li>License <a href="http:/creativecommons.org/licenses/by-nc/4.0/">CC BY-NC 4.0</a> </li>
<li>Curse 2022-2023</li>
</ul></h2>
</html>


### Exercise 1

   (statement)
It is desired to develop a controller for a traffic light.
The controller has a 32-bit CPU, separate I/O map and RISC-V 32 instruction set.
Two I/O modules are connected to this CPU.
The first is a timer and the second is the I/O module that controls the operation of the traffic light.

The chronometer module has the following three registers:
  * Register with address 1000. The value corresponding to the countdown in seconds is loaded into this register.
  * Register with address 1004. In this register a 1 is loaded when you want to start the countdown.
  * Register with address 1008. When the countdown reaches 0, a 1 is loaded into this register. While the countdown is counting down, the value of this register is 0.

The I/O module that controls the traffic lights has four registers:
  * Register with address 1012. In this register, the value corresponding to the color of the traffic light is coded: 100 for red, 010 for yellow and 001 for green.
  * Register with address 1016. It is a register that indicates the duration in seconds corresponding to red.
  * Register with address 1020. It is a register that indicates the duration corresponding to yellow, which occurs at the red-green transition.
  * Register with address 1024. It is a register that indicates the duration in seconds of green.

<html>
Se pide:<br>
<ol type="a">
<li>Write the assembler program that controls the operation of this traffic light. The traffic light always starts its operation on red.</li>
<li>What inefficiency is identified in the above program and how could it be resolved?</li>
</ol>
</html>

   (solution)
<html>
<ol type="a">
<li>
<pre>
RED:
	li 	t0, 100
	OUT 	t0, 1012
	IN 	t0, 1016
	OUT 	t0, 1000
	IN 	t0, 1
	OUT 	t0, 1004
WAIT4RED:
	IN 	t0, 1008
	li 	t1, 1
	beq 	t0, t1, WAIT4RED
YELLOW:
	li 	t0, 010
	OUT 	t0, 1012
	IN 	t0, 1020
	OUT 	t0, 1000
	IN 	t0, 1
	OUT 	t0, 1004
WAIT4YELLOW:
	IN 	t0, 1008
	li 	t1, 1
	beq 	t0, t1, ESPERA_AMARILO
GREEN:
	li 	t0, 010
	OUT 	t0, 1012
	IN 	t0, 1024
	OUT 	t0, 1000
	IN 	t0, 1
	OUT 	t0, 1004
WAIT4GREEN:
	IN 	t0, 1008
	li 	t1, 1
	beq 	t0, t1, WAIT4GREEN
	beq 	x0, x0, RED
<pre>
</li>

<li>
The main cause of inefficiency is CPU consumption during counter timeout. The solution would be the use of I/O through interrupts.
</li>
</ol>

</html>

