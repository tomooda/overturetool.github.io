---
layout: default
title: diet2japan
---

~~~
This example is made by Shin Sahara as a test of local higher order
~~~
###Diet.vdmpp

{% raw %}
~~~

class Diet
values
functions
static public getWeightFromBMI : real * real -> real
static public newton: (real ->real) -> real -> real
static public derivative : (real -> real) ->real -> real
static public Funtil[@T] : (@T -> bool) -> (@T -> @T) -> @T -> @T
end Diet

~~~{% endraw %}
