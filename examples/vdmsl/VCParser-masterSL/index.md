---
layout: default
title: VCParser-master
---

~~~

This example is created by Tomohiro Oda and it illustrates

#******************************************************
~~~
###VCParser.vdmsl

{% raw %}
~~~
module VCParser
Copyright (c) 2013 Tomohiro Oda and Software Research Associates, Inc.
Permission is hereby granted, free of charge, to any person obtaining a copy
The above copyright notice and this permission notice shall be included in
THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
exports all
values
    /***
        digit = label("digit", either([takeChar("0123456789"(index)) | index in set {1,...,10}]));
        natnum = label("nat",
functions    
    takeString : seq1 of char -> PARSER
    /***
    either : seq1 of PARSER -> PARSER
    star : PARSER -> PARSER
    option : PARSER -> PARSER

    trimBlanks : PARSER -> PARSER
    fail : PARSER -> PARSER
    concat : PARSER -> PARSER
    pass : PARSER -> PARSER
    label : LABEL * PARSER -> PARSER
    trans : (PARSED->PARSED) * PARSER->PARSER
    transtree : (TREE -> TREE) * PARSER -> PARSER
    iferror : seq of char * PARSER -> PARSER
~~~{% endraw %}
