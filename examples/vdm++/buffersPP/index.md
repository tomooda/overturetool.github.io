---
layout: default
title: buffers
---

~~~
This model is made by Yves Ledru et al. in a paper illustrating the
Filtering TOBIAS Combinatorial Test Suites, Yves Ledru, Lydie du 
#******************************************************
~~~
###buffers2.vdmpp

{% raw %}
~~~

class Buffers

instance variables
  b1 : nat := 0;
inv b1 + b2 + b3 <= 40 and b1 <= b2 and b2 <= b3 and b3 - b1 <= 15
operations
public Add: nat ==> ()
public Remove: nat ==> ()
public getBuffers: () ==> nat * nat * nat
end Buffers
instance variables
  b : Buffers := new Buffers()
traces
S1: let x in set {1,...,5} in b.Add(x); b.getBuffers()
S1': b.Add(1); (b.Add(2) | b.Add(3)); b.Add(4)
S2: b.Add(2); ((let x in set {1,...,5} in b.Add(x)) |
S3: b.Add(5){7}; ((let x in set {1,...,5} in b.Add(x)) |
S4: let x in set {1,...,5} in b.Add(x); 
end UseBuffers

~~~{% endraw %}
