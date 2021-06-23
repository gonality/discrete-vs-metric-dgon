# Code and figures to accompany the paper "Discrete and metric divisorial gonality can be different"

This repository contains additional material accompanying the paper [DSW21], including more figures and instructions for reproducing our computational results.
Contents:

   0. Links to the relevant source code;
   1. Instructions to verify the counterexamples from [DSW21, Figure 4];
   2. Drawings of several examples with more than 3 cycles on the outer ring, and instructions to compute the corresponding gonalities;
   3. Drawings of all 29 simple counterexamples on 10 vertices, and instructions to reproduce this list;
   4. Instructions to verify the Brill–Noether conjecture for all simple graphs on at most 13 vertices.


## 0. Where to find the code
For gonality computations, we use the programs `find_gonality`, `subdivision_conjecture` and `Brill_Noether_geng` from [dgon-tools](https://github.com/gonality/dgon-tools/).
To generate graphs, we sometimes use the program `geng` from the `gtools` suite packaged with `nauty`; see [MP20].
For instructions to compile these programs, please refer to the documentation of those projects.


## 1. Verifying the examples from [DSW21, Figure 4]
In [DSW21, Figure 4], a total of 8 counterexamples are shown.
To verify that each of these is a counterexample, run
```
subdivision_conjecture -vv < Figure_4.in
```


## 2. More than 3 cycles on the outer ring
We also considered graphs where the outer ring consists of n cycles for some n ≥ 3.
Some of these resulted in a counterexample, some didn't.
Examples can be found in `more_cycles_on_the_outer_ring.pdf`.

To reproduce these results, run
```
subdivision_conjecture -vv < more_cycles_on_the_outer_ring.in
```


## 3. The 29 simple counterexamples on 10 vertices
We have tested the 2-subdivision conjecture for all connected simple graphs on at most 10 vertices.
We found that there are no counterexamples with ≤ 9 vertices, and exactly 29 counterexamples with 10 vertices.
These counterexamples are depicted in the file `29_counterexamples.pdf`.

This result can be reproduced by running
```
# Test the conjecture for connected simple graphs on 9 vertices (no counterexamples)
geng -cl 9 graphs-9.g6
subdivision_conjecture -g < graphs-9.g6

# Test the conjecture for connected simple graphs on 10 vertices (29 counterexamples)
geng -cl 10 graphs-10.g6
subdivision_conjecture -g < graphs-10.g6
```
Warning: this computation took several weeks, although all counterexamples were found within the first few days.



## 4. Testing the Brill–Noether conjecture
We tested the gonality conjecture dgon(G) ≤ ⌊(g+3)/2⌋ for all simple graphs G on at most 13 vertices.
We found no counterexamples.
This can be reproduced by running
```
Brill_Noether_geng -v 13
```
Warning: this computation took approximately 8000 CPU hours.
The program `Brill_Noether_geng` is capable of dividing the task into smaller subtasks.
We divided this task into 48 subtasks, of which we ran 8 at a time on an Intel(R) Xeon(R) CPU E3-1240 V2 @ 3.40GHz.
Each set of 8 simultaneous subtasks took about a week, so the entire computation lasted about 6 weeks.
The exact command we used is the following:
```
Brill_Noether_geng -v 13 $i/48
```
where `$i` is an integer in the range 0,...,47 denoting the number of the current subprocess.



## References

  [DSW21]: Josse van Dobben de Bruyn, Harry Smit, and Marieke van der Wegen. *Discrete and metric divisorial gonality can be different*, preprint, 2021.
  
  [MP20]: Brendan D. McKay and Adolfo Piperno, *nauty and Traces*, version 2.7r1, 2020. https://pallini.di.uniroma1.it.
