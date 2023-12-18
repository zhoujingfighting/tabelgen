---
layout: two-cols
---

<h1> TableGen basic - Lexical Analysis </h1>

## Numeric literals
* TokInteger     ::=  DecimalInteger | HexInteger | BinInteger
* DecimalInteger ::=  ["+" | "-"] ("0"..."9")+
* HexInteger     ::=  "0x" ("0"..."9" | "a"..."f" | "A"..."F")+
* BinInteger     ::=  "0b" ("0" | "1")+

```cpp {monaco}
class Demo {
    int A = 10;
    int B = -25;
    int C = 0x16;
    int D = 0b1111;
}
def D : Demo;
```

```py
def D { // Demo
  int A = 10;
  int B = -25;
  int C = 22;
  int D = 15;
}
```




<style>
.code-container {
  display: flex;
  justify-content: space-between;
}
  pre {
    background-color: #fff; /* change background color */
    color: #abb2bf; /* change text color */
    padding: 20px; /* add some padding */
    border-radius: 10px; /* round the corners */
    overflow-x: auto; /* add a horizontal scrollbar if needed */
  }
  code {
    font-family: 'Fira Code', monospace; /* change font */
    font-size: 14px; /* change font size */
  }
</style>

---

<h1> TableGen basic - Lexical Analysis </h1>

## String literals

```
TokString ::=  '"' (non-'"' characters and escapes) '"'

TokCode   ::=  "[{" (shortest text not containing "}]") "}]"
```

```cpp {monaco}
class Demo1 {
    string A = "Hello world";
    // string B = "hello "bug"";
    code B = "[{ return "dwwwd"; }]";
}

def D : Demo1;
```

```cpp
def D { // Demo1
  string A = "Hello world";
  code B = [{ return "dwwwd"; }];
}
```

---

<h1>TableGen basic - Lexical Analysis</h1>

## Identifiers


* ualpha        ::=  "a"..."z" | "A"..."Z" | "_"
* TokIdentifier ::=  <span class="highlight">("0"..."9")* </span> ualpha (ualpha | "0"..."9")*
* TokVarName    ::=  "$" ualpha (ualpha |  "0"..."9")*


### Reserved keywords

```txt
assert     bit           bits          class         code
dag        def           dump          else          false
foreach    defm          defset        defvar        field
if         in            include       int           let
list       multiclass    string        then          true
```

---

<h1>TableGen basic - Lexical Analysis</h1>

## [Bang operators](https://linuxize.com/post/bash-shebang/)

```txt
BangOperator ::=  one of
                  !add         !and         !cast        !con         !dag
                  !div         !empty       !eq          !exists      !filter
                  !find        !foldl       !foreach     !ge          !getdagarg
                  !getdagname  !getdagop    !gt          !head        !if
                  !interleave  !isa         !le          !listconcat  !listremove
                  !listsplat   !logtwo      !lt          !mul         !ne
                  !not         !or          !range       !repr        !setdagarg
                  !setdagname  !setdagop    !shl         !size        !sra
                  !srl         !strconcat   !sub         !subst       !substr
                  !tail        !tolower     !toupper     !xor
```

```cpp {monaco}
class Demo {
    int A = !add(1,10); >>> int A = 11;
    bit B = !eq(1,2); >>> bit B = 0;
}
def D : Demo;
```

---

<h1>TableGen basic - Lexical Analysis</h1>

## Include files

```txt
IncludeDirective ::=  "include" TokString

PreprocessorDirective ::=  "#define" | "#ifdef" | "#ifndef"
```

```cpp {monaco}
#ifdef _INCLUDE
include "bang.td"
#endif
```
---

<h1>TableGen basic - Types</h1>

```txt
Type    ::=  "bit" | "int" | "string" | "dag"
            | "bits" "<" TokInteger ">"
            | "list" "<" Type ">"
            | ClassID
ClassID ::=  TokIdentifier
```

```cpp {monaco}
def test; // record

class Terapines {
    string name = "Terapines";
}

def T : Terapines;

class TypeDemo {
    bit A = 0;
    int B = 123;
    string C = "Terapines";
    dag D = (test 1, 2); // dag 
    Terapines E = T; // ClassID
    string F = T.name;
}
```

---

<h1>TableGen basic - Values and Expressions</h1>

```txt
Value         ::=  SimpleValue ValueSuffix*
                  | Value "#" [Value]
ValueSuffix   ::=  "{" RangeList "}"
                  | "[" SliceElements "]"
                  | "." TokIdentifier
RangeList     ::=  RangePiece ("," RangePiece)*
RangePiece    ::=  TokInteger
                  | TokInteger "..." TokInteger
                  | TokInteger "-" TokInteger
                  | TokInteger TokInteger
SliceElements ::=  (SliceElement ",")* SliceElement ","?
SliceElement  ::=  Value
                  | Value "..." Value
                  | Value "-" Value
                  | Value TokInteger

```
