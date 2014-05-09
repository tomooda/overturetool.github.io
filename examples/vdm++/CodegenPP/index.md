---
layout: default
title: Codegen
---

~~~
This example is produced by a group of students as a part
~~~
###Codegen.vdmpp

{% raw %}
~~~
class Codegen
	values
	instance variables
	operations
	public Generate : GiraffeSpecification ==> seq of char
	public Generate : GiraffeClassDefinition ==> seq of char
	public Generate : GiraffeMethodDefinition ==> seq of char
	public Generate : GiraffeParameter ==> seq of char
	public Generate : GiraffeType ==> seq of char
	public Generate : GiraffeStatement ==> seq of char
	public GenerateExpression : GiraffeExpression ==> seq of char
	public GenerateBinaryExpression : GiraffeBinaryExpression ==> seq of char
	functions
	public tail : seq of seq of char -> seq of seq of char
end Codegen
~~~{% endraw %}

###Compiler.vdmpp

{% raw %}
~~~
class Compiler
	values
	instance variables
	typeDefs : seq of SimpleTypeDefinition := [];
	context : map seq of char to seq of char := {|->};
	varDecls : seq of GiraffeVariableDeclStatement := [];
	uid : nat1 := 1;
	operations
private getUniqeName : () ==> seq of char
private getUniqeSimpleName : () ==> seq of char
	return ""
public Compile : seq of char * SimpleSpecification ==> GiraffeSpecification
public Compile : SimpleFunctionDefinition ==> GiraffeMethodDefinition
public Compile : SimpleParameter ==> GiraffeParameter
public Compile : SimpleType ==> [GiraffeType]
public Compile : SimpleExpression ==> [GiraffeExpression]
public CompileCases : SimpleCasesExpression ==> GiraffeExpression
public CompileLet : SimpleLetExpression ==> GiraffeExpression
public Compile : SimpleBinaryOperator * SimpleExpression * SimpleExpression ==> [GiraffeBinaryExpression]
		"PLUS" -> let	glhs : GiraffeExpression = Compile(lhs),
public GetType : SimpleExpression ==> SimpleType
public GetBasicType : SimpleType ==> SimpleBasicType
functions
public CompileIf : SimpleIfExpression -> GiraffeIfExpression
public deflatten : seq of SimpleElseIfExpression * SimpleExpression -> GiraffeExpression
end Compiler
~~~{% endraw %}

###nativetest.vdmpp

{% raw %}
~~~
class codegen_Util
instance variables
compiler : Compiler := new Compiler();
operations
public Run : () ==> (bool|int|seq of char)
public Run : seq of seq of char ==> seq of char
functions
	public showType : int -> int
	public getSimpleNames : () -> seq of seq of char
	public parseSimpleProgram : seq of char -> SimpleSpecification
	public writeProgram : seq of char * seq of char -> bool
	public compileProgram : seq of char -> bool
	public runProgram : seq of char -> (int|bool)
end codegen_Util

~~~{% endraw %}

###VDMUtil.vdmpp

{% raw %}
~~~
class VDMUtil
-- 	Overture STANDARD LIBRARY: MiscUtils
functions
-- Returns a context information tuple which represents
-- Converts a VDM value into a seq of char.
-- converts VDM value in ASCII format into a VDM value
end VDMUtil
class A
end A
~~~{% endraw %}
