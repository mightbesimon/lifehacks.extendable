# lifehacks.metaclasses ![version](https://img.shields.io/pypi/v/lifehacks.metaclasses?label=)

[![sponsor](https://img.shields.io/badge/-Sponsor_Us-%23d73a49)](https://github.com/sponsors/mightbesimon)
![downloads](https://img.shields.io/pypi/dm/lifehacks.metaclasses?color=white&label=&logo=python)
![publish](https://github.com/mightbesimon/lifehacks.metaclasses/actions/workflows/publish.yml/badge.svg)

## Structure

```plaintext
📦 lifehacks.metaclasses
├── meta
├── enum
└── EnumException
```

## Installation

```bash
pip install lifehacks.metaclasses
```

## Usage

- [`meta` metaclass](#meta-metaclass)
- [`enum` metaclass](#enum-metaclass)
- [`EnumException`](#enumexception)

### `meta` metaclass

There are a few ways to make an `meta` class.

```python
from lifehacks.metaclasses import meta

class myenum0(metaclass=meta): ...

@meta  		# preferred method
class myenum1: ...

@meta()		# do not use this method
class myenum2: ...
```

### `enum` metaclass

Same with `meta` metaclass from above,
there are a few ways to make an `enum` class.

```python
from lifehacks.metaclasses import enum

# with typing
class MyPalette0(metaclass=enum[Colour]): ...

@enum  		# preferred method
class MyPalette1: ...

@enum[Colour]	# syntax only allowed python>=3.9
class MyPalette2: ...

@enum()		# do not use this method
class MyPalette3: ...
```

usage example:

```python
from lifehacks.metaclasses import enum

@enum[Colour]
class BasePalette:
	BLACK = ...
	WHITE = ...

# extending base palette enum
class SubPalette(BasePalette):
	RED = ...
	GREEN = ...

# can be used in type hinting
def print_colours(palette:enum[Colour]) -> None:
	for name, value in palette:
		print(name, value)

print_colours(BasePalette) # BLACK, WHITE
print_colours(SubPalette)  # BLACK, WHITE, RED, GREEN
print(BasePalette.BLACK in SubPalette) # True
```

`enum` classes are not instantiable, more on that [below](#enumexception).

### `EnumException`

`enum` classes are not instantiable.
If you try to, you get an `EnumException`

```python
@enum
class Palette: ...

p = Palette()	# illegal, raises EnumException
```

## Contributors

- **Simon** - [mightbesimon](https://github.com/mightbesimon)
- 👉 you? 👈
