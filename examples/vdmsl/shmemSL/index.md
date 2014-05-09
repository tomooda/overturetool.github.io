---
layout: default
title: shmem
---

~~~
This example was produced by Nick Battle and it is used in the VDMJ user
The specification output indicates which allocation policy, first-fit or 
#******************************************************
~~~
###shmem.vdmsl

{% raw %}
~~~
module M
Quadrant = seq of M;
M :: type : <USED> | <FREE>

state Memory of
end
values
MAXMEM = 10000;
functions
sizeof: M -> nat1
least: nat1 * nat1 -> nat1
spacefor: nat1 * Quadrant -> nat1
QuadrantLen:  nat1 * Quadrant -> nat
bestfit: nat1 * Quadrant -> nat1
add: nat1 * nat1 * Quadrant -> Quadrant
QuadrantLen2: nat1 * nat1 * Quadrant -> nat
combine: Quadrant -> Quadrant
QuadrantLen0: Quadrant -> nat
delete: M * Quadrant -> Quadrant
MQuadrantLen: M * Quadrant -> nat
fragments: Quadrant -> nat
operations
seed: nat1 ==> ()
inc: () ==> ()
rand: nat1 ==> nat1
FirstFit: nat1 ==> bool
BestFit: nat1 ==> bool
Reset: () ==> ()
DeleteOne: () ==> ()
TryFirst: nat ==> nat
  while count < loops and FirstFit(rand(CHUNK)) 
  -- return count;
TryBest: nat ==> nat
  while count < loops and BestFit(rand(CHUNK)) 
  -- return count;
main: nat1 * nat1 ==> seq of (<BEST> | <FIRST> | <SAME>)
  for i = 1 to tries 
     Reset();
     Reset();
     if best = first
  return result;
end M
~~~{% endraw %}
