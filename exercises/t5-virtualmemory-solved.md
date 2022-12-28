## Computer Structure

<html>
<h2><ul>
<li>License <a href="http:/creativecommons.org/licenses/by-nc/4.0/">CC BY-NC 4.0</a> </li>
<li>Curse 2022-2023</li>
</ul></h2>
</html>


### Exercise 1

   (statement)
<html>
Let be a 20-bit computer with virtual memory paged with 1 KiB pages and a total physical memory of 512 KB.<br>.
It is asked, in a reasoned and brief form:<br>
<ol type="a">
<li>What is the format of the virtual address? Indicate the fields and the number of bits in the fields.</li>
<li>What is the maximum number of page table entries (one level)?</li>
<li>How many page frames does the main memory have?</li>
<li>What are the fields that are included in a page table entry? Also indicate what each of the fields is used for.</li>
</ol>
</html>

   (solution)
<html>
<ol type="a">
<li>The size of each page is 1 KB = 2<sup>10</sup> bytes. Because the virtual address has 20 bits, to identify a page it is needed 20 - 10 = 10 bits.
Therefore, the format uses the upper 10 bits of the address for the page number and the lower 10 bits for the offset within the page.</li>
<li>The maximum number of entries in the page table coincides with the maximum number of pages, i.e.  2<sup>10</sup> = 1024 entries.</li>
<li>The number of page frames is given by 512 KB / 1 KB = 512 frames.</li>
<li>Each entry in the page table includes, among other things:
<ul>
<li>Presence bit</li>
<li>Modified bit</li>
<li>Validity bit</li>
<li>Field where the frame identifier is stored</li>
</ul>
</ol>
</html>

