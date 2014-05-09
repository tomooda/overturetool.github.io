---
layout: default
title: gateway
---

~~~
This example is for a trusted gateway made by John Fitzgerald and 
Peter Gorm Larsen, Tom Brookes, Mike Green and John Fitzgerald, 
J.S. Fitzgerald, T.M. Brookes, M.A. Green, and P.G. Larsen, Formal 
Peter Gorm Larsen, John Fitzgerald, Tom Brookes, Mike Green, Formal 
John Fitzgerald, Peter Gorm Larsen, Tom Brookes and Mike Green, 
Peter Gorm Larsen, John Fitzgerald and Tom Brookes, Lessons Learned 
T.M. Brookes, J.S. Fitzgerald, and P.G. Larsen, Formal and Informal 
#******************************************************
~~~
###gateway.vdmsl

{% raw %}
~~~
-- A trusted gateway
types
  String = seq of char
  Message = String
  Classification = <HI> | <LO>;
  Category = set of String;
  Ports :: high: seq of Message
functions
-- checking whether a substring occur in another string
  Occurs: String * String -> bool
-- Classifying messages
  Classify: Message * Category -> Classification

-- The main gateway function using recursion
  Gateway: seq of Message * Category -> Ports
   MesLen: seq of Message * Category -> nat
-- Classify the message and add to the appropriate port.
  ProcessMessage: Message * Category * Ports -> Ports

-- The main gateway function without using recursion
  Gateway2: seq of Message * Category -> Ports
-- Functions illustrating other sequence operators. 
  AnyHighClass: seq of Message * Category -> bool
  Censor: seq of Message * Category -> seq of Message
  FlattenMessages: seq of Message -> Message



~~~{% endraw %}
