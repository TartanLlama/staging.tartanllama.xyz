---
author: Sy Brand
pubDatetime: 2016-10-18
title: "Declaring Classes in Function Declarations"
draft: false
tags:
  - C++
canonicalURL: https://tartanllama.xyz/posts/declare-class-in-func
description: You can do this, but don't
---

C++ allows you to declare classes in function declarations. The following code is fully standards-compliant:

```cpp
void foo (class A*){}

A* g_a;

int main() {
    A* a;
    foo(a);
}
```

I thought this was pretty odd and interesting, so went searching for the applicable rules from the standard. Here is the breakdown on how this works.

-------------

`class A` or `struct A` is called an *elaborated-type-specifier*.

> [[basic.lookup.elab]/2](https://timsong-cpp.github.io/cppwp/n4140/basic.lookup.elab#2):
> 
>[...] If the *elaborated-type-specifier* is introduced by the *class-key* and this lookup does not find a previously declared *type-name*, or if the *elaborated-type-specifier* appears in a declaration with the form:
>
> *class-key attribute-specifier-seqopt identifier ;*
>
>the *elaborated-type-specifier* is a declaration that introduces the *class-name* as described in 3.3.2.

> [[basic.scope.pdecl]/7](https://timsong-cpp.github.io/cppwp/n4140/basic.scope.pdecl#7)
>
> The point of declaration of a class first declared in an elaborated-type-specifier is as follows:
>
> - [...]
> - for an elaborated-type-specifier of the form
>
> *class-key identifier*
>
> if the elaborated-type-specifier is used in the decl-specifier-seq or parameter-declaration-clause of a function defined in namespace scope, the identifier is declared as a class-name in the namespace that contains the declaration; otherwise, except as a friend declaration, the identifier is declared in the smallest namespace or block scope that contains the declaration.

-------------

**Don't do this.**