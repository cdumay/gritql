# use-fstring

Consider using fstring instead of the builtin str.

```grit
engine marzano(0.1)
language python

`str($data)` where {
    $data <: maybe contains `"` => `'`
} => `f"{$data}"`
```

## Example

```python
print(str(5))
d = {"a": "toto"}
print(str(d["a"]))
```

## Result

```python
print(f"{5}")
d = {"a": "toto"}
print(f"{d['a']}")
```
