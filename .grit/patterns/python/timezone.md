# Prefer timezone-aware datetimes to utcnow()

To get the current time in UTC use a datetime object with the timezone explicitly set to UTC.

```grit
engine marzano(0.1)
language python

or {
    and {
         $new_import = `timezone`,
         `datetime.utcnow()` => `datetime.now($new_import.utc)` where {
            $new_import <: ensure_import_from(source = `datetime`),
        }
    },
    `datetime.datetime.utcnow()` => `datetime.datetime.now(datetime.timezone.utc)`
}

```
## Example

```python
from datetime import datetime

print(datetime.utcnow())
```

## Result

```python
from datetime import datetime, timezone

print(datetime.now(timezone.utc))
```
