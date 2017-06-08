---
layout: post
title: 'Resharper Plugin: ZenSharp'
tags: ['ReSharper', 'ZenSharp']
category: 'resharper'
date: '2017-03-27 11:44'
author: 'GaryNg'
---

# Resharper Plugin: ZenSharp
> ZenSharp for ReSharper is mnemonics on steroids!

_from [ZenSharp](https://github.com/ulex/ZenSharp) repo_

The [official documentation](https://github.com/ulex/ZenSharp/blob/master/README.md) already has a lot of useful macros/templates/usages, but I found a lot of undocumented templates by going through [Templates.ltg](https://github.com/ulex/ZenSharp/blob/master/ZenSharp.Integration/Templates.ltg) (located under `MyDocuments` folder).

## `Templates.ltg`

Here is the version of `Templates.ltg` that I used:
```
space ::= " "
cursor ::= "$END$"
cursorb ::= "(" cursor ")"
// Resharper macros:
identifier ::= <name default="$name$" macros = "suggestVariableName()">
identifier2 ::= <name2 default="$name2$" macros = "suggestVariableName()">
//
// Types:
//
suggType ::= <type short="t" expand="$type$" macros = "complete()">

// Primive types:
maybeType  ::= type | "void"
type       ::= generic | primType ("?"="?")? ("[]"=a)? | suggType
primType   ::= string=s | byte=by | bool=b | "System.DateTime"=dt | decimal=dc | double=d | int=i | uint=ui | "System.Guid"=g | "System.Uri"=u | "System.Xml.Linq.XElement"=x |
               object=o
taskType   ::= "System.Threading.Tasks.Task"

// Complex types:
generic1 ::= (SCG "." ("IList"=l | "IEnumerable"="~")) "<" type ">"
generic2 ::= (SCG "." ("SortedList"=sl | "IDictionary"=di)) "<" type ", " type ">"
SCG      ::= "System.Collections.Generic"
generic ::= generic1 | generic2


access ::= (internal=i | public=p | private=_ | protected=P) space

// Auto properties:
property        ::= access ("abstract "=ap | "static "=P | "virtual "=vp | ""=p) type space identifier propertyBody cursor
propertyBody    ::= "{ get;" propertySetAccessor " set; }"
propertySetAccessor ::= "protected "="+P" | ""="+" | "private "

// Methods:
methodAttributes ::=
    | "[NUnit.Framework.SetUpAttribute]"=su
    | "[NUnit.Framework.TestFixtureSetUpAttribute]"=tfsu
    | "[NUnit.Framework.TestFixtureTearDownAttribute]"=tftd
    | "[NUnit.Framework.TearDownAttribute]"=td
    | "[NUnit.Framework.TestCaseAttribute]"=tc
    | "[NUnit.Framework.TestAttribute]"=t
method_async ::= (methodAttributes)? access "async" space ("virtual "=vm | "abstract "=am | "static "=M | ""=m)   (taskType "<"=T type ">" | taskType ""=T) space identifier methodArgs methodBody
method_generic ::= (methodAttributes)? access ("virtual "=vm | "abstract "=am | "static "=M | ""=m) (type | "void") space identifier methodArgs methodBody
method ::= method_async | method_generic
methodBody ::= " { " cursor " }"
methodArgs ::=  "(" ((""="," | ""="(") arg)? ")"
arg ::= primType " " identifier2

// Consts:
// const ::= access "const "=c primType space identifier "= """ identifier """;"
const ::= access "const "=c primType space identifier "="="=" cursor ";"

// Fields:
field ::= access ("readonly "=r)? type space identifier ("="="=" identifier2 ";" | ";")

// Classes:
classAtributes ::= ("[NUnit.Framework.TestFixtureAttribute]" = tf)?
class ::= classAtributes access ("sealed "=E)? ("class"=c | "static class"=C) space  classBody
classBody ::= identifier (" : "=":" type)? "{" cursor "}"

//Enums:
enum ::= access space "enum"=e space identifier "{" cursor "}"

scope "InCSharpClass" {
  start    ::=  method | property | field | const | other

  other ::=
    | class
	| ""=dbset "public DBSet<" identifier " > " identifier "s {get; set; }"
  | enum
}

scope "InCSharpTypeAndNamespace" {
  start ::=
    | class
    | interface
    | enum

  interface ::= access "interface"=i space classBody
}

scope "InCSharpInterface" {
  start ::=
    | type space identifier propertyBody cursor
    | method
    | property

  propertyBody ::= "{ get; }" | "{ get; set; }"="+"
  access ::= ""
  methodBody ::= ";"
}

scope "InCSharpStruct" {
 // start ::= ""
}

scope "InCSharpStatement" {
  start ::=
    | "if ("=ifr identifier " == null) return;"
	| "Log."=l (Fatal=f | Info=i | Error=e | Trace=t | Debug=d) "(""" cursor """);"
}
```

I changed

```
identifier ::= <name default="$name$" macros = "complete()">
identifier2 ::= <name2 default="$name2$" macros = "complete()">
```

to

```
identifier ::= <name default="$name$" macros = "suggestVariableName()">
identifier2 ::= <name2 default="$name2$" macros = "suggestVariableName()">
```

and

```
scope "InCSharpClass" {
  start    ::=  method | property | field | const | other

  other ::=
    | class
	| ""=dbset "public DBSet<" identifier " > " identifier "s {get; set; }"
}
```

to

```
scope "InCSharpClass" {
  start    ::=  method | property | field | const | other

  other ::=
    | class
	| ""=dbset "public DBSet<" identifier " > " identifier "s {get; set; }"
  | enum
}
```

## Documentation
These are the notes I wrote while playing with ZenSharp.

### 1. Access Modifiers
> &lt;Access Modifiers&gt;

Shortcut	|	Expand To
----------|-----------
`p`				|	`public`
`_`				|	`private`
`i`				|	`internal`
`P`				|	`protected`

### 2. Types
Shortcut	|	Note
----------|---------------------------------------------------------------------
`t`				|	`$type$` (ask for user input/aka "hotspot")
`a`				|	any primitive type ends with `a` will expand to the array of the type
`?`				|	any primitive type ends with `?` will expand to nullable of the type

### 3. Primitive Types
> #### Format
> `<t|<Type>>[?][a][<Identifier>]`
>
> #### Note
>
Symbol							|	Meaning
--------------------|---------
`[]`								|	Optional
<code>&#124;</code>	|	Or
`<>`								|	Required

Shortcut	|	Expand To
----------|-----------
`s`				|	`string`
`by`			|	`byte`
`b`				|	`bool`
`dt`			|	`DateTime`
`d`				|	`double`
`i`				|	`int`
`ui`			|	`uint`
`g`				|	`Guid`
`dc`			|	`decimal`
`u`				|	`Uri`
`x`				|	`XElement`
`o`				|	`object`

#### Examples
Shortcut	|	Expand To
----------|-----------
`b?`			|	`bool?`
`ba`			|	`bool[]`
`b?a`			|	`bool?[]`


### 4. Complex Types
Shortcut	|	Expand To
----------|-----------
`l`				|	`IList`
`~`				|	`IEnumerable`

> #### Format (for `sl` and `di`)
> `<Access Modifiers><sl|di><<Type>|t><<Type>|t>[<Identifier>]`

Shortcut	|	Expand To
----------|-----------
`sl`			|	`SortedList`
`di`			|	`IDictionary`

#### Examples
Shortcut	|	Expand To
----------|-----------
`li`			| `IList<int>`
`~s`			| `IEnumerable<string>`

### 5. Properties
> #### Format
> `<Access Modifiers><ap|P|vp|p><t|<Type>>[<Identifier>][+[P]]`

Shortcut	|	Expand To
----------|-----------
`ap`			|	`abstract`
`P`				|	`static`
`vp`			|	`virtual`
`p`				|	"" (normal property)

### Property Set Accessor
Shortcut		|	Expand To
------------|-----------
_default_		| `private set;`
`+`					| `public set;`
`+P`				| `protected set;`

#### Examples
> #### Note
> `$name$`: Hotspot (ask for user input)

Shortcut					|	Expand To
------------------|---------------------------------------------
`ppt`							| `public $type$ $name$ { get; private set; }`
`pps`							| `public string $name$ { get; private set; }`
`ppsTesting`			| `public string Testing { get; private set; }`
`ppsTesting+`			| `public string Testing { get; set; }`
`ppsTesting+P`		| `public string Testing { get; protected set; }`
`pvpiTest+`				| `public virtual int Test { get; set; }`
`pPi?aTest+P`			| `public static int?[] Test { get; protected set; }`
`pvp~i?aTesting+P`| `public virtual IEnumerable<int?[]> Testing { get; protected set; }`

### 6. Method Attributes
> #### Note
> Specific to NUnit only

Shortcut		|	Expand To
------------|-----------
`su`				| `[SetUp]`
`tfsu`			| `[TestFixtureSetUp]`
`tftd`			| `[TestFixtureTearDown]`
`td`				| `[TearDown]`
`tc`				| `[TestCase]`
`t`					| `[Test]`

### 7. Methods
> #### Format
> `[<Method Attributes>]<Access Modifier><am|vm|M|m>[t|<Type>|T[<Type>|t]][<Identifier>][,<Type>[<Identifier>]]`

Shortcut		|	Expand To
------------|-----------
`am`				| `abstract`
`vm`				| `virtual`
`M`					| `static`
`m`					| `void`

#### Examples
Shortcut						|	Expand To
--------------------|-----------
`_m`								| `private void $name$(){}`
`_vmt`							| `private virtual $type$ $name$(){}`
`_ms`								| `private string $name$(){}`
`_msTesting`				| `private string Testing(){}`
`_msTesting,s`			| `private string Testing(string $name2$){}`
`_msTesting,sparam`	| `private string Testing(string param){}`

#### async Method Examples
Shortcut							|	Expand To
----------------------|-----------
`_mT`									| `private async Task $name$(){}`
`_mTt`								| `private async Task<$type$> $name$(){}`
`_mTs`								| `private async Task<string> $name$(){}`
`_mTsTesting`					| `private async Task<string> Testing(){}`
`_mTsTesting,s`				| `private async Task<string> Testing(string $name2$){}`
`_mTsTesting,sparam`	| `private async Task<string> Testing(string param){}`

#### More Examples
Shortcut							|	Expand To
----------------------|-----------
`tpmTsTesting,icase`	| `[NUnit.Framework.TestAttribute]` <br> `public async Task<string> Testing(int case){}`

### 8. Consts
> #### Format
> `<Access Modifier>c<Type>[<Identifier>]=`

#### Examples
Shortcut				|	Expand To
----------------|-----------
`_cs=`					| `private const string $S$ = $$;`
`_csTesting=`		| `private const string Testing = $$;`

> #### Note
> Need to include the ending `=`, otherwise it will be expanded as `class`

### 9. Fields
> #### Format
> `<Access Modifier>[r]<<Type>|t>[<Identifier>][=]`

Shortcut				|	Expand To
----------------|-----------
`r`							| `readonly`

#### Examples
Shortcut				|	Expand To
----------------|-----------
`_s`						| `private string $_s$;`
`_s_testing`		| `private string _testing;`
`_s=`						| `private string $_s$ = $name2$;`
`_s_testing=`		| `private string _testing = $name2$;`
`_rs`						| `private readonly string $_s$;`
`_rs_testing`		| `private readonly string _testing;`
`_rs=`					| `private readonly string $_s$ = $name2$;`
`_rs_testing=`	| `private readonly string _testing = $name2$;`

### 10. Enums
> #### Format
> `<Access Modifier>e[<Identifier>]`

#### Examples
Shortcut				|	Expand To
----------------|-----------
`pe`						| `public enum $name${}`
`peTesting`			| `public enum Testing{}`

### 11. Class Attributes
> #### Note
> Specific to NUnit only

Shortcut				|	Expand To
----------------|-----------
`tf`						| `[TestFixture]`

### 12. Classes
> #### Format
> `[<Class Attributes>]<Access Modifier>[s]<c|C><Identifier>[:<<Type>|t>]`


Shortcut				|	Expand To
----------------|-----------
`s`							| `sealed` <br> > Note: Unexpandable? (Will be expanded to `string`)

#### Examples
Shortcut				|	Expand To
----------------|-----------
`pcTesting`			| `public class Testing{}`
`pcTesting:t`		| `public class Testing : $type${}`
`pcTesting:o`		| `public class Testing : object{}`

### 13. Interfaces
> #### Format
> `<Access Modifier>i[<Identifier>][:<<Type>|t>]`
> #### Scope
> Type and Namespace

Shortcut				|	Expand To
----------------|-----------
`pi`						| `public interface $name${}`
`piTesting`			| `public interface Testing{}`
`piTesting:t`		| `public interface Testing : $type${}`
`piTesting:lt`	| `public interface Testing : IList<$type$>{}`

### 14. Logging
> #### Format
> `l<f|i|e|t|d>`
> #### Scope
> Statements

Shortcut				|	Expand To
----------------|-----------
`f`							| `Fatal`
`i`							| `Info`
`e`							| `Error`
`t`							| `Trace`
`d`							| `Debug`

#### Examples
Shortcut				|	Expand To
----------------|-----------
`lf`						| `Log.Fatal("$$");`
> #### Note
> `lf"` is better (It will become the first entry in Intellisense)

### 15. Others
Shortcut				|	Expand To																			| Scope
----------------|-----------------------------------------------|---------
`dbset`					| `public DBSet<$name$> $names$ { get; set; }`	|	Class
`ifr`						| `if ($name$ == null) return;`									|	Statements

## Documention Gist
[ZenSharp Documentation](https://gist.github.com/garyng/3a597234d8a24544da5485e8cb1e4f61)


## Reference
[ZenSharp](https://github.com/ulex/ZenSharp)

[ReSharper 2016.3 Help: List of Template Macros](https://www.jetbrains.com/help/resharper/2016.3/Template_Macros.html)
