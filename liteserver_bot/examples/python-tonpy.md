# Python: tonpy

Tonpy has LiteClient only in dev version (tonpy-dev) at the moment:

```
from tonpy import *

test = LiteClient(host="...", port=...,
                    pubkey_hex="...", timeout=5)

test.get_masterchain_info_ext().last
```
