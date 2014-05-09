---
layout: default
title: library
---

~~~
This specification is for a bibliography database. It has been written

#******************************************************
~~~
###library.vdmsl

{% raw %}
~~~
types
Id = nat;
Article::id	:Id
Book::	id	:Id
Inproceeding::	id	:Id
Manual::id	:Id
Techreport::	id	:Id
Record =  Article | Book | Inproceeding | Manual | Techreport;
Recordtype = <article> | <book> | <inproceeding> | <manual> | <techreport>;
Value = Id | String | Edition | Month | Number | Pages | 
Valuetype = <id> | <address> | <author> | <booktitle> | <edition> | 


state mgd of

functions

field: Recordtype +> set of Valuetype


get: set of Record*Id +> Record
CardDb: set of Record*Id +> nat
getvalue: Valuetype*set of Record*Id +> Value
iscomplete :set of Record*Id +> bool
isedition: Value +> bool
isempty: Value +> bool
isidentical: set of Record +> bool
isidentical2: set of Record*set of Record*set of Record*Record +>bool
isidentical3: set of Record*set of Record*set of Record*Record*
ismonth: Value +> bool
isnumber: Value +> bool
ispages: Value +> bool
isstring: Value +> bool
issubstring: String*String +> bool
issubstring2: String*String*String +> bool


isvalueoffield: Value*Valuetype +> bool
isvolume: Value +> bool
isyear: Value +> bool
optional: Recordtype +> set of Valuetype
recordtype: set of Record*Id +> Recordtype
required: Recordtype +> set of Valuetype
substring(s:String,i:nat1,j:nat1) r:String
usedIds: set of Record +> set of Id
idset: set of Record*set of Id +> set of Id
CardRecords: set of Record*set of Id +> nat
operations
CREATE: Recordtype ==> Id
post 	RESULT not in set usedIds(dB~) and 
UPDATE(i:Id,f:Valuetype,v:Value)==
COMPLETE: Id ==> bool

DELETE(i:Id)==
SEARCH: String ==> set of Id
GET: Id ==> Record


~~~{% endraw %}
