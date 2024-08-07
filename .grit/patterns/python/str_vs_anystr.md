# use-str-in-annotations

Consider using str instead of a the AnyStr generic type.

```grit
engine marzano(0.1)
language python

or {
    `from types import $imports` where {
        $values = [],
        $imports <: some bubble($values) `$import` where {
            if (! $import <: r"AnyStr|str") {
                $values += `$import`
            }
        },
        $length = length($values),
        if (! $length <: 0) {
            $new_data = join(list=$values, separator=", "),
            $new_data = `from types import $new_data`,
        }
        else {
            $new_data =``
        }
    } => $new_data,
    `AnyStr` => `str`,
}
```

## Example

```python
from types import AnyStr, Tuple, Optional
from types import AnyStr

def logic1(s: AnyStr) -> AnyStr:
    return 2 * s

def logic2() -> dict:
    return {}

something = True

def x(s: AnyStr) -> Tuple[Optional[AnyStr], Optional[dict]]:
   if something:
      return logic1(s), logic2()
   return None, None
```

## Result

```python
from types import Tuple, Optional

def logic1(s: str) -> str:
    return 2 * s

def logic2() -> dict:
    return {}

something = True

def x(s: str) -> Tuple[Optional[str], Optional[dict]]:
   if something:
      return logic1(s), logic2()
   return None, None
```
