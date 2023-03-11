---
layout: page
title: Projects
permalink: /projects/
---

Releasy
=======

Releasy is an open source tool that collects provenance data from releases by parsing the software version control and issue tracking systems.

The tool is available under MIT License at <https://github.com/gems-uff/releasy>, and you can learn more about it through the following paper:

  - [Curty, F., Kohwalter, T., Braganholo, V., Murta, L., 2018. An Infrastructure for Software Release Analysis through Provenance Graphs. Presented at the VI Workshop on Software Visualization, Evolution and Maintenance.](https://goo.gl/9u8rzc)


pytest-pyspec
=============

[pytest-pyspec](https://github.com/felipecrp/pytest-pyspec) is an open-source plugin to pytest. The plugin transforms the pytest output into a result similar to the RSpec. It can nest unlimited test cases and include the test docstring in the test output. It can generate outputs like the following:


```
test/test_sample.py 

A house
  ✓ Has door

A house
  With two floors
    ✓ Has stairs
    ✓ Has second floor
    ✗ Has third floor
```