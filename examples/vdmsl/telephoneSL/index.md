---
layout: default
title: telephone
---

~~~
This example due to Abrial has been translated from the 
#******************************************************
~~~
###telephone.vdmsl

{% raw %}
~~~

module EXCH
   Initiator =  <AI> | <WI> | <SI>;
   Recipient = <WR> | <SR>;
   Status = <fr> | <un> | Initiator | Recipient;
 state Exchange of


operations
  Lift(s: Subscriber)
  Connect(i: Subscriber, r: Subscriber)
  MakeUn(i: Subscriber)
  Answer(r: Subscriber)    
  ClearAttempt(i: Subscriber)
  ClearWait(i: Subscriber)
  ClearSpeak(i: Subscriber)
  Suspend(r: Subscriber)
  ClearUn(s: Subscriber)
end EXCH  

~~~{% endraw %}
