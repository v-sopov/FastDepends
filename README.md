# FastDepends

<p align="center">
    <a href="https://github.com/Lancetnik/FastDepends/actions/workflows/tests.yml" target="_blank">
        <img src="https://github.com/Lancetnik/FastDepends/actions/workflows/tests.yml/badge.svg" alt="Tests coverage"/>
    </a>
    <a href="https://coverage-badge.samuelcolvin.workers.dev/redirect/lancetnik/fastdepends" target="_blank">
        <img src="https://coverage-badge.samuelcolvin.workers.dev/lancetnik/fastdepends.svg" alt="Coverage">
    </a>
    <a href="https://pypi.org/project/fast-depends" target="_blank">
        <img src="https://img.shields.io/pypi/v/fast-depends?label=pypi%20package" alt="Package version">
    </a>
    <a href="https://pepy.tech/project/fast-depends" target="_blank">
        <img src="https://static.pepy.tech/personalized-badge/fast-depend?period=total&units=international_system&left_color=grey&right_color=blue&left_text=Downloads" alt="downloads"/>
    </a>
    <br/>
    <a href="https://pypi.org/project/fast-depend" target="_blank">
        <img src="https://img.shields.io/pypi/pyversions/fast-depends.svg" alt="Supported Python versions">
    </a>
    <a href="https://github.com/Lancetnik/FastDepends/blob/main/LICENSE" target="_blank">
        <img alt="GitHub" src="https://img.shields.io/github/license/Lancetnik/FastDepends?color=%23007ec6">
    </a>
</p>

---

Documentation: https://lancetnik.github.io/FastDepends/

---

FastDepends - Fastapi dependency injection system extracted from Fastapi and cleared of all HTTP logic.
This is a small library which provides you with the ability to use lovely Fastapi interfaces in your own
projects or tools.

Thanks to [*fastapi*](https://fastapi.tiangolo.com/) and [*pydantic*](https://docs.pydantic.dev/) projects for this
greate functionality. This package is just a small change of the original Fastapi sources to provide DI functionality in a pyre-Python way.

Async and sync modes are both supported.

## Installation

```bash
pip install fast-depends
```

## Usage

There is no way to make Dependency Injection easier

You can use this library without any frameworks in both **sync** and **async** code.

### Async code
```python
import asyncio

from fast_depends import inject, Depends

async def dependency(a: int) -> int:
    return a

@inject
async def main(
    a: int,
    b: int,
    c: int = Depends(dependency)
) -> float:
    return a + b + c

assert asyncio.run(main("1", 2)) == 4.0
```

### Sync code
```python
from fast_depends import inject, Depends

def dependency(a: int) -> int:
    return a

@inject
def main(
    a: int,
    b: int,
    c: int = Depends(dependency)
) -> float:
    return a + b + c

assert main("1", 2) == 4.0
```

`@inject` decorator plays multiple roles at the same time:

* resolve *Depends* classes
* cast types according to Python annotation
* validate incoming parameters using *pydantic*

---

### Features
Synchronous code is fully supported in this package: without any `async_to_sync`, `run_sync`, `syncify` or any other tricks.

Also, *FastDepends* casts functions' return values the same way, it can be very helpful in building your own tools.

These are two main defferences from native Fastapi DI System.

---

### Note
Library was based on **0.95.0 FastAPI** version.

If we are too far behind, please, contact [me](mailto:diementros@yandex.ru)
or contubute yourself. Really appreciate your help.
