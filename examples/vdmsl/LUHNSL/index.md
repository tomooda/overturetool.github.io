---
layout: default
title: LUHN
---

~~~
Luhn algorithm
The Luhn algorithm or Luhn formula, also known as the "modulus 10" or "mod 10" algorithm, is a simple
The algorithm is in the public domain and is in wide use today. It is specified in ISO/IEC 7812-1.[1]
~~~
###LUHN.vdmsl

{% raw %}
~~~
/**
functions
  -- Convenience function for "12345"
  -- Convenience function for numbers
  total: seq of Digit -> nat
  slen: seq of Digit -> nat
  strToSeq: seq1 of char -> seq1 of Digit
  natToSeq: nat -> seq of Digit
  id: nat -> nat
traces
  /**
  AllAdjacentTranspositions:
--  AllTwoDigitErrors:
  /**
  /**
operations
  checkOK: seq1 of Digit * Digit ==> bool

~~~{% endraw %}
