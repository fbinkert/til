---
title: Python `match` Performance
description: Performance trade-offs in Python's structural pattern matching. 
pubDate: 2025-09-17
author: Fabian Binkert
tags:
  - Python
---

Python's `match ... case` is terribly slow is not comparable to a C-style `switch`. The Python interpreter doesn't construct a O(1) jump table (at least not CPython).
Performance wise, simple literal/type checks, are on par with analogous `if/elif` implementations. The more complex the pattern matching component, the more overhead you get.

For example, nested patterns and captures like `[ *rest ]` or `{ **rest }` do extra work and allocate new containers. If you need it, order cheap, selective cases first and prefer fixed-size patterns.

For performance-critical key->action dispatch, keep using a dict lookup. It beats both `match ... case` and `if/elif` any day in terms of performance. 

Approximate performance characteristics (your mileage may vary):
- Literal/type checks: ~same speed as if/elif
- Complex patterns (nested, *rest, **rest): 2-8x slower (allocates new containers)
- Dict dispatch: ~6x faster than match for key→action
