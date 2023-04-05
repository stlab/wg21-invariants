---
title: "Class Invariants"
document: TBD
date: 2023-03-28
audience: SG21
author:
  - name: Nick DeMarco
    email: <demarco@adobe.com>
  - name: Sean Parent
    email: <sparent@adobe.com>
  - name: David Sankel
    email: <dsankel@adobe.com>
toc: true
toc-depth: 4
---

\pagebreak

# Revision History

  - R0 --- TODO

# Executive Summary

We propose semantics for class invariants in C++, independent of a particular syntax. Additionally, we identify a set of standard library functions which are necessary to test class invariants in situations where implicit checks are impossible for a compiler to generate. Finally, we provide illustrative examples with a syntax inspired by [@P2461].

# Semantic Principles

TODO: Preamble

1. Invariants are checked as if they were postconditions of public constructors and non-`const` member functions.
2. Invariants only have access to a `const *this`.
3. Invariants have private access.

## Motivation

1. Conceptually, a class invariant is a property which holds whenever the state of a class instance is _observed_ by code outside of that class's definition. (TODO: How do we handle public member access? That's observable too, and we don't have a model for enforcing invariants after, say, `mystruct.field = -1`)

2. Invariants are simply expressions of constraints, and therefore have no need to modify the class instances they constrain. Outright modificiations of objects during an invariant test are unidiomatic at best. 

3. Clearly, invariants must be able to express constraints on the private state of class instances. We cannot imagine a useful implementation of invariants that lacks this property.

# Example

```cpp
class type {
  int _x{0};
  int _y{0};

invariant { 0 <= _x }
invariant { _x <= _y }
};
```

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
