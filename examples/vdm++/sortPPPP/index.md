---
layout: default
title: sortPP
---

~~~
This VDM++ model is made by Peter Gorm Larsen in 2010 based on the original 
#******************************************************
~~~
###dosort.vdmpp

{% raw %}
~~~

class DoSort is subclass of Sorter
operations
  public Sort: seq of int ==> seq of int
functions
  DoSorting: seq of int -> seq of int
  InsertSorted: int * seq of int -> seq of int
  Len: seq of int -> nat
  Len: int * seq of int -> nat
end DoSort 

~~~{% endraw %}

###explsort.vdmpp

{% raw %}
~~~

class ExplSort is subclass of Sorter
operations
  public Sort: seq of int ==> seq of int
functions
  Permutations: seq of int -> set of seq of int
  RestSeq: seq of int * nat -> seq of int
  IsOrdered: seq of int -> bool
  Len: seq of int -> nat
end ExplSort

~~~{% endraw %}

###implsort.vdmpp

{% raw %}
~~~

class ImplSort is subclass of Sorter
operations
  public Sort: seq of int ==> seq of int
functions
  public ImplSorter(l: seq of int) r: seq of int
  IsPermutation: seq of int * seq of int -> bool
  IsOrdered: seq of int -> bool
end ImplSort

~~~{% endraw %}

###mergesort.vdmpp

{% raw %}
~~~

class MergeSort is subclass of Sorter
operations
  public Sort: seq of int ==> seq of int
functions
  MergeSorter: seq of real -> seq of real
  Len: seq of real -> nat
  Merge: seq of int * seq of int -> seq of int
  Len: seq of int * seq of int -> nat
end MergeSort


~~~{% endraw %}

###sorter.vdmpp

{% raw %}
~~~

class Sorter
operations
  public
end Sorter

~~~{% endraw %}

###sortmachine.vdmpp

{% raw %}
~~~


class SortMachine
instance variables


operations
  public SetSort: Sorter ==> ()
  public GoSorting: seq of int ==> seq of int  
  public SetAndSort: Sorter * seq of int ==> seq of int
traces
  DiffSorting: let srt in set {new DoSort(),new ExplSort(),new ImplSort(),
end SortMachine


~~~{% endraw %}
