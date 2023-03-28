---
title: "Class Invariants"
document: TBD
date: 2023-03-28
audience: SG21
author:
  - name: Nick DeMarco
    email: <demarco@adobe.com>
  - name: Rani Kumar
    email: <ranik@adobe.com>
  - name: Sean Parent
    email: <sparent@adobe.com>
toc: true
toc-depth: 4
---

\pagebreak

# Revision History

  - R0 --- TODO

# Executive Summary

We propose a model for expressing class invariants in C++, to be added to the so-called _Contracts MVP_. We believe this facility, or one with comparable semantics, is necessary to support minimum viable contracts support in C++. In short, we propose a class-scope keyword `invariant`, which opens a scope that has `const` access to `*this`. Each invariant block is to be evaluated (in unspecified order) at the exit of every public constructor and non-const member function, as if it were a postcondition.

```cpp
class type {
  int _x{0};
  int _y{0};

invariant { 0 <= _x }
invariant { _x <= _y }
};
```

By expressing these as invariants, rather than as postconditions of member functions, we avoid the issue of infinite recursion described in [@p2388r4] (§9.5). This issue appears to demonstrate the infeasibility of implementing class invariants in terms of postconditions, and justifies the need for direct invariant support in an adequate _Contracts MVP_.

# Introduction

[@P2817R0]

# Motivation and Scope

# Before/After Comparisons

## Comparison 1

::: tonytable

### Before
```cpp
void before() {}
```

### After
```cpp
void after() {}
```

:::

# Design Overview

# Acknowledgements

TODO

\pagebreak

---
references:
  - id: P2182R1
    citation-label: P2817
    title: "Contract Support: Defining the Minimum Viable Feature Set"
    author:
      - family: Krzemieński
        given: Andrzej
      - family: Berne
        given: Joshua
      - family: McDougall
        given: Ryan
    issued:
      year: 2020
    URL: https://www.open-std.org/jtc1/sc22/wg21/docs/papers/2020/p2182r1.html
  - id: P2388R4
    citation-label: P2388
    title: "Minimum Contract Support: either _No\_eval_ or _Eval\_and\_abort_"
    author:
      - family: Krzemieński
        given: Andrzej
      - family: Ažman
        given: Gašper
    issued:
      year: 2021
    URL: https://www.open-std.org/jtc1/sc22/wg21/docs/papers/2021/p2388r4.html
  - id: P2461R1
    citation-label: P2461
    title: "Closure-Based Syntax for Contracts"
    author:
      - family: Ažman
        given: Gašper
      - family: Sunstrum
        given: Caleb
      - family: Kozicki
        given: Bronek
    issued:
      year: 2021
    URL: https://www.open-std.org/jtc1/sc22/wg21/docs/papers/2021/p2461r1.pdf
  - id: P2817R0
    citation-label: P2817
    title: "The idea behind the contracts MVP"
    author:
      family: Krzemieński
      given: Andrzej
    issued:
      year: 2023
    URL: https://isocpp.org/files/papers/P2817R0.html
---
