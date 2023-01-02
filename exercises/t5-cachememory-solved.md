## Materials used for Computer Structure

<html>
<h2><ul>
<li>License <a href="http:/creativecommons.org/licenses/by-nc/4.0/">CC BY-NC 4.0</a> </li>
<li>Curse 2022-2023</li>
</ul></h2>
</html>


### Exercise 1

   (statement)
<html>
A computer has the following features:<br>
<ul>
<li>MP block access time: 150 ns.</li>
<li>Cache access time: 5 ns.</li>
</ul>

Indicate:<br>
<ol type="a">
<li>With a 90% cache hit rate, what is the average memory access time?</li>
<li>iF the average access time is required to be less than 2 ns, what hit rates are needed?</li>
</ol>
</html>

   (solution)
<html>
<ol type="a">
<li>
𝑇<sub>m</sub> = 5*0.9 + (150+5)*0.1 = 4.5 + 15.5 = 20 ns
</li>
<li>
2 = 5*h + (150+5)*(1-h) => h = 153/150 => h>1.02<br>
But the hit ratio (h) must be a value between 0 and 1, so 1.02 means that is impossible to archive an average time of 2ns with a cache memory with 5ns of access time.
</li>
</ol>
</html>

